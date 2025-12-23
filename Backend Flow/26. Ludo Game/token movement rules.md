## 🚶 5. Token Movement Rules

```text
FUNCTION moveToken(player, tokenIndex, diceValue):

  token = player.tokens[tokenIndex]

  IF token is not open AND diceValue != 6
    REJECT move

  IF token is not open AND diceValue == 6
    token.isOpen = true
    token.position = startPosition
    RETURN

  IF token.position + diceValue > HOME_POSITION
    REJECT move

  token.position += diceValue

  IF token.position == HOME_POSITION
    token.isFinished = true
```
