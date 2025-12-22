## 5️⃣ Pseudocode — **Todo Statistics (Aggregation)**
Example output:  [{ byStatus: { _id: "done", count: 10 }], overdue: [{ overdue: 3 }] }
```bash
FUNCTION getTodoStats:

    --------------------------------------------------------------
    STEP 1: Capture the current date and time
    --------------------------------------------------------------
    SET now = CURRENT_DATETIME


    --------------------------------------------------------------
    STEP 2: Start MongoDB aggregation on the Todo collection
    --------------------------------------------------------------
    RUN AGGREGATION with the following stages:

        ----------------------------------------------------------
        STAGE 1: $match  → Filter active todos only
        ----------------------------------------------------------
        KEEP ONLY documents WHERE:
            softDelete == false


        ----------------------------------------------------------
        STAGE 2: $facet  → Run multiple calculations at once
        ----------------------------------------------------------
        CREATE two parallel pipelines:

            ──────────────────────────────────────────────────────
            PIPELINE A:  byStatus
            ──────────────────────────────────────────────────────
            GOAL: Count how many todos exist in each status

            STEPS:
                A1. GROUP documents BY the value of "status"
                    For each group:
                        - Output "_id" = status name
                        - Output "count" = number of documents in that group


            ──────────────────────────────────────────────────────
            PIPELINE B:  overdue
            ──────────────────────────────────────────────────────
            GOAL: Count how many todos are overdue and still pending

            STEPS:
                B1. FILTER documents WHERE:
                        dueDate < now          (deadline already passed)
                        AND status != "done"   (not completed yet)

                B2. COUNT how many documents matched
                    - Output field name = "overdue"


    --------------------------------------------------------------
    STEP 3: The aggregation returns an ARRAY with ONE element
    --------------------------------------------------------------
    SET stats = FIRST_ELEMENT of aggregation result


    --------------------------------------------------------------
    STEP 4: Send the final result to the client
    --------------------------------------------------------------
    RESPOND with:
        data = stats


END FUNCTION

```

---

## Big Mental Model 🧠

```
Read input
↓
Validate state (deleted / active)
↓
Update database atomically
↓
Increment version
↓
Log activity
↓
Send response
```

---

## Next-Level Improvement Ideas 💡

- 🔹 Use **MongoDB transactions**
    
    - Ensure Todo + Activity always stay in sync
        
- 🔹 Add **optimistic locking**
    
    - Reject update if version mismatch
        
- 🔹 Add **authorization**
    
    - Only owner can update/delete
        
- 🔹 Add **event-based logging**
    
    - Emit events instead of direct Activity writes
        
- 🔹 Add **materialized stats**
    
    - Cache stats for dashboards
        