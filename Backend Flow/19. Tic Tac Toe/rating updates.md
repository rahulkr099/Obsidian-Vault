## 11. Rating Update (ELO-like)

```
FUNCTION updateRatings(winner, loser):
  expectedWinner = formula
  ratings[winner] += K * (1 - expectedWinner)
  ratings[loser] -= K * (expectedWinner)
```
