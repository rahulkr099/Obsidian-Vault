## 🧩 1. Data Model (Poll)

```text
Poll
 ├─ id
 ├─ question
 ├─ options
 │   ├─ optionId
 │   ├─ text
 │   ├─ votes
 ├─ voters          // list of userIds who already voted
 ├─ expiresAt
 ├─ createdAt
```
