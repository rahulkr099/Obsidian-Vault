## 1. Server Initialization

```
START APPLICATION

Load environment variables

Create Express app

Enable JSON body parsing

Initialize local upload directory
  IF directory does not exist
    Create directory

Initialize AWS S3 client using credentials and region

Initialize in-memory storage for file metadata

Start server on PORT
```
