## 📊 5. Get Poll Results (Analytics)

```text
FUNCTION getPollResults(request):

  READ pollId FROM request.params

  FIND poll by pollId

  IF poll not found
     RETURN error "Poll not found"

  totalVotes = SUM of votes of all options

  FOR each option in poll.options
     percentage = (option.votes / totalVotes) * 100
     STORE option text, votes, percentage

  leadingOption = option with highest votes

  RETURN
    question
    totalVotes
    result list
    leadingOption
```
