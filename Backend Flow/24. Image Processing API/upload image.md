## 📤 3. Upload Image

```text
FUNCTION uploadImage(request):

  READ file from multipart request

  IF file is missing OR file size too large OR invalid type
    RETURN error

  SAVE file to storage
  GENERATE imageId

  STORE image metadata (optional DB)

  RETURN imageId and download URL
```
