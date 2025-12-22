DEFINE handleShortenURL
    READ URL, custom ID, expiry from request body
    READ user ID from authenticated request

    IF URL missing
        RETURN error response
    END

    VALIDATE URL format
    IF invalid
        RETURN error response
    END

    IF URL already exists in database
        RETURN existing short URL
    END

    GENERATE nano ID (custom or auto)
    IF custom ID provided AND already exists
        RETURN error response
    END

    CREATE new short URL entry in database
    RETURN generated short URL
END
