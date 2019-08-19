# PUT /payments/cancellation

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

## Success scenarios

### Required fields in request

:x: from
:x: business_service
:x: case_identification
- [ ] uetr (a list of accepted uetrs)
- [ ] underlying_cancellation_details -> cancellation_reason_information (return response body needs to match)

> Scenario 1 - Request to cancel a transaction with reason CUST

response: only if uetr in the request is "97ed4827-7b6f-4491-a06f-b548d5a7512d" AND underlying_cancellation_details -> cancellation_reason_information is "CUST"

```json
{
"cancel_transaction_response": {
"network_reference": "20190522000128293-010000068667"
}
}
```

> Scenario 2 - Request to cancel a transaction with reason DUPL

response: only if uetr in the request is "97ed4827-7b6f-4491-a06f-b548d5a7512d" AND underlying_cancellation_details -> cancellation_reason_information is "DUPL"

```json
{
"cancel_transaction_response": {
"network_reference": "20190522000128293-010000068667"
}
}
```
