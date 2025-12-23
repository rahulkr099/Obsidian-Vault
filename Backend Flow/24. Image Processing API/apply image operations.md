## 🧪 5. Apply Image Operations (Sharp Pipeline)

```text
FUNCTION applyOperations(imagePath, operations):

  image = LOAD image with Sharp

  FOR each operation IN operations:

    IF operation is "resize"
      image.resize(width, height, fit)

    IF operation is "crop"
      image.extract(left, top, width, height)

    IF operation is "format"
      image.convert(type, quality)

    IF operation is "watermark"
      CREATE watermark overlay
      image.composite(overlay)

  SAVE processed image to new file

  RETURN processed image path
```
