```
DEFINE refresh access token handler

READ refresh token from cookies, body, or headers

IF refresh token missing

RETURN unauthorized response

END

  

VERIFY refresh token using JWT

IF token invalid or expired

RETURN unauthorized response

END

  

FIND user using token data

IF user not found OR token does not match database

RETURN unauthorized response

END

  

GENERATE new access token

GENERATE new refresh token

UPDATE refresh token in database

  

SET new tokens as HTTP-only cookies

RETURN success response with new tokens

END
```