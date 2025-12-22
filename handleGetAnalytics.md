DEFINE handleGetAnalytics
    READ nano ID from request params
    IF nano ID missing
        RETURN error response
    END

    FIND URL entry by nano ID
    IF not found
        RETURN error response
    END

    RETURN URL analytics data
END
DEFINE handleGetAnalytics
    READ nano ID from request params
    IF nano ID missing
        RETURN error response
    END

    FIND URL entry by nano ID
    IF not found
        RETURN error response
    END

    RETURN URL analytics data
END