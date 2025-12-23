## 🗳️ 3. Vote on Poll (1 user = 1 vote)

```text
FUNCTION voteOnPoll(request):

  READ pollId FROM request.params
  READ optionIndex, userId FROM request.body

  FIND poll by pollId

  IF poll does not exist
     RETURN error "Poll not found"

  IF poll.expiresAt exists AND current time > expiresAt
     RETURN error "Poll expired"

  IF userId exists in poll.voters
     RETURN error "User already voted"

  IF optionIndex is invalid
     RETURN error "Invalid option"

  INCREMENT poll.options[optionIndex].votes by 1
  ADD userId to poll.voters

  SAVE poll

  EMIT real-time update (optional wow)

  RETURN success "Vote recorded"
```
