DEFINE authenticateGoogleRequest handler
    READ Google refresh token from cookies or request body

    IF refresh token missing
        RETURN unauthorized response
    END

    CALL refreshGoogleToken using refresh token
    RECEIVE new access token and refresh token

    SET new tokens as HTTP-only cookies
    RETURN success response with tokens
END
