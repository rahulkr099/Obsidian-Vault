## ❌ 7. Error Handling

```text
ON CSV parsing error:
  RETURN 400 with error message

ON stream failure:
  RETURN 500 with internal error

ON maxRows exceeded:
  STOP stream
  RETURN error
```
