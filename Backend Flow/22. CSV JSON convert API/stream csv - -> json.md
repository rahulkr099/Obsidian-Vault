## 🔁 4. Stream CSV → JSON (Core Logic)

```text
FUNCTION streamCSVtoJSON(inputStream, response, options):

  INIT csvParser with delimiter and header options

  rowCount = 0
  firstRow = true
  collectedRows = [] (only if pretty output)

  PIPE inputStream INTO csvParser

  FOR EACH parsedRow FROM csvParser:

    rowCount += 1

    IF sampleRows exists AND rowCount > sampleRows
      STOP parsing

    IF maxRows exists AND rowCount > maxRows
      THROW error "Row limit exceeded"

    IF ndjson == true
      WRITE JSON.stringify(parsedRow) + newline TO response

    ELSE IF pretty == true
      ADD parsedRow TO collectedRows

    ELSE
      IF firstRow
        WRITE "[" + JSON.stringify(parsedRow)
        firstRow = false
      ELSE
        WRITE "," + JSON.stringify(parsedRow)

  ON csvParser end:

    IF ndjson == true
      END response

    ELSE IF pretty == true
      WRITE JSON.stringify(collectedRows, formatted)
      END response

    ELSE
      IF no rows processed
        WRITE "[]"
      ELSE
        WRITE "]"
      END response
```
