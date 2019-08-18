# gpi-v3-sandbox-design
Design solution for gpi v3 dynamic sandbox.

For all dynamic responses, LAU response headers will be handled by the api gateway, thus out of scope in the discussion below. The following is only for the design of the response bodies. :shipit:

## PUT /payments/cancellation/status

### Errors on sandbox
- [ ] invalid_request (400)
- [ ] missing_mandatory_field (400)
- [ ] 500, 502, 503, 504 error response at random with uetr =  522ec102-f643-4b3c-995f-d62b7a27ec96

### Errors on gateway
- [ ] missing_headers (400)
- [ ] lau_error (400)
- [ ] authentication_failture (401)
- [ ] service_too_many_requests (429)
- [ ] system_too_many_requests (429)

:question: What's the difference between "service_too_many_requests" vs "system_too_many_requests"?

### Success scenarios

#### Required fields in request

:x: from
:x: business_service
:x: case_identification
:x: originator
- [ ] uetr
- [ ] underlying_cancellation_details->investigation_execution_status (return response body needs to match)

> Scenario 1 - Cancelled

Only if uetr in the request is "97ed4827-7b6f-4491-a06f-b548d5a7512d" AND

"underlying_cancellation_details": {
"investigation_execution_status": "CNCL"
},

response:
```json
{
"transaction_cancellation_status_response": {
"network_reference": "20190522000128293-010000068667-cncl"
}
}
```

> Scenario 2 - Pending, forwarded to next agent

Only if uetr in the request is "97ed4827-7b6f-4491-a06f-b548d5a7512d" AND 

"underlying_cancellation_details": {
"investigation_execution_status": "PDCR",
"investigation_execution_status_reason": {
"pending": "PTNA"
}

response:
```json
{
"transaction_cancellation_status_response": {
"network_reference": "20190522000128293-010000068667-ptna"
}
}
```

> Scenario 2 - Pending, debit authorisation requested from creditor

Only if uetr in the request is "97ed4827-7b6f-4491-a06f-b548d5a7512d" AND

"underlying_cancellation_details": {
"investigation_execution_status": "PDCR",
"investigation_execution_status_reason": {
"pending": "RQDA"
}

response:
```json
{
"transaction_cancellation_status_response": {
"network_reference": "20190522000128293-010000068667-rqda"
}
}
```

> Scenario 2 - Rejected, no answer from creditor.

Only if uetr in the request is "97ed4827-7b6f-4491-a06f-b548d5a7512d" AND
"underlying_cancellation_details": {
      "investigation_execution_status": "RJCR",
      "investigation_execution_status_reason": {
        "rejected": "NOAS"
      }

> response:
```json
{
"transaction_cancellation_status_response": {
"network_reference": "20190522000128293-010000068667-rjcr"
}
}
```
