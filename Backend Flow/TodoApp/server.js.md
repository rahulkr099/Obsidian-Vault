# server.js
```bash
Purpose: database connection and start the server

1.Require files and libraries
	IMPORT mongoose library
	IMPORT dotenv library
	IMPORT Express app

2.LOAD environment variables
	dotenv configuration
	SET port number
	SET MongoDB connection URL



3.DEFINE async function startServer
    TRY 
    4.  CONNECT to MongoDB with AWAIT
        PRINT "Connected to MongoDB"

    5.  START server on given port
        PRINT "Server running"

    CATCH error
    6.  PRINT error message
        EXIT application with 1

CALL startServer function

```
# Big Picture Flow (Easy to Remember)
```
Load configs
↓
Create Express app
↓
Attach middleware & routes
↓
Handle errors
↓
Connect database
↓
Start server

```
