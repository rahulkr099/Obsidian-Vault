DEFINE checkGoogleAccessToken handler
    READ Google access token from cookies or request body

    IF access token missing
        RETURN unauthorized response
    END

    FETCH user info from Google using access token
    IF fetch fails
        RETURN unauthorized response
    END

    FIND user in database using email from Google
    GENERATE Google middleware token for user

    SET Google access token and middleware token as HTTP-only cookies
    RETURN success response with user data
END