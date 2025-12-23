## 🌐 6. Convert CSV from Remote URL

```text
FUNCTION convertFromURL(request, response):

  READ url and options

  FETCH remote CSV as stream

  IF fetch fails
    RETURN error

  CALL streamCSVtoJSON(remoteStream, response, options)
```
