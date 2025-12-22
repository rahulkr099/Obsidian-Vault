## 7. Upload File to AWS S3

```
WHEN POST request to "/upload/s3"

  Use multer to extract file into memory

  IF file is missing or invalid
    RETURN error response

  IF S3 bucket is not configured
    RETURN server error

  Generate unique file ID

  Generate S3 object key
    - group files by date
    - include unique ID and original name

  Upload file buffer to S3

  Create metadata object
    - id
    - storage type = s3
    - original name
    - file size
    - mime type
    - S3 object key
    - upload time

  Store metadata in memory

  RETURN success response with metadata
```
