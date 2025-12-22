```
DEFINE signup handler

READ user details from request body

IF any required field missing

RETURN error response

END

IF user already exists in database

RETURN error response

END

HASH password

CREATE new user in database

RETURN success response

END
```