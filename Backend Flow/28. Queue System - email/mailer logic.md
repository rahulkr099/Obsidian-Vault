## ✉️ 5. Mailer Logic (SMTP / Ethereal)

```text
GLOBAL transporter

FUNCTION createTransporter():

  IF transporter exists
    RETURN transporter

  IF environment is development
    CREATE Ethereal test account
    transporter = CREATE SMTP transporter with Ethereal creds
  ELSE
    transporter = CREATE SMTP transporter using real SMTP creds

  RETURN transporter
```

```text
FUNCTION sendMail(emailData):

  transporter = createTransporter()

  info = transporter.sendMail(emailData)

  IF Ethereal
    ATTACH preview URL for debugging

  RETURN info
```

---
