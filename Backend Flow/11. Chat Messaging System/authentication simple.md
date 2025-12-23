## 5. Authentication (Simple / Stub)

```
WHEN user logs in

  IF username not provided
    RETURN error

  IF user exists
    RETURN existing user

  ELSE
    Create new user

  Generate token (simple userId for demo)

  RETURN token + user info
```
