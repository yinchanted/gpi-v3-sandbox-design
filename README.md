# gpi-v3-sandbox-design
Design solution for gpi v3 dynamic sandbox

## /payments/status

> request:

Only if uetr in the request is "97ed4827-7b6f-4491-a06f-b548d5a7512d"

> response:
```json
{
  "update_payment_status_request": {
    "from": "BANCDEFF",
    "business_service": "001",
    "update_payment_scenario": "CCTR",
    "uetr": "97ed4827-7b6f-4491-a06f-b548d5a7512d",
    "instruction_identification": "abc123",
    "payment_status": {
      "detailed_status": {
        "originator": "BANCDEFF",
        "funds_available": "2018-01-01T17:00:00.000Z",
        "transaction_status": {
          "status": "ACCC"
        },
        "return": false,
        "confirmed_amount": {
          "currency": "USD",
          "amount": "980."
        },
        "charge_amount": [
          {
            "currency": "USD",
            "amount": "20."
          }
        ]
      }
    }
  }
}
```
