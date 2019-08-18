# gpi-v3-sandbox-design
Design solution for gpi v3 dynamic sandbox.

For all dynamic responses, LAU response headers will be handled by the api gateway, thus out of scope in the discussion below. The following is only for the design of the response bodies. :shipit:

## GET /payments/events/invalid

### Errors on sandbox
- [ ] invalid_request (400)
- [ ] missing_mandatory_field (400)
- [ ] 500, 502, 503, 504 error response at random with uetr =  522ec102-f643-4b3c-995f-d62b7a27ec96
- [ ] "from_date_time" > "to_date_time"

:question: What error is returned if "from_date_time" is greater than "to_date_time"?

### Errors on gateway
- [ ] missing_headers (400)
- [ ] lau_error (400)
- [ ] authentication_failture (401)
- [ ] service_too_many_requests (429)
- [ ] system_too_many_requests (429)

:question: What's the difference between "service_too_many_requests" vs "system_too_many_requests"?

### Success scenarios

#### Required fields in request

:x: from_date_time
:x: to_date_time
:x: maximum_number
:x: next

> Scenario - return as many invalid events as possible

response:

```json
{
  "invalid_events_response": {
    "event": [
      {
        "uetr": "3a6fae6e-dc42-4145-bf95-ec6df7912b3b",
        "business_service": "001",
        "participant": true,
        "network_reference": "a1",
        "tracker_event_type": "COPT",
        "message_name_identification": "202COV.",
        "instruction_identification": "redundantInfo",
        "from": "BANABEBB",
        "to": "BANBUS33",
        "invalidity_reason": "INVA/X011"
      },
      {
        "uetr": "a6eda092-ef62-4f71-8189-42896da08605",
        "business_service": "002",
        "participant": true,
        "network_reference": "a2",
        "tracker_event_type": "CTTS",
        "message_name_identification": "199.",
        "instruction_identification": "updateNotAllowed",
        "from": "BANABEBB",
        "to": "TRCKCHZZ",
        "invalidity_reason": "INVA/X002"
      },
      {
        "uetr": "3578ba88-2205-4956-8696-899c5b223e35",
        "business_service": "005",
        "participant": true,
        "network_reference": "a3",
        "tracker_event_type": "CTSU",
        "message_name_identification": "199.",
        "instruction_identification": "notAParticipant",
        "from": "BANABEBB",
        "to": "BANBUSUS",
        "invalidity_reason": "INVA/X008"
      }
    ]
  }
}
```
