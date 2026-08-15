For a MERN developer, `kulala.nvim` is a great addition because you'll spend a lot of time testing:

- Express APIs
- Authentication endpoints
- JWT flows
- CRUD routes
- External APIs

without leaving Neovim.

---

# 1. Install Kulala

Create:

```bash
~/.config/nvim/lua/plugins/kulala.lua
```

```lua
return {
  {
    "mistweaverco/kulala.nvim",
    ft = "http",
    opts = {},
  },
}
```

Then:

```
:Lazy sync
```

Restart Neovim.

---

# 2. Create an HTTP Requests Folder

Inside your backend project:

```
backend/
├── src/
├── package.json
├── .env
└── requests/
    ├── auth.http
    ├── users.http
    └── posts.http
```

I usually keep all API testing files inside:

```
requests/
```

---

# 3. Create Your First Request

Example:

```
POST <http://localhost:5000/api/users>
Content-Type: application/json

{
  "name": "Rahul",
  "email": "rahul@gmail.com"
}
```

Save as:

```
users.http
```

---

# 4. Run the Request

Open:

```
users.http
```

Place cursor anywhere inside the request.

Run:

```
:lua require("kulala").run()
```

You will see:

```json
{
  "success": true,
  "user": {
    ...
  }
}
```

inside Neovim.

---

# 5. Add Useful Keymaps

Add to your keymaps:

```lua
vim.keymap.set("n", "<leader>hr", function()
  require("kulala").run()
end, { desc = "HTTP Run Request" })
```

Now:

```
<leader>hr
```

runs current request.

---

## Show Last Response

```lua
vim.keymap.set("n", "<leader>hp", function()
  require("kulala").jump_prev()
end, { desc = "Previous Request" })
```

---

## Jump Next Request

```lua
vim.keymap.set("n", "<leader>hn", function()
  require("kulala").jump_next()
end, { desc = "Next Request" })
```

---

# 6. Multiple Requests in One File

```
### Register User

POST <http://localhost:5000/api/auth/register>
Content-Type: application/json

{
  "name": "Rahul",
  "email": "rahul@gmail.com",
  "password": "123456"
}

### Login

POST <http://localhost:5000/api/auth/login>
Content-Type: application/json

{
  "email": "rahul@gmail.com",
  "password": "123456"
}

### Get Profile

GET <http://localhost:5000/api/auth/me>
```

The `###` separator creates multiple requests.

Move cursor into a request and run it.

---

# 7. Variables (Very Useful)

```
@baseUrl=http://localhost:5000

GET {{baseUrl}}/api/users
```

Now when your port changes:

```
@baseUrl=http://localhost:8000
```

you only update one line.

---

# 8. JWT Authentication

```
@token=eyJhbGciOi...

GET <http://localhost:5000/api/auth/me>
Authorization: Bearer {{token}}
```

Perfect for MERN authentication projects.

---

# 9. Environment Variables

Create:

```
.env.http
```

```
@baseUrl=http://localhost:5000
@token=YOUR_TOKEN
```

Then use:

```
GET {{baseUrl}}/api/users
Authorization: Bearer {{token}}
```

---

# 10. My Recommended MERN Workflow

When building an API:

```
1. Create route
2. Create controller
3. Start server
4. Open requests/auth.http
5. Test with <leader>hr
6. Fix bugs
7. Repeat
```

No browser.

No Postman.

No Thunder Client.

Everything stays inside:

```
tmux
├── nvim
├── server logs
└── git
```

which fits very well with your terminal-first Neovim workflow.

### Keymaps I'd use

```lua
vim.keymap.set("n", "<leader>hr", function()
  require("kulala").run()
end, { desc = "Run HTTP Request" })

vim.keymap.set("n", "<leader>hn", function()
  require("kulala").jump_next()
end, { desc = "Next Request" })

vim.keymap.set("n", "<leader>hp", function()
  require("kulala").jump_prev()
end, { desc = "Previous Request" })
```

For a MERN setup, I'd put Kulala right behind:

1. Telescope
2. Harpoon
3. Treesitter
4. LSP
5. Oil
6. Kulala

because API testing is something you'll do every day when building Express backends.