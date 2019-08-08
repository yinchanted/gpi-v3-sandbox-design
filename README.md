# gpi-v3-sandbox-design
Design solution for gpi v3 dynamic sandbox

## /payments/status
For all dynamic responses, LAU response headers will be handled by the api gateway, thus out of scope in the discussion below. The following is only for the design of the response bodies. :shipit:

> request:

Only if uetr in the request is "97ed4827-7b6f-4491-a06f-b548d5a7512d"

> response:
```json
{
  "update_payment_status_response": {
    "network_reference": "123."
  }
}
```

## /payments/{uetr}/transactions

> request:

Only if uetr in the request is "97ed4827-7b6f-4491-a06f-b548d5a7512d"

> response:
```json
{
  "payment_transaction_details_response": {
    "uetr": "97ed4827-7b6f-4491-a06f-b548d5a7512d",
    "transaction_status": {
      "status": "ACSP",
      "reason": "G000"
    },
    "cancellation_status": {
      "transaction_cancellation_status": "CNCL"
    },
    "initiation_time": "2018-01-01T09:00:00.000Z",
    "last_update_time": "2018-01-01T17:00:00.000Z",
    "payment_event": [
      {
        "network_reference": "abc",
        "message_name_identification": "103.",
        "business_service": "001",
        "tracker_event_type": "CTPT",
        "valid": true,
        "instruction_identification": "abc123.",
        "transaction_status": {
          "status": "ACSP",
          "reason": "G000"
        },
        "from": "BANABEBBXXX",
        "to": "BANBUS33XXX",
        "serial_parties": {
          "debtor_agent": "BANABEBB",
          "creditor_agent": "BANCDEFF"
        },
        "sender_acknowledgement_receipt": "2018-01-01T09:00:01.000Z",
        "received_date": "2018-01-01T09:00:02.000Z",
        "instructed_amount": {
          "currency": "USD",
          "amount": "1000."
        },
        "interbank_settlement_amount": {
          "currency": "USD",
          "amount": "1000."
        },
        "interbank_settlement_date": "2018-01-01T00:00:00.000Z",
        "charge_bearer": "DEBT",
        "last_update_time": "2018-01-01T09:00:03.000Z"
      },
      {
        "network_reference": "def",
        "message_name_identification": "199.",
        "business_service": "001",
        "tracker_event_type": "CTSU",
        "valid": true,
        "instruction_identification": "statusabc123.",
        "transaction_status": {
          "status": "ACSP",
          "reason": "G000"
        },
        "forwarded_to_agent": "BANCDEFF",
        "from": "BANBUS33XXX",
        "to": "TRCKCHZZXXX",
        "originator": "BANBUS33",
        "sender_acknowledgement_receipt": "2018-01-01T09:00:04.000Z",
        "confirmed_amount": {
          "currency": "USD",
          "amount": "1000."
        },
        "last_update_time": "2018-01-01T09:00:05.000Z"
      },
      {
        "network_reference": "ghi",
        "message_name_identification": "192.",
        "business_service": "002",
        "tracker_event_type": "CTCA",
        "valid": true,
        "case_identification": "123.",
        "original_instruction_identification": "abc123",
        "underlying_cancellation_details": {
          "cancellation_request_details": {
            "cancellation_reason_information": "DUPL",
            "indemnity_agreement": "INDM"
          }
        },
        "from": "BANABEBBXXX",
        "to": "TRCKCHZZXXX",
        "sender_acknowledgement_receipt": "2018-01-01T10:00:00.000Z",
        "last_update_time": "2018-01-01T10:00:00.000Z"
      },
      {
        "network_reference": "jkl",
        "message_name_identification": "192.",
        "business_service": "002",
        "tracker_event_type": "CTCA",
        "valid": true,
        "case_identification": "123.",
        "original_instruction_identification": "def567",
        "underlying_cancellation_details": {
          "cancellation_request_details": {
            "cancellation_reason_information": "DUPL",
            "indemnity_agreement": "INDM"
          }
        },
        "from": "TRCKCHZZXXX",
        "to": "BANCDEFFXXX",
        "sender_acknowledgement_receipt": "2018-01-01T10:00:01.000Z",
        "interbank_settlement_amount": {
          "currency": "USD",
          "amount": "1000."
        },
        "interbank_settlement_date": "2018-01-01T00:00:00.000Z",
        "last_update_time": "2018-01-01T10:00:05.000Z"
      },
      {
        "network_reference": "mno",
        "message_name_identification": "199.",
        "business_service": "002",
        "tracker_event_type": "CTTS",
        "valid": true,
        "instruction_identification": "trackref001.",
        "related_reference": "123.",
        "underlying_cancellation_details": {
          "cancellation_request_tracking_status": "S000"
        },
        "from": "TRCKCHZZXXX",
        "to": "BANABEBBXXX",
        "originator": "TRCKCHZZ",
        "sender_acknowledgement_receipt": "2018-01-01T10:00:01.000Z",
        "last_update_time": "2018-01-01T10:00:05.000Z"
      },
      {
        "network_reference": "pqr",
        "message_name_identification": "199.",
        "business_service": "002",
        "tracker_event_type": "CTTS",
        "valid": true,
        "instruction_identification": "trackref002.",
        "related_reference": "123.",
        "underlying_cancellation_details": {
          "cancellation_request_tracking_status": "S001"
        },
        "from": "TRCKCHZZXXX",
        "to": "BANABEBBXXX",
        "originator": "TRCKCHZZ",
        "sender_acknowledgement_receipt": "2018-01-01T10:00:02.000Z",
        "last_update_time": "2018-01-01T10:00:06.000Z"
      },
      {
        "network_reference": "stv",
        "message_name_identification": "199.",
        "business_service": "002",
        "tracker_event_type": "CTTS",
        "valid": true,
        "instruction_identification": "trackref003.",
        "related_reference": "123.",
        "underlying_cancellation_details": {
          "cancellation_request_tracking_status": "S002"
        },
        "from": "TRCKCHZZXXX",
        "to": "BANABEBBXXX",
        "originator": "TRCKCHZZ",
        "sender_acknowledgement_receipt": "2018-01-01T10:00:03.000Z",
        "last_update_time": "2018-01-01T10:00:07.000Z"
      },
      {
        "network_reference": "wyy",
        "message_name_identification": "199.",
        "business_service": "002",
        "tracker_event_type": "CTTS",
        "valid": true,
        "instruction_identification": "trackref004.",
        "related_reference": "123.",
        "underlying_cancellation_details": {
          "cancellation_request_tracking_status": "S003"
        },
        "from": "TRCKCHZZXXX",
        "to": "BANABEBBXXX",
        "originator": "TRCKCHZZ",
        "sender_acknowledgement_receipt": "2018-01-01T10:00:04.000Z",
        "last_update_time": "2018-01-01T10:00:08.000Z"
      },
      {
        "network_reference": "zab",
        "message_name_identification": "199.",
        "business_service": "002",
        "tracker_event_type": "CTTS",
        "valid": true,
        "instruction_identification": "trackref005.",
        "related_reference": "123.",
        "underlying_cancellation_details": {
          "cancellation_request_tracking_status": "S004"
        },
        "from": "TRCKCHZZXXX",
        "to": "BANABEBBXXX",
        "originator": "TRCKCHZZ",
        "sender_acknowledgement_receipt": "2018-01-01T10:00:05.000Z",
        "last_update_time": "2018-01-01T10:00:09.000Z"
      },
      {
        "network_reference": "zac",
        "message_name_identification": "196.",
        "business_service": "002",
        "tracker_event_type": "CTCR",
        "valid": true,
        "assignment_identification": "responseref",
        "resolved_case_identification": "123.",
        "underlying_cancellation_details": {
          "cancellation_response_details": {
            "investigation_execution_status": "CNCL"
          }
        },
        "from": "BANCDEFFXXX",
        "to": "TRCKCHZZXXX",
        "originator": "BANCDEFF",
        "sender_acknowledgement_receipt": "2018-01-01T11:00:00.000Z",
        "last_update_time": "2018-01-01T11:00:00.000Z"
      },
      {
        "network_reference": "zad",
        "message_name_identification": "196.",
        "business_service": "002",
        "tracker_event_type": "CTCR",
        "valid": true,
        "assignment_identification": "responseref",
        "resolved_case_identification": "123.",
        "underlying_cancellation_details": {
          "cancellation_response_details": {
            "investigation_execution_status": "CNCL"
          }
        },
        "from": "TRCKCHZZXXX",
        "to": "BANABEBBXXX",
        "originator": "TRCKCHZZ",
        "sender_acknowledgement_receipt": "2018-01-01T11:00:01.000Z",
        "last_update_time": "2018-01-01T11:00:05.000Z"
      }
    ]
  }
}
```
