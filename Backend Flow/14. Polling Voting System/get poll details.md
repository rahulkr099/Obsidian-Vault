## 📄 4. Get Poll Details

```text
FUNCTION getPoll(request):

  READ pollId FROM request.params

  FIND poll by pollId

  IF poll not found
     RETURN error "Poll not found"

  RETURN poll
```
