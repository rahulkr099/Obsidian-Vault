## 2. Multer Configuration (Validation Layer)

```
DEFINE allowed file types
  - JPEG
  - PNG
  - GIF
  - PDF

DEFINE max file size (5 MB)

FUNCTION fileFilter(file)
  IF file type NOT in allowed list
    Reject file
  ELSE
    Accept file
END FUNCTION
```
