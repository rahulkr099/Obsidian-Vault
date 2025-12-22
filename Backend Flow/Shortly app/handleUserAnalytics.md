DEFINE handleUserAnalytics
    READ user ID from authenticated request
    FIND all URLs for user
    IF no URLs found
        RETURN not found response
    END
    RETURN user analytics data
END