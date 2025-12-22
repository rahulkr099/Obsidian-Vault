DEFINE handleRedirect
    READ nano ID from request params
    IF nano ID missing
        RETURN error response
    END

    FIND URL entry by nano ID
    IF not found
        RETURN error response
    END

    IF URL expired
        RETURN expired response
    END

    READ referrer, device, browser, IP
    ADD visit record to history
    INCREMENT click count
    UPDATE last visited time
    SAVE URL entry

    REDIRECT to original URL
END