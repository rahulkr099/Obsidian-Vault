**Yes—but with an important distinction.**

For **API development and testing**, you can replace **90–95%** of what Postman and Insomnia do using command-line tools like `curl`, `jq`, and a few others. However, some GUI features are more convenient in Postman and Insomnia.

Here's a comparison:

|Feature|`curl` + CLI|Postman/Insomnia|
|---|---|---|
|GET, POST, PUT, PATCH, DELETE|✅|✅|
|Custom headers|✅|✅|
|JSON request body|✅|✅|
|Authentication (Bearer, Basic, API Key)|✅|✅|
|Cookies|✅|✅|
|File upload|✅|✅|
|Download files|✅|✅|
|View response headers|✅|✅|
|Format JSON|✅ (`jq`)|✅|
|Save requests|✅ (shell scripts/files)|✅|
|Environment variables|✅|✅|
|Collections|⚠️ Manual|✅|
|GUI request builder|❌|✅|
|Team collaboration|⚠️ Git/manual|✅|
|Automated API tests|✅|✅|
|Mock servers|⚠️ Possible with other tools|✅|
|API documentation|⚠️ Separate tools|✅|

## A complete CLI toolkit

These tools together cover almost everything:

### 1. curl

Send HTTP requests.

```bash
curl <https://api.github.com/users/octocat>
```

---

### 2. jq

Pretty-print and filter JSON.

```bash
curl <https://api.github.com/users/octocat> | jq
```

Extract one field:

```bash
curl <https://api.github.com/users/octocat> | jq '.followers'
```

---

### 3. fx (optional)

Interactive JSON explorer.

```bash
curl ... | fx
```

---

### 4. gron (optional)

Flatten JSON so it's searchable with `grep`.

```bash
curl ... | gron
```

---

### 5. xh or HTTPie (optional)

More human-friendly alternatives to `curl`.

```bash
xh POST api.example.com/users name=Rahul
```

or

```bash
http POST api.example.com/users name=Rahul
```

---

### 6. doggo

Test DNS.

```bash
doggo google.com
```

---

### 7. yq

Work with YAML.

```bash
cat docker-compose.yml | yq
```

---

### 8. bat

View saved responses with syntax highlighting.

```bash
bat response.json
```

---

### 9. fzf

Search through saved requests or scripts interactively.

---

## Example workflow

Instead of Postman:

```
POST /users
Authorization: Bearer token
Body:
{
    "name": "Rahul"
}
```

You can do:

```bash
TOKEN="your_token"

curl \
  -X POST \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"name":"Rahul"}' \
  <https://api.example.com/users> \
| jq
```

Everything happens in the terminal.

---

## What Postman still does better

A GUI can be more convenient for:

- Visual request builder
- Organizing large collections of requests
- Sharing collections with teammates
- One-click API documentation
- Visual environment management
- Mock servers and API monitoring

These aren't impossible from the terminal, but they usually require additional tools and more setup.

---

## As a backend developer

Based on your goal of becoming a Linux-focused backend developer, I would recommend making the **terminal your primary API tool**.

A strong stack would be:

- `curl` — send requests
- `jq` — inspect JSON
- `xh` or `HTTPie` — for quicker, more readable requests
- `doggo` — DNS troubleshooting
- `openssl` — SSL/TLS inspection
- `bat` — view files
- `fzf` — search history and scripts
- `tmux` — manage multiple terminal sessions

With this setup, you'll be able to do almost everything you'd use Postman or Insomnia for while building skills that transfer directly to servers, containers, CI/CD pipelines, and SSH sessions.

My suggestion is to **learn `curl` deeply first**. Once you're comfortable with it, you'll find that GUI tools become optional rather than essential, and you'll be much more effective when debugging APIs on remote Linux machines where no graphical interface is available.