Since you're learning backend development, Docker, Kubernetes, and Linux, **`yq`** is one of the most useful CLI tools you'll learn. You'll use it whenever you need to read or modify YAML files from the terminal.

---

# What is `yq`?

`yq` is a command-line tool for working with **YAML** files.

Think of it like this:

- `grep` → searches text
- `sed` → edits text
- `jq` → processes JSON
- **`yq` → processes YAML**

---

# Install

Ubuntu/Debian

```bash
sudo apt install yq
```

Check the version

```bash
yq --version
```

---

# Sample YAML

Create a file.

```bash
nano config.yaml
```

Paste this:

```yaml
app:
  name: TodoApp
  version: 1.0

server:
  host: localhost
  port: 5000

database:
  host: mongodb://localhost
  port: 27017

users:
  - Rahul
  - Amit
  - Priya
```

We'll use this file for every example.

---

# 1. Print the whole file

```bash
yq '.' config.yaml
```

Output

```yaml
app:
  name: TodoApp
  version: 1.0
server:
  host: localhost
  port: 5000
database:
  host: mongodb://localhost
  port: 27017
users:
  - Rahul
  - Amit
  - Priya
```

`.` means "the entire document."

---

# 2. Read one value

```bash
yq '.app.name' config.yaml
```

Output

```
TodoApp
```

---

Another example

```bash
yq '.server.port' config.yaml
```

Output

```
5000
```

---

# 3. Read nested values

```bash
yq '.database.host' config.yaml
```

Output

```
mongodb://localhost
```

---

# 4. Read array items

```bash
yq '.users'
```

Output

```yaml
- Rahul
- Amit
- Priya
```

---

First user

```bash
yq '.users[0]' config.yaml
```

Output

```
Rahul
```

---

Second user

```bash
yq '.users[1]' config.yaml
```

Output

```
Amit
```

---

# 5. Count array elements

```bash
yq '.users | length' config.yaml
```

Output

```
3
```

---

# 6. Change a value

Without changing the file:

```bash
yq '.server.port = 8000' config.yaml
```

Output

```yaml
server:
  port: 8000
```

The file is **not** modified.

---

# 7. Modify the file

Use `-i`.

```bash
yq -i '.server.port = 8000' config.yaml
```

Now open the file.

```bash
cat config.yaml
```

You'll see

```yaml
server:
  port: 8000
```

---

# 8. Add a new key

```bash
yq -i '.server.debug = true' config.yaml
```

Now

```yaml
server:
  host: localhost
  port: 8000
  debug: true
```

---

# 9. Delete a key

```bash
yq -i 'del(.server.host)' config.yaml
```

Result

```yaml
server:
  port: 8000
```

---

# 10. Add a new user

```bash
yq -i '.users += ["Neha"]' config.yaml
```

Now

```yaml
users:
  - Rahul
  - Amit
  - Priya
  - Neha
```

---

# 11. Remove an array item

```bash
yq -i 'del(.users[1])' config.yaml
```

Output

```yaml
users:
  - Rahul
  - Priya
  - Neha
```

---

# 12. Convert YAML to JSON

```bash
yq -o=json config.yaml
```

Output

```json
{
  "app": {
    "name": "TodoApp"
  }
}
```

---

# 13. Select multiple values

```bash
yq '.app.name, .server.port' config.yaml
```

Output

```
TodoApp
8000
```

---

# 14. Create a new field

```bash
yq -i '.app.author = "Rahul"' config.yaml
```

Result

```yaml
app:
  name: TodoApp
  version: 1.0
  author: Rahul
```

---

# 15. Read keys only

```bash
yq 'keys' config.yaml
```

Output

```yaml
- app
- database
- server
- users
```

---

# 16. Check if a key exists

```bash
yq 'has("database")' config.yaml
```

Output

```
true
```

---

# 17. Pretty-print another YAML file

```bash
cat config.yaml | yq
```

or

```bash
yq '.' config.yaml
```

---

# Real-world examples

## Docker Compose

Read the image for the `web` service:

```bash
yq '.services.web.image' docker-compose.yml
```

Change the image:

```bash
yq -i '.services.web.image = "nginx:latest"' docker-compose.yml
```

---

## Kubernetes Deployment

Get the number of replicas:

```bash
yq '.spec.replicas' deployment.yaml
```

Increase replicas:

```bash
yq -i '.spec.replicas = 5' deployment.yaml
```

---

## GitHub Actions

Get the workflow name:

```bash
yq '.name' .github/workflows/build.yml
```

List job names:

```bash
yq '.jobs | keys' .github/workflows/build.yml
```

---

# Practice exercises

Try these on your sample `config.yaml`:

1. Print the application version.
2. Print the database port.
3. Add `environment: production` under `app`.
4. Change the database host.
5. Add another user.
6. Delete the `version` field.
7. Count the number of users.
8. Convert the YAML file to JSON.

---

# Most useful commands to memorize

|Task|Command|
|---|---|
|Print file|`yq '.' file.yaml`|
|Read value|`yq '.server.port' file.yaml`|
|Read array item|`yq '.users[0]' file.yaml`|
|Update value|`yq -i '.server.port = 8080' file.yaml`|
|Add key|`yq -i '.debug = true' file.yaml`|
|Delete key|`yq -i 'del(.password)' file.yaml`|
|Convert to JSON|`yq -o=json file.yaml`|
|List keys|`yq 'keys' file.yaml`|
|Count array items|`yq '.users|

## Tips

- Always test your expression **without** `i` first. Once the output looks correct, rerun it with `i` to modify the file.
- `yq` has multiple implementations. The examples above are for **Mike Farah's `yq` (v4+)**, which is the version most tutorials use. If you installed `yq` from your distribution's package manager and commands behave differently, check the version with `yq --version`; you may need to install the Mike Farah release instead.

# gron

`gron` is a small but very powerful tool for **exploring unknown JSON**. Instead of writing complex `jq` filters, it converts JSON into simple assignment statements that you can search with tools like `grep`, `less`, or `fzf`.

Think of it like this:

- `jq` → Query and transform JSON
- `gron` → Flatten JSON so it's easy to search

---

# Install

Ubuntu/Debian

```bash
sudo apt install gron
```

Verify

```bash
gron --version
```

---

# Sample JSON

Create a file.

```bash
nano user.json
```

Paste this:

```json
{
  "user": {
    "name": "Rahul",
    "age": 21,
    "email": "rahul@example.com"
  },
  "skills": [
    "Python",
    "JavaScript",
    "Linux"
  ]
}
```

---

# 1. Flatten JSON

```bash
gron user.json
```

Output

```jsx
json = {};
json.user = {};
json.user.name = "Rahul";
json.user.age = 21;
json.user.email = "rahul@example.com";
json.skills = [];
json.skills[0] = "Python";
json.skills[1] = "JavaScript";
json.skills[2] = "Linux";
```

Notice how every value has its own line.

---

# 2. Search with grep

Find the email field.

```bash
gron user.json | grep email
```

Output

```jsx
json.user.email = "rahul@example.com";
```

---

Find the age.

```bash
gron user.json | grep age
```

Output

```jsx
json.user.age = 21;
```

---

# 3. Case-insensitive search

```bash
gron user.json | grep -i rahul
```

Output

```jsx
json.user.name = "Rahul";
```

---

# 4. Search nested values

Imagine this JSON:

```json
{
  "company": {
    "employees": {
      "manager": {
        "name": "Alice"
      }
    }
  }
}
```

Normally you'd inspect several levels.

With `gron`:

```bash
gron company.json | grep manager
```

Output

```jsx
json.company.employees.manager.name = "Alice";
```

---

# 5. Search API responses

Instead of saving a file:

```bash
curl <https://dummyjson.com/users/1> | gron
```

Search for email.

```bash
curl <https://dummyjson.com/users/1> | gron | grep email
```

Search for phone.

```bash
curl <https://dummyjson.com/users/1> | gron | grep phone
```

---

# 6. GitHub API example

```bash
curl <https://api.github.com/users/octocat> | gron
```

Find the avatar.

```bash
curl <https://api.github.com/users/octocat> | gron | grep avatar
```

---

# 7. Use less

Large JSON

```bash
gron huge.json | less
```

Search inside `less`.

```
/email
```

Press

```
n
```

for the next match.

---

# 8. Search with fzf

```bash
gron data.json | fzf
```

This lets you interactively search through flattened JSON.

---

# 9. Convert back to JSON

Suppose you only keep some lines:

```bash
gron user.json | grep name
```

Output

```jsx
json.user.name = "Rahul";
```

Convert back:

```bash
gron user.json | grep name | gron --ungron
```

Output

```json
{
  "user": {
    "name": "Rahul"
  }
}
```

---

# 10. View arrays

Input

```json
{
  "numbers": [10, 20, 30]
}
```

Output

```jsx
json.numbers[0] = 10;
json.numbers[1] = 20;
json.numbers[2] = 30;
```

Search

```bash
gron numbers.json | grep '\[1\]'
```

---

# 11. Debug unknown APIs

Instead of scrolling through hundreds of lines:

```bash
curl <https://dummyjson.com/products> | jq
```

Use

```bash
curl <https://dummyjson.com/products> | gron | grep title
```

You immediately see every `title` field.

---

# 12. Combine with wc

Count email fields.

```bash
gron users.json | grep email | wc -l
```

---

# 13. Combine with sort

```bash
gron users.json | sort
```

---

# 14. Combine with bat

```bash
gron user.json | bat
```

You'll get syntax highlighting.

---

# 15. Combine with rg (ripgrep)

Faster than `grep` on large outputs:

```bash
gron user.json | rg email
```

---

# Real-world examples

## GitHub CLI

```bash
gh api user | gron | grep login
```

---

## Kubernetes JSON

```bash
kubectl get pods -o json | gron | grep image
```

---

## Docker Inspect

```bash
docker inspect nginx | gron | grep IPAddress
```

---

## npm package info

```bash
npm view express --json | gron | grep version
```

---

## Terraform state

```bash
terraform show -json | gron | grep aws_instance
```

---

# When to use `gron` vs `jq`

Use **`gron`** when you don't know the JSON structure yet and want to explore it.

Use **`jq`** once you know the structure and want to extract or transform specific values.

For example:

```bash
curl <https://api.github.com/users/octocat> | gron | grep followers
```

shows you where the `followers` field is. Once you know the path, you can use:

```bash
curl <https://api.github.com/users/octocat> | jq '.followers'
```

to extract just that value.

---

# Practice exercises

Create a `student.json` file:

```json
{
  "student": {
    "name": "Rahul",
    "roll": 101,
    "department": "Computer Science"
  },
  "subjects": [
    "DSA",
    "OS",
    "DBMS"
  ]
}
```

Try these commands:

1. Show the flattened JSON.
    
2. Find the `department` field.
    
3. Find the `roll` field.
    
4. Search for `"DSA"`.
    
5. Count how many subject entries exist:
    
    ```bash
    gron student.json | grep 'subjects\[' | wc -l
    ```
    
6. Search interactively:
    
    ```bash
    gron student.json | fzf
    ```
    
7. Convert the `name` entry back to JSON:
    
    ```bash
    gron student.json | grep name | gron --ungron
    ```
    

## Commands to remember

|Task|Command|
|---|---|
|Flatten JSON|`gron file.json`|
|Search a field|`gron file.json|
|Interactive search|`gron file.json|
|Browse output|`gron file.json|
|Convert back to JSON|`gron --ungron`|
|Count matches|`gron file.json|

### A practical workflow

When working with a new REST API:

1. Fetch the response.
2. Pipe it to `gron`.
3. Search for the field you need with `grep` or `rg`.
4. Once you know the JSON path, switch to `jq` for precise extraction.

This combination is one of the fastest ways to understand unfamiliar JSON responses from APIs, Docker, Kubernetes, GitHub, and many other developer tools.

# fx

`fx` is an **interactive JSON viewer** for the terminal.

Unlike `jq`, which is used to filter and transform JSON, `fx` lets you **explore JSON visually**. It's especially useful when you receive a large API response and don't yet know its structure.

Think of it like this:

|Tool|Purpose|
|---|---|
|`jq`|Filter and transform JSON|
|`gron`|Flatten JSON for searching|
|`fx`|Interactively browse JSON|

---

# Install

Using npm

```bash
npm install -g fx
```

Verify

```bash
fx --version
```

---

# Sample JSON

Create a file.

```bash
nano user.json
```

Paste:

```json
{
  "user": {
    "name": "Rahul",
    "age": 21,
    "email": "rahul@example.com",
    "skills": [
      "Python",
      "JavaScript",
      "Linux"
    ]
  }
}
```

---

# 1. Open a JSON file

```bash
fx user.json
```

You'll see an interactive tree similar to:

```
▼ user
    name      Rahul
    age       21
    email     rahul@example.com
  ▼ skills
      [0] Python
      [1] JavaScript
      [2] Linux
```

---

# 2. Pipe JSON into `fx`

```bash
cat user.json | fx
```

or

```bash
curl <https://dummyjson.com/users/1> | fx
```

---

# 3. GitHub API example

```bash
curl <https://api.github.com/users/octocat> | fx
```

You can expand and collapse fields to inspect the response.

---

# 4. Docker example

```bash
docker inspect nginx | fx
```

Explore:

- NetworkSettings
- IPAddress
- Mounts
- Config
- Image

without writing any `jq` queries.

---

# 5. Kubernetes example

```bash
kubectl get pods -o json | fx
```

Expand:

```
items
 ├── metadata
 ├── spec
 ├── status
```

This is much easier than reading raw JSON.

---

# 6. npm package information

```bash
npm view express --json | fx
```

Explore:

- versions
- maintainers
- dependencies
- repository

---

# 7. Explore API responses

```bash
curl <https://dummyjson.com/products> | fx
```

Expand:

```
products
    product
        title
        price
        brand
        category
```

---

# 8. Keyboard shortcuts

|Key|Action|
|---|---|
|↑ / ↓|Move up and down|
|←|Collapse object or go back|
|→|Expand object|
|Enter|Expand/collapse|
|q|Quit|
|/|Search (in many versions)|

---

# 9. Pipe from another command

```bash
gh api user | fx
```

```bash
curl api.example.com/data | fx
```

```bash
cat response.json | fx
```

---

# 10. Use with `watch`

Refresh JSON every few seconds:

```bash
watch -n 2 'curl -s <https://dummyjson.com/users/1> | fx'
```

> Note: Because `fx` is interactive, using it with `watch` is mainly useful for quickly viewing refreshed output rather than interacting with it.

---

# 11. Compare with `jq`

Without `fx`

```bash
curl api.example.com | jq
```

Output

```json
{
  "user": {
    "name": "Rahul",
    "email": "rahul@example.com"
  }
}
```

With `fx`

```bash
curl api.example.com | fx
```

You can:

- expand nodes
- collapse nodes
- browse arrays
- inspect nested objects

No need to know the JSON structure beforehand.

---

# 12. Real-world examples

## GitHub CLI

```bash
gh api repos/octocat/Hello-World | fx
```

---

## Docker

```bash
docker inspect postgres | fx
```

---

## Kubernetes

```bash
kubectl get deployment nginx -o json | fx
```

---

## Terraform

```bash
terraform show -json | fx
```

---

## AWS CLI

```bash
aws ec2 describe-instances | fx
```

---

## Node.js package

```bash
npm view react --json | fx
```

---

# Typical workflow

Suppose you're working with an unfamiliar API.

### Step 1: Explore

```bash
curl api.example.com/users | fx
```

Find the field you're interested in.

---

### Step 2: Extract

```bash
curl api.example.com/users | jq '.users[].email'
```

---

### Step 3: Search quickly

```bash
curl api.example.com/users | gron | grep email
```

Each tool has a different role:

- `fx` → Discover the structure
- `gron` → Search for field names
- `jq` → Extract and transform data

---

# Practice exercises

Create this file:

```json
{
  "company": {
    "name": "OpenAI",
    "employees": [
      {
        "name": "Alice",
        "role": "Engineer"
      },
      {
        "name": "Bob",
        "role": "Designer"
      }
    ]
  }
}
```

Try:

```bash
fx company.json
```

Practice by:

1. Expanding `company`.
2. Opening `employees`.
3. Viewing the first employee.
4. Viewing the second employee.
5. Quitting with `q`.

---

# When to use `fx`

Use `fx` when you:

- Want to inspect a large JSON response visually.
- Don't know the JSON structure yet.
- Are debugging API responses.
- Are working with Docker, Kubernetes, GitHub, AWS, Terraform, or any tool that outputs JSON.

Once you've found the data you need, switch to `jq` for automation or scripting.

## Commands to remember

|Task|Command|
|---|---|
|Open a JSON file|`fx file.json`|
|Pipe JSON|`cat file.json|
|View an API response|`curl URL|
|GitHub CLI|`gh api user|
|Docker|`docker inspect <container>|
|Kubernetes|`kubectl get pods -o json|

For a backend/Linux developer, a great mental model is:

- **`fx`** → _Explore_ JSON.
- **`gron`** → _Search_ JSON.
- **`jq`** → _Process_ JSON.