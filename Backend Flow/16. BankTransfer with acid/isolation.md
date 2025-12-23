## 🚦 7. Isolation (Concurrent Transfers)

```text
DATABASE ensures:
- One transaction cannot see partial updates of another
- Parallel transfers don’t double-spend balance
```

(Optional improvement)

```text
USE version field
IF version changed
  RETRY transaction
```
