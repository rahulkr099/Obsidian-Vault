## 💸 4. Transfer Money (Main Logic)

```text
FUNCTION transferMoney(senderId, receiverId, amount):

  IF senderId == receiverId
    RETURN error "Cannot transfer to same account"

  START database session
  START transaction

  TRY
    sender = FIND account(senderId) USING session
    receiver = FIND account(receiverId) USING session

    IF sender OR receiver does not exist
      THROW "Account not found"

    IF sender.balance < amount
      THROW "Insufficient funds"

    sender.balance = sender.balance - amount
    SAVE sender USING session

    receiver.balance = receiver.balance + amount
    SAVE receiver USING session

    RECORD ledger entry with status = "success"

    COMMIT transaction
    END session

    RETURN success

  CATCH error
    ABORT transaction
    END session

    RECORD ledger entry with status = "failed"

    RETURN error
```
