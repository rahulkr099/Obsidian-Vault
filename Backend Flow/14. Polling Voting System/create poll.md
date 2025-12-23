## 🚀 2. Create Poll

```text
FUNCTION createPoll(request):

  READ question, options, expiresAt FROM request.body

  IF question is empty OR options length < 2
     RETURN error "Invalid poll data"

  CREATE poll
    poll.question = question
    poll.options = map options to { text, votes = 0 }
    poll.expiresAt = expiresAt
    poll.voters = empty list

  SAVE poll to database

  RETURN poll
```
