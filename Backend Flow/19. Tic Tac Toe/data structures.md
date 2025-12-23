## 4. Data Structures

### Matchmaking Queue

```
QUEUE waitingPlayers
```

---

### Room Store

```
ROOMS = {
  roomId: {
    players: [playerA, playerB],
    game: TicTacToeGame,
    ratings: { playerA: rating, playerB: rating },
    rematchVotes
  }
}
```

---

### Player Rating Store

```
RATINGS = {
  playerId: rating
}
```
