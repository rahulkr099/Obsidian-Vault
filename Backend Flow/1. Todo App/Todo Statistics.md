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
    This controller is doing **analytics using MongoDB aggregation**.  
Instead of returning individual todos, it returns **statistics about todos**.

Let’s walk through a **real example step-by-step**.

---

# 1️⃣ Database contains some todos

Assume the database currently has these documents.

```json
[
  {
    "_id": "1",
    "title": "Finish MERN project",
    "status": "pending",
    "dueDate": "2026-03-05",
    "softDelete": false
  },
  {
    "_id": "2",
    "title": "Practice DSA",
    "status": "done",
    "dueDate": "2026-03-01",
    "softDelete": false
  },
  {
    "_id": "3",
    "title": "Learn Docker",
    "status": "pending",
    "dueDate": "2026-03-12",
    "softDelete": false
  },
  {
    "_id": "4",
    "title": "Old removed task",
    "status": "pending",
    "softDelete": true
  }
]
```

Assume today's date:

```
2026-03-09
```

---

# 2️⃣ Frontend sends request

User opens **Dashboard page**.

Frontend calls:

```http
GET /todos/stats
```

The goal is to show something like:

```
Total Pending Tasks
Completed Tasks
Overdue Tasks
```

---

# 3️⃣ Controller starts

Your controller runs:

```javascript
const now = new Date();
```

Example value:

```
now = 2026-03-09
```

This will help detect **overdue tasks**.

---

# 4️⃣ Aggregation pipeline starts

```javascript
Todo.aggregate([
```

Aggregation pipeline processes data **step by step**.

Think of it like a **data processing pipeline**.

```
Todos → filter → group → count → result
```

---

# 5️⃣ First Stage: `$match`

```javascript
{ $match: { softDelete: false } }
```

This removes deleted tasks.

Remaining documents:

```json
[
  { "title": "Finish MERN project", "status": "pending", "dueDate": "2026-03-05" },
  { "title": "Practice DSA", "status": "done", "dueDate": "2026-03-01" },
  { "title": "Learn Docker", "status": "pending", "dueDate": "2026-03-12" }
]
```

Deleted task is ignored.

---

# 6️⃣ `$facet` splits the pipeline

This is a powerful MongoDB feature.

```javascript
$facet
```

means:

```
Run multiple aggregations in parallel
```

Your code runs **two analytics pipelines** at the same time:

```
1️⃣ byStatus
2️⃣ overdue
```

---

# 7️⃣ Pipeline 1: `byStatus`

```javascript
byStatus: [
  { $group: { _id: '$status', count: { $sum: 1 } } }
]
```

This groups todos by **status**.

Database processes:

```
pending
done
pending
```

Grouped result:

```json
[
  { "_id": "pending", "count": 2 },
  { "_id": "done", "count": 1 }
]
```

Meaning:

```
2 pending tasks
1 completed task
```

---

# 8️⃣ Pipeline 2: `overdue`

```javascript
{ $match: { dueDate: { $lt: now }, status: { $ne: 'done' } } }
```

Meaning:

```
dueDate < today
AND
status is not done
```

Let's check tasks.

|Task|Due Date|Status|Overdue|
|---|---|---|---|
|Finish MERN project|Mar 5|pending|✅|
|Practice DSA|Mar 1|done|❌|
|Learn Docker|Mar 12|pending|❌|

Only one task qualifies.

Then this runs:

```javascript
{ $count: 'overdue' }
```

Result:

```json
[
  { "overdue": 1 }
]
```

---

# 9️⃣ Final aggregation result

MongoDB returns:

```json
[
  {
    "byStatus": [
      { "_id": "pending", "count": 2 },
      { "_id": "done", "count": 1 }
    ],
    "overdue": [
      { "overdue": 1 }
    ]
  }
]
```

---

# 🔟 Controller sends response

Your code:

```javascript
res.json({ data: stats[0] });
```

Frontend receives:

```json
{
  "data": {
    "byStatus": [
      { "_id": "pending", "count": 2 },
      { "_id": "done", "count": 1 }
    ],
    "overdue": [
      { "overdue": 1 }
    ]
  }
}
```

---

# 1️⃣1️⃣ Frontend dashboard example

Frontend might display:

```
📊 Todo Statistics

Pending Tasks: 2
Completed Tasks: 1
Overdue Tasks: 1
```

---

# 🔁 Full Data Flow

```
User opens Dashboard
        │
        ▼
Frontend sends GET /todos/stats
        │
        ▼
Controller runs aggregation pipeline
        │
        ▼
Filter active todos
        │
        ▼
Run two analytics pipelines
   │           │
   ▼           ▼
Group by status   Find overdue tasks
   │           │
   ▼           ▼
Counts generated
        │
        ▼
Result returned to frontend
        │
        ▼
Dashboard shows statistics
```

---

# ⭐ Why this controller is powerful

This endpoint enables **dashboard analytics**.

Many real products have similar endpoints:

```
Jira task statistics
GitHub issue stats
Notion task dashboards
Trello board analytics
```

Instead of sending **1000 todos to frontend**, the backend directly sends **aggregated insights**.

Much faster and scalable.

---

💡 **Small improvement idea**

You could extend this endpoint to include:

```
totalTodos
completedToday
tasksCreatedToday
highPriorityTasks
```

That would make a **full productivity dashboard API**.

---

If you want, I can also show you **a simple visual diagram explaining MongoDB aggregation pipeline** so `$match`, `$group`, `$facet`, `$count` become extremely easy to understand.