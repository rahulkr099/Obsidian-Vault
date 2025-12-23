## 4. Pagination Helper

```
FUNCTION paginate(request):
  page = max(1, request.page OR 1)
  limit = min(100, request.limit OR 10)
  skip = (page - 1) * limit
  RETURN skip, limit
END FUNCTION
```
