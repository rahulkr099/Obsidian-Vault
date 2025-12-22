## 10. Generate S3 Signed Download URL (WOW Factor ⭐)

```
WHEN GET request to "/files/:id/signed-url"

  Find file metadata by ID

  IF file not found
    RETURN 404 error

  IF file storage type is NOT S3
    RETURN error (signed URL not applicable)

  Generate temporary signed URL from S3
    - valid for 5 minutes

  RETURN signed URL and expiry time
```
