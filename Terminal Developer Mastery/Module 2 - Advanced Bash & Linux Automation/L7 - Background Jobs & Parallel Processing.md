> **"One of the biggest performance improvements you can make is to stop doing independent work one task at a time."**

Many beginners write scripts like this:

```
Task A (5 sec)
      ↓
Task B (5 sec)
      ↓
Task C (5 sec)

Total = 15 sec
```

Professional scripts often run independent tasks **in parallel**:

```
Task A (5 sec) ─┐
Task B (5 sec) ─┼──► Done
Task C (5 sec) ─┘

Total ≈ 5 sec
```

This lesson teaches you how to safely run multiple commands at the same time.

---

# Learning Objectives

By the end of this lesson, you'll be able to:

- Run background jobs
- Synchronize parallel tasks
- Use `wait` effectively
- Capture exit statuses
- Limit concurrency
- Monitor running jobs
- Build faster automation scripts

**Estimated Time:** 7–9 hours

**Difficulty:** ⭐⭐⭐⭐☆

---

# Sequential Execution

Example:

```bash
sleep 3
sleep 3
sleep 3
```

Timeline:

```
0s ──► 3s ──► 6s ──► 9s
```

Total:

```
9 seconds
```

---

# Background Jobs

Add:

```bash
&
```

Example:

```bash
sleep 3 &
sleep 3 &
sleep 3 &
```

Timeline:

```
0s

Task A ─────┐
Task B ─────┤

Task C ─────┘

3s
```

Total:

```
3 seconds
```

---

# What Does `&` Do?

Instead of waiting...

Bash starts another process.

Example:

```bash
echo "One"

sleep 5 &

echo "Two"
```

Output:

```
One

Two
```

The shell continues immediately.

---

# Waiting

Without:

```bash
sleep 5 &
echo "Finished"
```

Output:

```
Finished
```

before the background task ends.

Use:

```bash
sleep 5 &

wait

echo "Finished"
```

Now Bash waits for all background jobs.

---

# Waiting for Specific Jobs

Example:

```bash
sleep 3 &
pid1=$!

sleep 5 &
pid2=$!

wait "$pid1"

echo "First done"

wait "$pid2"

echo "Second done"
```

---

# `$!`

Contains the PID of the **most recently started** background process.

```bash
sleep 10 &

echo "$!"
```

Example:

```
5423
```

---

# Running Multiple Commands

```bash
(
    sleep 3
    echo "Task A"
) &

(
    sleep 2
    echo "Task B"
) &
```

Each subshell runs independently.

---

# Capturing Exit Status

Suppose:

```bash
false &
pid=$!

wait "$pid"

echo $?
```

Output:

```
1
```

`wait` returns the exit status of the background process.

This is important for checking whether parallel tasks succeeded.

---

# Example — Parallel Downloads

```bash
curl -O file1 &
curl -O file2 &
curl -O file3 &

wait
```

Instead of downloading one after another.

---

# Example — Multiple Git Repositories

Instead of:

```
Repo1

↓

Repo2

↓

Repo3
```

Use:

```bash
git -C repo1 pull &
git -C repo2 pull &
git -C repo3 pull &

wait
```

Useful if you maintain many repositories.

---

# Example — Build Multiple Projects

```bash
npm run build --prefix frontend &
npm run build --prefix backend &

wait
```

Both builds happen simultaneously.

---

# Job Control

View jobs:

```bash
jobs
```

Example:

```
[1]+ Running sleep 100 &
```

---

# Bring to Foreground

```bash
fg %1
```

---

# Send to Background

Press:

```
Ctrl+Z
```

Then:

```bash
bg
```

---

# Parallel Loops

Example:

```bash
for dir in project1 project2 project3
do
    (
        cd "$dir" || exit
        git pull
    ) &
done

wait
```

This pattern is widely used for batch operations.

---

# Limiting Parallelism

Too many parallel jobs can overwhelm your system.

Simple approach:

```bash
max_jobs=4

for file in *.log
do
    process "$file" &

    while [ "$(jobs -r | wc -l)" -ge "$max_jobs" ]
    do
        sleep 1
    done
done

wait
```

This keeps at most four jobs running at once.

---

# Real Backend Example — Health Checks

Instead of:

```
Server1

↓

Server2

↓

Server3
```

Run together:

```bash
curl -s <http://server1/health> &
curl -s <http://server2/health> &
curl -s <http://server3/health> &

wait
```

This reduces monitoring time.

---

# Real Backend Example — Image Optimization

```bash
for image in images/*
do
    optimize "$image" &
done

wait
```

Great for CPU-bound tasks.

---

# Measuring Performance

Sequential:

```bash
time bash sequential.sh
```

Parallel:

```bash
time bash parallel.sh
```

Compare the execution times to see the benefit of concurrency.

---

# Avoid Race Conditions

Suppose two jobs write to the same file:

```bash
echo "A" >> output.txt &
echo "B" >> output.txt &
```

The order is unpredictable.

Better:

Each job writes to its own file:

```
result1.txt

result2.txt

result3.txt
```

Then combine them later.

---

# Backend Example — API Checks

```bash
for api in \
<https://api1.example.com/health> \
<https://api2.example.com/health>
do
    curl -s "$api" &
done

wait
```

This is a simple health-check dashboard.

---

# Hands-on Lab

Create:

```
parallel-demo.sh
```

Requirements:

Launch:

```bash
sleep 2
sleep 4
sleep 6
```

in parallel.

Print:

```
All jobs completed.
```

Measure the execution time with `time`.

---

# Mini Project

Create:

```
multi-repo-status.sh
```

Given:

```
projects/
├── api/
├── frontend/
├── admin/
├── docs/
```

Run:

```bash
git status
```

inside each repository **in parallel**.

Print a summary after all jobs finish.

---

# Common Mistakes

## Forgetting `wait`

Wrong:

```bash
task &
echo "Done"
```

The script may exit before the background task completes.

Correct:

```bash
task &

wait

echo "Done"
```

---

## Losing the PID

Wrong:

```bash
task &
```

Correct:

```bash
task &

pid=$!
```

Save the PID if you need to monitor or stop the process later.

---

## Launching Too Many Jobs

Starting hundreds of CPU-intensive tasks at once can reduce performance.

Limit concurrency when processing many items.

---

## Shared Output Files

Multiple jobs writing to the same file can produce mixed or corrupted output.

Prefer separate files or synchronization.

---

# Interview Questions

1. What does `&` do in Bash?
2. What is `$!`?
3. How does `wait` work?
4. How do you run multiple commands in parallel?
5. What is a race condition?
6. How would you limit the number of parallel jobs?
7. When should you use parallel processing?

---

# Cheat Sheet

```bash
# Background job
command &

# PID
pid=$!

# Wait for all
wait

# Wait for one
wait "$pid"

# Running jobs
jobs

# Background
bg

# Foreground
fg

# Measure execution time
time command
```

---

# Weekly Challenge 🚀

Build:

```
project-builder.sh
```

Input:

```
workspace/
├── frontend/
├── backend/
├── admin/
├── dashboard/
```

Requirements:

- Run `npm install` in every project **in parallel**.
- Then run `npm run build` in every project **in parallel**.
- Display a final report showing:
    - Successful builds
    - Failed builds
    - Total execution time

Store each project's log in a separate file.

---

# ⭐ Pro Challenge (Backend Engineer)

Create:

```
health-monitor.sh
```

Input:

```
servers.txt
```

Example:

```
<https://api.example.com/health>
<https://auth.example.com/health>
<https://admin.example.com/health>
```

Requirements:

1. Check all servers in parallel.
2. Record:
    - HTTP status
    - Response time
3. Wait for all checks.
4. Produce:

```
=========================
Health Report
=========================

API Server      ✓ 200  42ms

Auth Server     ✓ 200  55ms

Admin Server    ✗ 503  18ms

Total Servers : 3
Healthy       : 2
Unhealthy     : 1
```

This is similar to the health-check scripts used in monitoring systems and deployment pipelines.

---

# ⭐ Module 2 Progress

```
✅ Lesson 1 — Advanced Parameter Expansion
✅ Lesson 2 — Command Substitution & Process Substitution
✅ Lesson 3 — Here Documents & Here Strings
✅ Lesson 4 — Advanced Text Processing
✅ Lesson 5 — Regular Expressions
✅ Lesson 6 — Signals, Traps & Process Control
✅ Lesson 7 — Background Jobs & Parallel Processing

⬜ Lesson 8 — Scheduling (cron, at, systemd timers)
⬜ Lesson 9 — Writing Reusable Bash Libraries
⬜ Lesson 10 — API Automation with curl & JSON
⬜ Lesson 11 — Production Automation Projects
⬜ Lesson 12 — Final DevOps Toolkit Capstone
```

---

# 💡 Backend Engineer Insight

Parallel processing is one of the easiest ways to make automation significantly faster.

You'll encounter these patterns in:

- **CI/CD pipelines** that run tests concurrently.
- **Docker builds** executing independent stages.
- **Monitoring systems** checking multiple servers at once.
- **Monorepo tooling** building several packages in parallel.
- **Deployment scripts** updating multiple services simultaneously.

As you continue, keep asking: _"Can these tasks run independently?"_ If the answer is yes, parallel execution is often worth considering.

In **Lesson 8**, we'll move to **Scheduling** with `cron`, `at`, and `systemd` timers, where you'll learn how to automate tasks so they run at specific times or intervals without manual intervention.