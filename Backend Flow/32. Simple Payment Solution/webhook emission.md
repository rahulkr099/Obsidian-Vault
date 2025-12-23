## 🌐 9. Webhook Emission (Simulated)

```text
FUNCTION sendWebhook(event, payment):

  IF payment.metadata.webhook_url does not exist
    RETURN

  CREATE payload = { event, payment }

  SIGN payload using shared secret

  POST payload to webhook_url
```
