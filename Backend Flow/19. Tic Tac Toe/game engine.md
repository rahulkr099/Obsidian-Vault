## 5. Game Engine (Pure Logic)

### Initialize Game

```
FUNCTION initializeGame():
  board = [null x 9]
  currentPlayer = 'X'
  moves = 0
  finished = false
  winner = null
  history = []
```

---

### Validate Move

```
FUNCTION isValidMove(index):
  IF finished == true
    RETURN false
  IF index < 0 OR index > 8
    RETURN false
  IF board[index] is not null
    RETURN false
  RETURN true
```

---

### Make Move

```
FUNCTION makeMove(index):
  IF isValidMove(index) == false
    THROW error

  board[index] = currentPlayer
  add move to history
  moves += 1

  IF checkWin() == true
    finished = true
    winner = currentPlayer
    RETURN winner

  IF moves == 9
    finished = true
    winner = "draw"
    RETURN "draw"

  SWITCH currentPlayer
  RETURN null
```

---

### Check Win

```
FUNCTION checkWin():
  FOR each winningCombination
    IF all 3 positions have same symbol
      RETURN true
  RETURN false
```
