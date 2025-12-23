## 📜 10. Ledger / Journal (Real Banking Touch)

```text
ON transaction start:
  CREATE ledger record (status = started)

ON success:
  UPDATE ledger record (status = success)

ON failure:
  UPDATE ledger record (status = failed)
```

Used for audits, statements, and debugging.