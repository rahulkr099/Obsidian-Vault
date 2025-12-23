## 📥 3. Convert CSV (Main Endpoint)

```text
FUNCTION convertCSV(request, response):

  READ options from request (query/body)

  IF CSV provided as file upload
    inputStream = file stream
  ELSE IF CSV provided as raw body
    inputStream = request body stream
  ELSE
    RETURN error "No CSV provided"

  SET response content-type based on ndjson

  CALL streamCSVtoJSON(inputStream, response, options)
```
