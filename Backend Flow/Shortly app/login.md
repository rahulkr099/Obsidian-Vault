```
DEFINE login handler

READ email and password from request body

IF email or password missing

RETURN error response

END

  

FIND user by email

IF user not found

RETURN error response

END

  

COMPARE input password with stored password

IF password invalid

RETURN error response

END

  

GENERATE access token

GENERATE refresh token

SAVE refresh token in database

  

REMOVE sensitive fields from user data

SET access token and refresh token as HTTP-only cookies

RETURN success response with user data

END
```