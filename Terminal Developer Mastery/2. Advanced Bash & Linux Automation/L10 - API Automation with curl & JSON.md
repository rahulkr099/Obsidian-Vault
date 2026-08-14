> **"Modern backend engineering is impossible without APIs."**

Every day, backend developers interact with APIs:

- GitHub API
- OpenAI API
- Stripe API
- Twilio API
- Docker Hub API
- Kubernetes API
- AWS APIs
- Google APIs
- REST APIs
- GraphQL APIs

Bash is excellent for automating these interactions.

This lesson teaches you how to build production-quality API automation using `curl` and `jq`.

---

# Learning Objectives

By the end of this lesson, you'll be able to:

- Send HTTP requests with `curl`
- Work with all common HTTP methods
- Send headers and authentication
- Upload files
- Download files
- Parse JSON with `jq`
- Handle API errors
- Build reusable API clients
- Automate backend workflows

**Estimated Time:** 10–12 hours

**Difficulty:** ⭐⭐⭐⭐⭐

---

# What is an API?

An API (Application Programming Interface) allows applications to communicate.

```
Your Bash Script
        │
        ▼
      curl
        │
        ▼
 REST API Server
        │
        ▼
     JSON Response
```

Example:

```bash
curl <https://dummyjson.com/users/1>
```

Response:

```json
{
  "id": 1,
  "firstName": "Emily",
  "lastName": "Johnson"
}
```

---

# Installing `jq`

You already installed it earlier, but if needed:

Ubuntu/Debian:

```bash
sudo apt install jq
```

Verify:

```bash
jq --version
```

---

# Basic GET Request

```bash
curl <https://dummyjson.com/products/1>
```

---

Silent mode:

```bash
curl -s <https://dummyjson.com/products/1>
```

Removes the progress meter.

---

Follow redirects:

```bash
curl -L <https://example.com>
```

---

Fail on HTTP errors:

```bash
curl -fsSL <https://example.com>
```

Flags:

- `f` → fail on HTTP 4xx/5xx
- `s` → silent
- `S` → show errors
- `L` → follow redirects

This combination is excellent for scripts.

---

# Pretty Print JSON

```bash
curl -s <https://dummyjson.com/products/1> | jq
```

---

# Extract Fields

Example:

```bash
curl -s <https://dummyjson.com/users/1> | jq '.firstName'
```

Output:

```
"Emily"
```

Raw output:

```bash
jq -r '.firstName'
```

Output:

```
Emily
```

---

Multiple fields:

```bash
jq '{id, firstName, age}'
```

Output:

```json
{
  "id": 1,
  "firstName": "Emily",
  "age": 28
}
```

---

# Arrays

Example:

```json
{
  "users":[
    {"name":"Rahul"},
    {"name":"Amit"}
  ]
}
```

Extract names:

```bash
jq '.users[].name'
```

---

Count array length:

```bash
jq '.users | length'
```

---

Those are **command-line options (flags)** that tell `curl` how to make the HTTP request.

Here's your command:

```bash
curl \
-X POST \
-H "Content-Type: application/json" \
-d '{"name":"Rahul"}' \
<https://api.example.com/users>
```

Let's break it down.

### `curl`

The program itself. It sends HTTP requests to servers.

---

### `\` (backslash)

The backslash at the end of each line means:

> "Continue this command on the next line."

So this:

```bash
curl \
-X POST \
-H "Content-Type: application/json" \
-d '{"name":"Rahul"}' \
<https://api.example.com/users>
```

is exactly the same as:

```bash
curl -X POST -H "Content-Type: application/json" -d '{"name":"Rahul"}' <https://api.example.com/users>
```

---

## `X`

- `X` means **request method**.

Syntax:

```bash
-X METHOD
```

Example:

```bash
-X GET
-X POST
-X PUT
-X DELETE
-X PATCH
```

In your command:

```bash
-X POST
```

means

> "Send a POST request."

---

## `H`

- `H` means **HTTP Header**.

Syntax:

```bash
-H "Header-Name: Value"
```

Example:

```bash
-H "Content-Type: application/json"
```

This tells the server:

> "The data I'm sending is JSON."

You can send multiple headers:

```bash
-H "Authorization: Bearer TOKEN"
-H "Accept: application/json"
-H "Content-Type: application/json"
```

---

## `d`

- `d` means **data** (the request body).

Example:

```bash
-d '{"name":"Rahul"}'
```

This sends:

```json
{
  "name": "Rahul"
}
```

to the server.

Without `-d`, there would be no request body.

---

## URL

```bash
<https://api.example.com/users>
```

This is the endpoint where the request is sent.

---

# What happens step-by-step?

```bash
curl \
-X POST \
-H "Content-Type: application/json" \
-d '{"name":"Rahul"}' \
<https://api.example.com/users>
```

1. Start `curl`.
2. Use the **POST** method.
3. Tell the server the body is **JSON**.
4. Send this JSON:

```json
{
  "name": "Rahul"
}
```

1. Send it to:

```
<https://api.example.com/users>
```

---

# Common curl flags you'll use often

|Flag|Long form|Purpose|
|---|---|---|
|`-X`|`--request`|HTTP method (GET, POST, PUT, DELETE, etc.)|
|`-H`|`--header`|Add an HTTP header|
|`-d`|`--data`|Send request body|
|`-o`|`--output`|Save response to a file|
|`-O`|`--remote-name`|Save using the remote filename|
|`-i`|`--include`|Show response headers|
|`-I`|`--head`|Fetch only response headers|
|`-L`|`--location`|Follow redirects|
|`-u`|`--user`|Username and password (`user:pass`)|
|`-v`|`--verbose`|Show detailed request/response information|
|`-s`|`--silent`|Hide progress meter|
|`-k`|`--insecure`|Ignore SSL certificate verification (testing only)|
|`-A`|`--user-agent`|Set a custom User-Agent header|
|`-F`|`--form`|Send form data (e.g., file uploads)|

---

# Short vs. long options

Most `curl` options have both a short and a long form.

|Short|Long|
|---|---|
|`-X`|`--request`|
|`-H`|`--header`|
|`-d`|`--data`|
|`-o`|`--output`|
|`-O`|`--remote-name`|
|`-L`|`--location`|
|`-v`|`--verbose`|
|`-s`|`--silent`|

For example, these are equivalent:

```bash
curl -X POST -H "Content-Type: application/json"
```

and

```bash
curl --request POST --header "Content-Type: application/json"
```

The short forms are more common because they're quicker to type.

Since you're learning backend development and Linux, becoming comfortable with `curl` is very valuable. It's one of the fastest ways to test REST APIs directly from the terminal without opening tools like Postman or Insomnia.

# HTTP Methods 🥳

## GET

```bash
curl <https://api.example.com/users>
```

---

## POST

```bash
curl \
-X POST \
-H "Content-Type: application/json" \
-d '{"name":"Rahul"}' \
<https://api.example.com/users>
```

---

## PUT

```bash
curl \
-X PUT \
-H "Content-Type: application/json" \
-d '{"name":"Rahul Kumar"}' \
<https://api.example.com/users/1>
```

---

## PATCH

```bash
curl \
-X PATCH \
-H "Content-Type: application/json" \
-d '{"age":23}' \
<https://api.example.com/users/1>
```

---

## DELETE

```bash
curl -X DELETE <https://api.example.com/users/1>
```

---

# Headers

Example:

```bash
curl \
-H "Accept: application/json" \
-H "User-Agent: Bash Automation" \
<https://api.example.com>
```

---

# Authentication

Bearer token:

```bash
curl \
-H "Authorization: Bearer TOKEN" \
<https://api.example.com>
```

Store the token in an environment variable instead of hardcoding it:

```bash
curl \
-H "Authorization: Bearer $API_TOKEN" \
<https://api.example.com>
```

---

Basic authentication:

```bash
curl -u username:password
```

---

# Sending JSON

```bash
curl \
-X POST \
-H "Content-Type: application/json" \
-d @user.json \
<https://api.example.com/users>
```

The `@` symbol tells `curl` to read the request body from a file.

---

# Upload Files

```bash
curl \
-F "file=@photo.jpg" \
<https://api.example.com/upload>
```

---

# Download Files

```bash
curl \
-o report.pdf \
<https://example.com/report.pdf>
```

Keep the original filename:

```bash
curl -O <https://example.com/file.zip>
```

---

# HTTP Status Code

Capture only the status:

```bash
curl \
-o /dev/null \
-s \
-w "%{http_code}" \
<https://example.com>
```

Example:

```
200
```

---

# Response Time

```bash
curl \
-o /dev/null \
-s \
-w "%{time_total}\n" \
<https://example.com>
```

---

# Save Response and Status

```bash
response=$(curl -s \
    -w "\n%{http_code}" \
    <https://api.example.com>)

body=$(echo "$response" | sed '$d')
status=$(echo "$response" | tail -n1)
```

This lets you process the response body and status code separately.

---

# JSON Validation

Check if a file contains valid JSON:

```bash
jq empty data.json
```

If the JSON is invalid, `jq` exits with a non-zero status.

---

# Backend Example — Health Check

```bash
status=$(curl \
-o /dev/null \
-s \
-w "%{http_code}" \
<http://localhost:3000/health>)

if [[ "$status" == "200" ]]
then
    echo "Healthy"
else
    echo "Unhealthy"
fi
```

---

# Backend Example — GitHub API

```bash
curl \
-H "Accept: application/vnd.github+json" \
<https://api.github.com/repos/nodejs/node>
```

Extract stars:

```bash
jq '.stargazers_count'
```

---

# Backend Example — OpenWeather

```bash
curl \
"<https://api.openweathermap.org/>..."
```

Extract temperature:

```bash
jq '.main.temp'
```

---

# Backend Example — Docker Registry

```bash
curl \
<https://registry.hub.docker.com/v2/repositories/library/node/tags>
```

Extract tag names:

```bash
jq '.results[].name'
```

---

# Backend Example — REST Testing

Instead of Postman:

```bash
curl \
-X POST \
-H "Content-Type: application/json" \
-d '{"email":"test@test.com"}' \
<http://localhost:3000/api/users>
```

This is perfect for testing your own Express.js APIs.

---

# Building a Reusable API Function

```bash
api_get() {
    local url="$1"

    curl -fsSL "$url"
}
```

Usage:

```bash
api_get "<https://dummyjson.com/users/1>"
```

---

Improved version:

```bash
api_get_json() {
    local url="$1"

    curl -fsSL "$url" | jq
}
```

---

# Error Handling

```bash
if ! response=$(curl -fsSL "$url")
then
    echo "Request failed." >&2
    exit 1
fi
```

Always check whether API calls succeed.

---

# Rate Limiting

Avoid sending hundreds of requests per second.

Example:

```bash
sleep 1
```

between requests, or respect the API's documented rate limits.

---

# Hands-on Lab

Create:

```
weather.sh
```

Requirements:

- Ask for a city (or use a test endpoint if you don't have an API key).
- Call a weather API.
- Display:
    - Temperature
    - Humidity
    - Weather description

Use:

- `curl`
- `jq`

---

# Mini Project

Create:

```
api-monitor.sh
```

Input:

```
services.txt
```

Example:

```
<http://localhost:3000/health>
<https://example.com/health>
```

Output:

```
================================

Service Status

================================

API        200

Website    200

Admin      503

================================
```

Also record:

- Response time
- Timestamp

Save the report to a log file.

---

# Best Practices

## Use Environment Variables

Instead of:

```bash
TOKEN="abc123"
```

Use:

```bash
export API_TOKEN="..."
```

or load it from a secure `.env` file (outside version control).

---

## Fail Fast

Prefer:

```bash
curl -fsSL
```

over plain `curl` in scripts.

---

## Validate JSON

Don't assume the response is valid.

Use:

```bash
jq empty
```

---

## Quote Variables

Always:

```bash
curl "$url"
```

instead of:

```bash
curl $url
```

---

## Handle Timeouts

Example:

```bash
curl \
--connect-timeout 5 \
--max-time 15 \
<https://api.example.com>
```

This prevents scripts from hanging indefinitely.

---

# Common Mistakes

## Ignoring HTTP Status Codes

A request can return:

```
404
500
401
```

and still produce output.

Always check the status code if your logic depends on success.

---

## Hardcoding Secrets

Never commit:

```bash
API_KEY="secret"
```

to Git.

Use environment variables or a secure secrets manager.

---

## Forgetting `H "Content-Type: application/json"`

Many APIs require this header for JSON request bodies.

---

## Not Parsing JSON

Avoid trying to extract values with `grep` or `sed` when the response is valid JSON.

Use `jq` instead.

---

# Interview Questions

1. What is `curl` used for?
2. Explain the difference between GET and POST.
3. What does `jq` do?
4. How do you send JSON with `curl`?
5. How do you authenticate using a Bearer token?
6. How do you retrieve the HTTP status code?
7. Why should API keys be stored in environment variables?

---

# Cheat Sheet

```bash
# GET
curl <https://example.com>

# Silent + fail + redirects
curl -fsSL <https://example.com>

# POST JSON
curl -X POST \
-H "Content-Type: application/json" \
-d '{"name":"Rahul"}'

# Authorization
-H "Authorization: Bearer $API_TOKEN"

# Pretty JSON
jq

# Raw field
jq -r '.name'

# Count array
jq '.items | length'

# Download
curl -O URL

# Upload
curl -F "file=@image.png"

# HTTP status
curl -o /dev/null -s -w "%{http_code}"

# Response time
curl -o /dev/null -s -w "%{time_total}"
```

---

# Weekly Challenge 🚀

Build:

```
github-reporter.sh
```

Input:

```
repositories.txt
```

Example:

```
nodejs/node
expressjs/express
docker/cli
```

Requirements:

For each repository:

- Fetch repository details from the GitHub API.
- Display:
    - Stars
    - Forks
    - Open issues
    - Default branch
    - Last update time

Generate a neatly formatted report using `jq`.

---

# ⭐ Pro Challenge (Backend Engineer)

Build:

```
deployment-checker.sh
```

Input:

```
services.json
```

Example:

```json
[
  {
    "name": "API",
    "url": "<http://localhost:3000/health>"
  },
  {
    "name": "Auth",
    "url": "<http://localhost:4000/health>"
  }
]
```

Requirements:

1. Read the configuration with `jq`.
2. Check each service's health endpoint.
3. Record:
    - HTTP status
    - Response time
    - Timestamp
4. Retry failed requests up to three times with exponential backoff.
5. Produce a final summary showing healthy and unhealthy services.
6. Exit with a non-zero status if any service remains unhealthy.

This is very similar to the health-check scripts used in CI/CD pipelines before deployments.

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
✅ Lesson 8 — Scheduling (cron, at, systemd timers)
✅ Lesson 9 — Writing Reusable Bash Libraries
✅ Lesson 10 — API Automation with curl & JSON

⬜ Lesson 11 — Production Automation Projects
⬜ Lesson 12 — Final DevOps Toolkit Capstone
```

---

# 💡 Backend Engineer Insight

This lesson ties together many skills you've already learned:

- `curl` for HTTP requests
- `jq` for JSON parsing
- `grep`, `awk`, and `sed` for text processing
- Functions and libraries for reusable code
- Error handling with exit codes
- Scheduling with `cron` and `systemd`
- Parallel processing for faster API checks

Together, these form the foundation of many DevOps and backend automation workflows.

In **Lesson 11**, you'll build **Production Automation Projects** that combine everything you've learned in Module 2 into realistic, end-to-end tools—backup systems, deployment scripts, monitoring utilities, log analyzers, and maintenance automation similar to what engineers use in production environments every day.