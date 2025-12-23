## ⚙️ 4. Email Worker (Background Process)

```text
FUNCTION startWorker():

  queue = initQueue()

  PROCESS "send-email" jobs WITH concurrency = 5

    FOR each job:
      READ to, subject, text, html

      LOG "Processing job"

      CALL sendMail(to, subject, text, html)

      LOG "Email sent successfully"

      RETURN success
```
