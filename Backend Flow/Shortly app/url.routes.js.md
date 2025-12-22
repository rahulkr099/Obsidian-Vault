### 🔹 `url.routes.js` — PSEUDOCODE
[[Backend Flow/Shortly app/auth.middleware.js]]
[[url.controller.js]]
```text
IMPORT Router from Express
IMPORT Auth Middleware
IMPORT URL Controllers
IMPORT QR Code Service

CREATE Router Instance

ON POST "/shorten"
    APPLY Auth Middleware
    CALL Shorten URL Controller
END

ON GET "/:shortId"
    CALL Redirect Controller
END

ON GET "/analytics/:shortId"
    APPLY Auth Middleware
    CALL URL Analytics Controller
END

ON GET "/user/status"
    APPLY Auth Middleware
    CALL User Analytics Controller
END

ON POST "/generate-qr"
    APPLY Auth Middleware
    CALL QR Code Generator
END

EXPORT Router
```
