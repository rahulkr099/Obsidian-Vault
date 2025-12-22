# app.js
```bash
Purpose: Express setup for initialization of server

1.Require files and libraries
	IMPORT Express framework
	IMPORT express async errors handler
	IMPORT todo routes
	IMPORT centralized error handler

2.Initialize express app

3.ENABLE middleware:
	Parse JSON body
	Parse cookies
	Parse URL-encoded payloads

4.REGISTER "/todos" routes

5.CREATE "/healthz" route
    WHEN route is called
       - RETURN { ok: true }

6.HANDLE unknown routes
    IF route does not exist
        RETURN 404:
	       - success: false
	       - "Route not found"

7.REGISTER centralized error handler

8.EXPORT Express application to start the server
```
