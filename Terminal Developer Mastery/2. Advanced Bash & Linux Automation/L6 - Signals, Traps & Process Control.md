> **"Professional scripts don't just start correctly—they also stop correctly."**

Many beginners write scripts that work when everything goes well.

Professional engineers write scripts that also handle:

- `Ctrl+C`
- System shutdowns
- Unexpected failures
- Cleanup of temporary files
- Stopping child processes
- Releasing resources

This lesson teaches you how Linux communicates with processes using **signals**, and how Bash scripts can respond gracefully.

---

# Learning Objectives

By the end of this lesson, you'll be able to:

- Understand Linux signals
- Use `trap`
- Handle `Ctrl+C`
- Clean up temporary files
- Manage child processes
- Send signals with `kill`
- Inspect processes
- Write robust automation scripts

**Estimated Time:** 7–9 hours

**Difficulty:** ⭐⭐⭐⭐☆

---

# What is a Process?

Whenever you run:

```bash
node app.js
```

Linux creates a **process**.

Examples:

```bash
bash
git
node
python
docker
nginx
```

Everything running on Linux is a process.

---

# Process ID (PID)

Every process has a unique **Process ID**.

View running processes:

```bash
ps
```

Example:

```
PID   COMMAND

2145  bash

3178  node

4502  nginx
```

Show more details:

```bash
ps -ef
```

Or use an interactive viewer:

```bash
btop
```

(or `htop` if installed)

---

# What is a Signal?

A **signal** is a small message sent to a process.

Think of it as Linux saying:

```
Stop

Pause

Continue

Reload

Terminate
```

Signals let the operating system and users control processes.

---

# Common Signals

|Signal|Number|Purpose|
|---|---|---|
|`SIGINT`|2|Interrupt (`Ctrl+C`)|
|`SIGTERM`|15|Graceful termination|
|`SIGKILL`|9|Force kill (cannot be caught)|
|`SIGHUP`|1|Terminal closed / reload|
|`SIGQUIT`|3|Quit and produce core dump|
|`SIGSTOP`|19|Pause process|
|`SIGCONT`|18|Resume paused process|

---

# Viewing Signals

```bash
kill -l
```

Example output:

```
1) SIGHUP

2) SIGINT

3) SIGKILL

4) SIGTERM
```

---

# `Ctrl+C`

Suppose:

```bash
sleep 60
```

Press:

```
Ctrl+C
```

Linux sends:

```
SIGINT
```

The process exits.

---

# What is `trap`?

`trap` tells Bash:

> "When a particular signal arrives, run this command."

Syntax:

```bash
trap 'commands' SIGNAL
```

Example:

```bash
trap 'echo "Interrupted!"' SIGINT
```

Now pressing `Ctrl+C` prints:

```
Interrupted!
```

---

# Cleanup Example

Create a temporary file:

```bash
tmp=$(mktemp)

echo "Working..."
```

Without cleanup:

```
Ctrl+C

↓

Temporary file remains
```

With cleanup:

```bash
cleanup() {
    rm -f "$tmp"
    echo "Temporary file removed."
}

trap cleanup EXIT
```

Now the file is removed whether the script succeeds or fails.

---

# The `EXIT` Trap

`EXIT` is a special trap.

It runs when the script finishes for **any reason**:

- Success
- `exit`
- Error (with `set -e`)
- `Ctrl+C` (if not overridden)

Example:

```bash
cleanup() {
    echo "Cleaning..."
}

trap cleanup EXIT
```

---

# Handling `Ctrl+C`

```bash
cleanup() {
    echo
    echo "Interrupted by user."
    exit 130
}

trap cleanup SIGINT
```

Exit code `130` is commonly used for user interruptions.

---

# Multiple Signals

Handle more than one:

```bash
trap cleanup SIGINT SIGTERM
```

Now the same cleanup runs for either signal.

---

# Ignore a Signal

Sometimes you don't want a script interrupted.

```bash
trap '' SIGINT
```

Pressing `Ctrl+C` has no effect.

⚠️ Use this sparingly. Users generally expect `Ctrl+C` to work.

---

# Reset Default Behavior

```bash
trap - SIGINT
```

This restores the default action for `SIGINT`.

---

# Sending Signals

Start a process:

```bash
sleep 1000
```

Find its PID:

```bash
ps
```

Terminate gracefully:

```bash
kill 12345
```

Equivalent to:

```bash
kill -TERM 12345
```

---

# Force Kill

```bash
kill -9 12345
```

Sends:

```
SIGKILL
```

The process stops immediately.

⚠️ `SIGKILL` cannot be caught or ignored. It gives the program no chance to clean up.

Prefer `SIGTERM` first, and use `SIGKILL` only if necessary.

---

# Background Processes

Run:

```bash
sleep 100 &
```

Output:

```
[1] 5421
```

`5421` is the PID.

List background jobs:

```bash
jobs
```

---

# Bring Job to Foreground

```bash
fg
```

---

# Send Job to Background

Suspend with:

```
Ctrl+Z
```

Then:

```bash
bg
```

The job continues running in the background.

---

# Waiting for Child Processes

Example:

```bash
sleep 5 &

pid=$!

wait "$pid"

echo "Finished"
```

`$!` contains the PID of the most recently started background job.

`wait` pauses until it completes.

---

# Real Backend Example — Start Server

```bash
node server.js &

server_pid=$!

echo "Server PID: $server_pid"

wait "$server_pid"
```

Useful in test automation.

---

# Cleaning Child Processes

Example:

```bash
cleanup() {
    kill "$server_pid"
}

trap cleanup EXIT
```

If the script exits unexpectedly, the child process is also stopped.

This avoids leaving orphaned services running.

---

# Process Monitoring

Check if a process exists:

```bash
kill -0 "$pid"
```

If it exists:

Exit code:

```
0
```

Otherwise:

```
1
```

This sends no signal; it's simply a check.

---

# Backend Example — Wait for Server

```bash
until curl -s <http://localhost:3000> >/dev/null
do
    sleep 1
done

echo "Server Ready"
```

This waits until the application is accepting requests.

---

# Hands-on Lab

Create:

```
cleanup-demo.sh
```

Requirements:

1. Create a temporary file.
2. Print its path.
3. Sleep for 30 seconds.
4. Press `Ctrl+C`.
5. Verify the file is automatically deleted.

---

# Mini Project

Create:

```
server-runner.sh
```

Requirements:

- Start a Node.js application in the background.
- Save its PID.
- Wait until the server responds.
- Print "Server Ready".
- On exit, stop the Node.js process automatically.

This pattern is common in automated integration testing.

---

# Common Mistakes

## Using `kill -9` First

Wrong approach:

```bash
kill -9 1234
```

Preferred:

```bash
kill 1234
```

Only use `-9` if the process refuses to exit gracefully.

---

## Forgetting Cleanup

Without a cleanup handler:

```
Temporary files

↓

Still exist
```

Always clean up resources created by your script.

---

## Ignoring Child Processes

If your script launches background jobs, make sure they're terminated when the parent exits.

---

## Not Quoting PIDs

Always quote variables:

```bash
kill "$pid"
```

This helps avoid unexpected behavior if the variable is empty.

---

# Interview Questions

1. What is a Linux signal?
2. What does `SIGINT` represent?
3. What's the difference between `SIGTERM` and `SIGKILL`?
4. What does `trap` do?
5. When should you use an `EXIT` trap?
6. What does `$!` contain?
7. What is the purpose of `wait`?

---

# Cheat Sheet

```bash
# Trap Ctrl+C
trap cleanup SIGINT

# Trap exit
trap cleanup EXIT

# Multiple signals
trap cleanup SIGINT SIGTERM

# Reset trap
trap - SIGINT

# Ignore Ctrl+C
trap '' SIGINT

# Background process
sleep 10 &

# PID of last background job
pid=$!

# Wait
wait "$pid"

# Kill gracefully
kill "$pid"

# Force kill
kill -9 "$pid"

# List jobs
jobs

# Foreground
fg

# Background
bg

# Check process
kill -0 "$pid"
```

---

# Weekly Challenge 🚀

Build:

```
process-manager.sh
```

Supported commands:

```bash
./process-manager.sh start

./process-manager.sh stop

./process-manager.sh restart

./process-manager.sh status
```

Requirements:

- Store the application's PID in a file (for example, `app.pid`).
- Prevent multiple instances from running.
- Detect if the process is already stopped.
- Remove the PID file during cleanup.

This mirrors how many service managers operate.

---

# ⭐ Pro Challenge (Backend Engineer)

Create:

```
integration-test-runner.sh
```

Workflow:

```
Start Node Server
        │
        ▼
Wait Until Ready
        │
        ▼
Run Tests
        │
        ▼
Save Results
        │
        ▼
Always Stop Server
```

Requirements:

- Start the server in the background.
- Save its PID.
- Poll the health endpoint until it's ready.
- Run a placeholder test command.
- Use `trap` to guarantee the server is stopped even if the tests fail or the user presses `Ctrl+C`.

This is the same pattern used by many continuous integration systems.

---

# ⭐ Module 2 Progress

```
✅ Lesson 1 — Advanced Parameter Expansion
✅ Lesson 2 — Command Substitution & Process Substitution
✅ Lesson 3 — Here Documents & Here Strings
✅ Lesson 4 — Advanced Text Processing
✅ Lesson 5 — Regular Expressions
✅ Lesson 6 — Signals, Traps & Process Control

⬜ Lesson 7 — Background Jobs & Parallel Processing
⬜ Lesson 8 — Scheduling (cron, at, systemd timers)
⬜ Lesson 9 — Writing Reusable Bash Libraries
⬜ Lesson 10 — API Automation with curl & JSON
⬜ Lesson 11 — Production Automation Projects
⬜ Lesson 12 — Final DevOps Toolkit Capstone
```

---

# 💡 Backend Engineer Insight

The concepts from this lesson appear throughout modern backend infrastructure:

- **Docker** sends `SIGTERM` before stopping containers, giving applications a chance to shut down gracefully.
- **Node.js** applications often listen for `SIGINT` and `SIGTERM` to close database connections and finish in-flight requests.
- **CI/CD pipelines** start services, wait for them to become healthy, run tests, and always clean up—even if something fails.
- **System services** managed by `systemd` rely on proper signal handling for reliable start and stop behavior.

Learning to write scripts that clean up after themselves is a major step toward writing production-quality automation.

In **Lesson 7**, you'll learn **Background Jobs & Parallel Processing**, where you'll discover how to run multiple tasks concurrently, synchronize them, limit parallelism, and significantly speed up automation workflows.