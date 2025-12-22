## 9. Get Single File Metadata

```
WHEN GET request to "/files/:id"

  Search metadata store for matching ID

  IF not found
    RETURN 404 error

  RETURN file metadata
```
