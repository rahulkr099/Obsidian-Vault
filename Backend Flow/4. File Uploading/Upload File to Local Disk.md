## 6. Upload File to Local Disk

```
WHEN POST request to "/upload/local"

  Use multer to extract file from request

  IF file is missing or invalid
    RETURN error response

  Generate unique file ID

  Save file to local disk

  Create metadata object
    - id
    - storage type = local
    - original name
    - file size
    - mime type
    - local file path
    - upload time

  Store metadata in memory

  RETURN success response with metadata
```
