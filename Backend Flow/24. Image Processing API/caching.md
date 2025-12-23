## 🧠 9. Caching (Optional WOW)

```text
FUNCTION getCachedThumbnail(key):

  IF cache contains key
    RETURN cached image

  image = generate thumbnail
  STORE image in cache with TTL

  RETURN image
```
