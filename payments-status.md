# gpi-v3-sandbox-design
Design solution for gpi v3 dynamic sandbox.

For all dynamic responses, LAU response headers will be handled by the api gateway, thus out of scope in the discussion below. The following is only for the design of the response bodies. :shipit:

# PUT /payments/status

## Errors on sandbox
- [ ] invalid_request (400)
- [ ] missing_mandatory_field (400)
- [ ] 500, 502, 503, 504 error response at random with uetr =  522ec102-f643-4b3c-995f-d62b7a27ec96

## Errors on gateway
- [ ] missing_headers (400)
- [ ] lau_error (400)
- [ ] authentication_failture (401)
- [ ] service_too_many_requests (429)
- [ ] system_too_many_requests (429)

:question: What's the difference between "service_too_many_requests" vs "system_too_many_requests"?

:question: What is the error repo

## Success scenarios

### Required fields in request

:x: from
:x: instruction_identification
:x: confirmed_amount
- [ ] update_payment_scenario (return error if not one of the accepted ENUM)
- [ ] uetr (can only be from the list of acceptable UETRs)
- [ ] payment_status->transaction_status (return response body needs to match)

:question: What's the meaning of this attribute: "return"?
:question: What is the error response body when "uetr" provided cannot be found?

> Scenario 1 - ACCC

Only if uetr in the request is "6c475b07-1487-46b0-839e-5b6a810e19bc"

```json
{
  "update_payment_status_request": {
    "from": "BANCDEFF",
    "business_service": "001",
    "update_payment_scenario": "CCTR",
    "uetr": "6c475b07-1487-46b0-839e-5b6a810e19bc",
    "instruction_identification": "sandbox-payments-chain-first-leg",
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

response:

```json
{
  "payment_status_response": {
    "network_reference": "20190808193101560-010000000020-accc",
    "transaction_status": {
      "status": "ACCC"
    }
  }
}
```

> Scenario 2 - ACSP

Only if uetr in the request is "6c475b07-1487-46b0-839e-5b6a810e19bc"

```json
{
  "update_payment_status_request": {
    "from": "BANCDEFF",
    "business_service": "001",
    "update_payment_scenario": "CCTR",
    "uetr": "6c475b07-1487-46b0-839e-5b6a810e19bc",
    "instruction_identification": "sandbox-payments-chain-first-leg",
    "payment_status": {
      "detailed_status": {
        "originator": "BANCDEFF",
        "funds_available": "2018-01-01T17:00:00.000Z",
        "transaction_status": {
          "status": "ACSP",
          "reason": "G001"
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

response:

```json
{
  "payment_status_response": {
    "network_reference": "20190808193101560-010000000020-acsp",
    "transaction_status": {
      "status": "ACSP",
      "reason": "G001"
    }
  }
}
```

> Scenario 3 - RJCT

Only if uetr in the request is "6c475b07-1487-46b0-839e-5b6a810e19bc"

```json
{
  "update_payment_status_request": {
    "from": "BANCDEFF",
    "business_service": "001",
    "update_payment_scenario": "CCTR",
    "uetr": "6c475b07-1487-46b0-839e-5b6a810e19bc",
    "instruction_identification": "sandbox-payments-chain-first-leg",
    "payment_status": {
      "detailed_status": {
        "originator": "BANCDEFF",
        "funds_available": "2018-01-01T17:00:00.000Z",
        "transaction_status": {
          "status": "RJCT",
          "reason": "??" (find a reason code that match RJCT)
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

response:

```json
{
  "payment_status_response": {
    "network_reference": "20190808193101560-010000000020-rjct",
    "transaction_status": {
      "status": "RJCT",
      "reason": "??"
    }
  }
}
```
