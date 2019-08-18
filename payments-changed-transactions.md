# gpi-v3-sandbox-design
Design solution for gpi v3 dynamic sandbox.

For all dynamic responses, LAU response headers will be handled by the api gateway, thus out of scope in the discussion below. The following is only for the design of the response bodies. :shipit:

## GET /payments/changed/transactions

### Errors on sandbox
- [ ] invalid_request (400)
- [ ] missing_mandatory_field (400)
- [ ] 500, 502, 503, 504 error response at random with uetr =  522ec102-f643-4b3c-995f-d62b7a27ec96
- [ ] if from_date_time > to_date_time

### Errors on gateway
- [ ] missing_headers (400)
- [ ] lau_error (400)
- [ ] authentication_failture (401)
- [ ] service_too_many_requests (429)
- [ ] system_too_many_requests (429)

:question: What's the error if "from_date_time" is greater than "to_date_time"?

### Success scenarios

#### Required fields in request

:x: from_date_time
:x: to_date_time
:x: maximum_number
:x: next
- [ ] payment_scenario (return different responses for each ENUM)


> Scenario 1 - payment_scenario not set

response:

```json
{
  "changed_payment_transactions_response": {
    "payment_transaction": [
      {
        "uetr": "97ed4827-7b6f-4491-a06f-b548d5a7512d",
        "transaction_status": {
          "status": "ACCC"
        },
        "initiation_time": "2019-08-30T09:00:00.000Z",
        "completion_time": "2019-08-30T17:00:00.000Z",
        "last_update_time": "2019-08-30T17:00:00.000Z",
        "payment_event": [
          {
            "network_reference": "abc",
            "message_name_identification": "103",
            "business_service": "001",
            "tracker_event_type": "CTPT",
            "valid": true,
            "instruction_identification": "abc123",
            "transaction_status": {
              "status": "ACSP",
              "reason": "G000"
            },
            "return": false,
            "settlement_method": "INDA",
            "from": "BANABEBBXXX",
            "to": "BANBUS33XXX",
            "serial_parties": {
              "debtor_agent": "BANABEBBXXX",
              "creditor_agent": "BANDJPJTXXX"
            },
            "sender_acknowledgement_receipt": "2019-08-30T09:30:00.000Z",
            "received_date": "2019-08-30T09:30:00.000Z",
            "instructed_amount": {
              "currency": "USD",
              "amount": "1000"
            },
            "interbank_settlement_amount": {
              "currency": "USD",
              "amount": "990"
            },
            "interbank_settlement_date": "2019-08-30T00:00:00.000Z",
            "charge_bearer": "CRED",
            "charge_amount": [
              {
                "currency": "USD",
                "amount": "10"
              }
            ],
            "last_update_time": "2019-08-30T09:30:00.000Z"
          },
          {
            "network_reference": "def",
            "message_name_identification": "199",
            "business_service": "001",
            "tracker_event_type": "CTSU",
            "valid": true,
            "instruction_identification": "statusabc123",
            "transaction_status": {
              "status": "ACSP",
              "reason": "G000"
            },
            "return": false,
            "forwarded_to_agent": "BANCUS33XXX",
            "settlement_method": "INDA",
            "from": "BANBUS33XXX",
            "to": "TRCKCHZZXXX",
            "originator": "BANBUS33XXX",
            "sender_acknowledgement_receipt": "2019-08-30T10:00:00.000Z",
            "confirmed_amount": {
              "currency": "USD",
              "amount": "970"
            },
            "charge_bearer": "CRED",
            "charge_amount": [
              {
                "currency": "USD",
                "amount": "10"
              },
              {
                "currency": "USD",
                "amount": "20"
              }
            ],
            "last_update_time": "2019-08-30T10:00:00.000Z"
          },
          {
            "network_reference": "ghi",
            "message_name_identification": "103",
            "business_service": "001",
            "tracker_event_type": "CTPT",
            "valid": true,
            "instruction_identification": "def456",
            "transaction_status": {
              "status": "ACSP",
              "reason": "G000"
            },
            "return": false,
            "settlement_method": "INDA",
            "from": "BANCUS33XXX",
            "to": "BANDJPJTXXX",
            "serial_parties": {
              "debtor_agent": "BANABEBBXXX",
              "creditor_agent": "BANDJPJTXXX"
            },
            "sender_acknowledgement_receipt": "2019-08-30T10:30:00.000Z",
            "received_date": "2019-08-30T10:30:00.000Z",
            "instructed_amount": {
              "currency": "USD",
              "amount": "1000"
            },
            "interbank_settlement_amount": {
              "currency": "USD",
              "amount": "940"
            },
            "interbank_settlement_date": "2019-08-30T00:00:00.000Z",
            "charge_bearer": "CRED",
            "charge_amount": [
              {
                "currency": "USD",
                "amount": "10"
              },
              {
                "currency": "USD",
                "amount": "20"
              },
              {
                "currency": "USD",
                "amount": "30"
              }
            ],
            "last_update_time": "2019-08-30T10:30:00.000Z"
          },
          {
            "network_reference": "jkl",
            "message_name_identification": "199",
            "business_service": "001",
            "tracker_event_type": "CTSU",
            "valid": true,
            "instruction_identification": "statusdef456",
            "transaction_status": {
              "status": "ACCC"
            },
            "return": false,
            "funds_available": "2019-08-30T17:00:00.000Z",
            "from": "BANDJPJTXXX",
            "to": "TRCKCHZZXXX",
            "originator": "BANDJPJTXXX",
            "sender_acknowledgement_receipt": "2019-08-30T17:00:00.000Z",
            "confirmed_amount": {
              "currency": "USD",
              "amount": "900"
            },
            "charge_bearer": "CRED",
            "charge_amount": [
              {
                "currency": "USD",
                "amount": "10"
              },
              {
                "currency": "USD",
                "amount": "20"
              },
              {
                "currency": "USD",
                "amount": "30"
              },
              {
                "currency": "USD",
                "amount": "40"
              }
            ],
            "last_update_time": "2019-08-30T17:00:00.000Z"
          }
        ]
      },
      {
        "uetr": "46ed4827-7b6f-4491-a06f-b548d5a7512d",
        "transaction_status": {
          "status": "ACCC"
        },
        "initiation_time": "2019-08-30T09:00:00.000Z",
        "completion_time": "2018-01-01T17:00:00.000Z",
        "last_update_time": "2018-01-01T17:00:00.000Z",
        "payment_event": [
          {
            "network_reference": "abc",
            "message_name_identification": "103",
            "business_service": "001",
            "tracker_event_type": "CTPT",
            "valid": true,
            "instruction_identification": "abc123",
            "transaction_status": {
              "status": "ACSP",
              "reason": "G000"
            },
            "return": false,
            "settlement_method": "COVE",
            "from": "BANABEBBXXX",
            "to": "BANDJPJTXXX",
            "serial_parties": {
              "debtor_agent": "BANABEBBXXX",
              "instructing_reimbursement_agent": "BANBUS33XXX",
              "creditor_agent": "BANDJPJTXXX"
            },
            "sender_acknowledgement_receipt": "2019-08-30T09:00:00.000Z",
            "received_date": "2019-08-30T09:00:00.000Z",
            "instructed_amount": {
              "currency": "USD",
              "amount": "1000"
            },
            "interbank_settlement_amount": {
              "currency": "USD",
              "amount": "1000"
            },
            "interbank_settlement_date": "2019-08-30T00:00:00.000Z",
            "charge_bearer": "DEBT",
            "last_update_time": "2019-08-30T09:00:00.000Z"
          },
          {
            "network_reference": "def",
            "message_name_identification": "202COV",
            "business_service": "001",
            "tracker_event_type": "COPT",
            "valid": true,
            "instruction_identification": "def456",
            "related_reference": "abc123",
            "transaction_status": {
              "status": "ACSP",
              "reason": "G000"
            },
            "return": false,
            "settlement_method": "INDA",
            "from": "BANABEBBXXX",
            "to": "BANBUS33XXX",
            "cover_parties": {
              "debtor": "BANABEBBXXX",
              "debtor_agent": "BANBUS33XXX",
              "creditor_agent": "BANCUS33XXX",
              "creditor": "BANDJPJTXXX"
            },
            "sender_acknowledgement_receipt": "2019-08-30T09:05:00.000Z",
            "received_date": "2019-08-30T09:05:00.000Z",
            "interbank_settlement_amount": {
              "currency": "USD",
              "amount": "1000"
            },
            "interbank_settlement_date": "2019-08-30T00:00:00.000Z",
            "last_update_time": "2019-08-30T09:05:00.000Z"
          },
          {
            "network_reference": "ghi",
            "message_name_identification": "202COV",
            "business_service": "001",
            "tracker_event_type": "COPT",
            "valid": true,
            "instruction_identification": "ghi789",
            "related_reference": "abc123",
            "transaction_status": {
              "status": "ACSP",
              "reason": "G000"
            },
            "return": false,
            "settlement_method": "CLRG",
            "clearing_system": "FDW",
            "from": "BANBUS33XXX",
            "to": "BANCUS33XXX",
            "cover_parties": {
              "debtor": "BANABEBBXXX",
              "debtor_agent": "BANBUS33XXX",
              "creditor_agent": "BANCUS33XXX",
              "creditor": "BANDJPJTXXX"
            },
            "sender_acknowledgement_receipt": "2019-08-30T09:10:00.000Z",
            "received_date": "2019-08-30T09:10:00.000Z",
            "interbank_settlement_amount": {
              "currency": "USD",
              "amount": "1000"
            },
            "interbank_settlement_date": "2019-08-30T00:00:00.000Z",
            "last_update_time": "2019-08-30T09:10:00.000Z"
          },
          {
            "network_reference": "jkl",
            "message_name_identification": "299",
            "business_service": "001",
            "tracker_event_type": "COSU",
            "valid": true,
            "instruction_identification": "jkl000",
            "transaction_status": {
              "status": "ACCC"
            },
            "return": false,
            "funds_available": "2019-08-30T16:00:00.000Z",
            "from": "BANCUS33XXX",
            "to": "TRCKCHZZXXX",
            "originator": "BANCUS33XXX",
            "sender_acknowledgement_receipt": "2019-08-30T16:00:00.000Z",
            "confirmed_amount": {
              "currency": "USD",
              "amount": "1000"
            },
            "last_update_time": "2019-08-30T16:00:00.000Z"
          },
          {
            "network_reference": "mno",
            "message_name_identification": "199",
            "business_service": "001",
            "tracker_event_type": "CTSU",
            "valid": true,
            "instruction_identification": "mno000",
            "transaction_status": {
              "status": "ACCC"
            },
            "return": false,
            "funds_available": "2019-08-30T17:00:00.000Z",
            "from": "BANDJPJTXXX",
            "to": "TRCKCHZZXXX",
            "originator": "BANDJPJTXXX",
            "sender_acknowledgement_receipt": "2019-08-30T17:00:00.000Z",
            "confirmed_amount": {
              "currency": "USD",
              "amount": "1000"
            },
            "last_update_time": "2019-08-30T17:00:00.000Z"
          }
        ]
      },
      {
        "uetr": "54ed4827-7b6f-4491-a06f-b548d5a7512d",
        "transaction_status": {
          "status": "RJCT",
          "reason": "FOCR"
        },
        "cancellation_status": {
          "transaction_cancellation_status": "CNCL"
        },
        "cases": "1",
        "initiation_time": "2019-08-30T09:00:00.000Z",
        "completion_time": "2019-08-30T17:00:00.000Z",
        "last_update_time": "2019-08-30T17:00:00.000Z",
        "payment_event": [
          {
            "network_reference": "abc",
            "message_name_identification": "103",
            "business_service": "001",
            "tracker_event_type": "CTPT",
            "valid": true,
            "instruction_identification": "abc123",
            "transaction_status": {
              "status": "ACSP",
              "reason": "G000"
            },
            "return": false,
            "settlement_method": "INDA",
            "from": "BANABEBBXXX",
            "to": "BANBUS33XXX",
            "serial_parties": {
              "debtor_agent": "BANABEBB",
              "creditor_agent": "BANCDEFF"
            },
            "sender_acknowledgement_receipt": "2019-08-30T09:00:01.000Z",
            "received_date": "2019-08-30T09:00:02.000Z",
            "instructed_amount": {
              "currency": "USD",
              "amount": "1000"
            },
            "interbank_settlement_amount": {
              "currency": "USD",
              "amount": "1000"
            },
            "interbank_settlement_date": "2019-08-30T00:00:00.000Z",
            "charge_bearer": "DEBT",
            "last_update_time": "2019-08-30T09:00:03.000Z"
          },
          {
            "network_reference": "def",
            "message_name_identification": "199",
            "business_service": "001",
            "tracker_event_type": "CTSU",
            "valid": true,
            "instruction_identification": "statusabc123",
            "transaction_status": {
              "status": "ACSP",
              "reason": "G000"
            },
            "return": false,
            "forwarded_to_agent": "BANCDEFF",
            "settlement_method": "INDA",
            "from": "BANBUS33XXX",
            "to": "TRCKCHZZXXX",
            "originator": "BANBUS33",
            "sender_acknowledgement_receipt": "2019-08-30T09:00:04.000Z",
            "confirmed_amount": {
              "currency": "USD",
              "amount": "1000."
            },
            "charge_bearer": "DEBT",
            "last_update_time": "2019-08-30T09:00:05.000Z"
          },
          {
            "network_reference": "ghi",
            "message_name_identification": "192",
            "business_service": "002",
            "tracker_event_type": "CTCA",
            "valid": true,
            "case_identification": "123",
            "original_instruction_identification": "abc123",
            "return": false,
            "underlying_cancellation_details": {
              "cancellation_request_details": {
                "cancellation_reason_information": "DUPL",
                "indemnity_agreement": "INDM"
              }
            },
            "from": "BANABEBBXXX",
            "to": "TRCKCHZZXXX",
            "sender_acknowledgement_receipt": "2019-08-30T10:00:00.000Z",
            "last_update_time": "2019-08-30T10:00:00.000Z"
          },
          {
            "network_reference": "jkl",
            "message_name_identification": "192",
            "business_service": "002",
            "tracker_event_type": "CTCA",
            "valid": true,
            "case_identification": "123",
            "original_instruction_identification": "def567",
            "return": false,
            "underlying_cancellation_details": {
              "cancellation_request_details": {
                "cancellation_reason_information": "DUPL",
                "indemnity_agreement": "INDM"
              }
            },
            "from": "TRCKCHZZXXX",
            "to": "BANCDEFFXXX",
            "sender_acknowledgement_receipt": "2019-08-30T10:00:01.000Z",
            "interbank_settlement_amount": {
              "currency": "USD",
              "amount": "1000"
            },
            "interbank_settlement_date": "2019-08-30T00:00:00.000Z",
            "last_update_time": "2019-08-30T10:00:05.000Z"
          },
          {
            "network_reference": "mno",
            "message_name_identification": "199",
            "business_service": "002",
            "tracker_event_type": "CTTS",
            "valid": true,
            "instruction_identification": "trackref001",
            "related_reference": "123",
            "return": false,
            "underlying_cancellation_details": {
              "cancellation_request_tracking_status": "S000"
            },
            "from": "TRCKCHZZXXX",
            "to": "BANABEBBXXX",
            "originator": "TRCKCHZZ",
            "sender_acknowledgement_receipt": "2019-08-30T10:00:01.000Z",
            "last_update_time": "2018-01-01T10:00:05.000Z"
          },
          {
            "network_reference": "pqr",
            "message_name_identification": "199",
            "business_service": "002",
            "tracker_event_type": "CTTS",
            "valid": true,
            "instruction_identification": "trackref002",
            "related_reference": "123",
            "return": false,
            "underlying_cancellation_details": {
              "cancellation_request_tracking_status": "S001"
            },
            "from": "TRCKCHZZXXX",
            "to": "BANABEBBXXX",
            "originator": "TRCKCHZZ",
            "sender_acknowledgement_receipt": "2019-08-30T10:00:02.000Z",
            "last_update_time": "2019-08-30T10:00:06.000Z"
          },
          {
            "network_reference": "stv",
            "message_name_identification": "199",
            "business_service": "002",
            "tracker_event_type": "CTTS",
            "valid": true,
            "instruction_identification": "trackref003",
            "related_reference": "123",
            "return": false,
            "underlying_cancellation_details": {
              "cancellation_request_tracking_status": "S002"
            },
            "from": "TRCKCHZZXXX",
            "to": "BANABEBBXXX",
            "originator": "TRCKCHZZ",
            "sender_acknowledgement_receipt": "2019-08-30T10:00:03.000Z",
            "last_update_time": "2019-08-30T10:00:07.000Z"
          },
          {
            "network_reference": "wyy",
            "message_name_identification": "199",
            "business_service": "002",
            "tracker_event_type": "CTTS",
            "valid": true,
            "instruction_identification": "trackref004",
            "related_reference": "123",
            "return": false,
            "underlying_cancellation_details": {
              "cancellation_request_tracking_status": "S003"
            },
            "from": "TRCKCHZZXXX",
            "to": "BANABEBBXXX",
            "originator": "TRCKCHZZ",
            "sender_acknowledgement_receipt": "2019-08-30T10:00:04.000Z",
            "last_update_time": "2019-08-30T10:00:08.000Z"
          },
          {
            "network_reference": "zab",
            "message_name_identification": "199",
            "business_service": "002",
            "tracker_event_type": "CTTS",
            "valid": true,
            "instruction_identification": "trackref005",
            "related_reference": "123",
            "return": false,
            "underlying_cancellation_details": {
              "cancellation_request_tracking_status": "S004"
            },
            "from": "TRCKCHZZXXX",
            "to": "BANABEBBXXX",
            "originator": "TRCKCHZZ",
            "sender_acknowledgement_receipt": "2019-08-30T10:00:05.000Z",
            "last_update_time": "2019-08-30T10:00:09.000Z"
          },
          {
            "network_reference": "zac",
            "message_name_identification": "196",
            "business_service": "002",
            "tracker_event_type": "CTCR",
            "valid": true,
            "case_identification": "123",
            "assignment_identification": "responseref",
            "return": false,
            "underlying_cancellation_details": {
              "cancellation_response_details": {
                "investigation_execution_status": "CNCL"
              }
            },
            "from": "BANCDEFFXXX",
            "to": "TRCKCHZZXXX",
            "originator": "BANCDEFF",
            "sender_acknowledgement_receipt": "2018-01-01T11:00:00.000Z",
            "last_update_time": "2019-08-30T11:00:00.000Z"
          },
          {
            "network_reference": "zad",
            "message_name_identification": "196",
            "business_service": "002",
            "tracker_event_type": "CTCR",
            "valid": true,
            "case_identification": "123",
            "assignment_identification": "responseref",
            "return": false,
            "underlying_cancellation_details": {
              "cancellation_response_details": {
                "investigation_execution_status": "CNCL"
              }
            },
            "from": "TRCKCHZZXXX",
            "to": "BANABEBBXXX",
            "originator": "TRCKCHZZ",
            "sender_acknowledgement_receipt": "2018-01-01T11:00:01.000Z",
            "last_update_time": "2019-08-30T11:00:05.000Z"
          }
        ]
      }
    ],
    "next": "cGFzcyB0aGlzIHZhbHVlIGluIHF1ZXJ5IHBhcmFtIGZvciBtb3JlIHZhbHVlcw=="
  }
}
```

> Scenario 2 - payment_scenario = "COVE"

response:

```json
{
  "changed_payment_transactions_response": {
    "payment_transaction": [
      {
        "uetr": "46ed4827-7b6f-4491-a06f-b548d5a7512d",
        "transaction_status": {
          "status": "ACCC"
        },
        "initiation_time": "2019-08-30T09:00:00.000Z",
        "completion_time": "2018-01-01T17:00:00.000Z",
        "last_update_time": "2018-01-01T17:00:00.000Z",
        "payment_event": [
          {
            "network_reference": "abc",
            "message_name_identification": "103",
            "business_service": "001",
            "tracker_event_type": "CTPT",
            "valid": true,
            "instruction_identification": "abc123",
            "transaction_status": {
              "status": "ACSP",
              "reason": "G000"
            },
            "return": false,
            "settlement_method": "COVE",
            "from": "BANABEBBXXX",
            "to": "BANDJPJTXXX",
            "serial_parties": {
              "debtor_agent": "BANABEBBXXX",
              "instructing_reimbursement_agent": "BANBUS33XXX",
              "creditor_agent": "BANDJPJTXXX"
            },
            "sender_acknowledgement_receipt": "2019-08-30T09:00:00.000Z",
            "received_date": "2019-08-30T09:00:00.000Z",
            "instructed_amount": {
              "currency": "USD",
              "amount": "1000"
            },
            "interbank_settlement_amount": {
              "currency": "USD",
              "amount": "1000"
            },
            "interbank_settlement_date": "2019-08-30T00:00:00.000Z",
            "charge_bearer": "DEBT",
            "last_update_time": "2019-08-30T09:00:00.000Z"
          },
          {
            "network_reference": "ghi",
            "message_name_identification": "202COV",
            "business_service": "001",
            "tracker_event_type": "COPT",
            "valid": true,
            "instruction_identification": "ghi789",
            "related_reference": "abc123",
            "transaction_status": {
              "status": "ACSP",
              "reason": "G000"
            },
            "return": false,
            "settlement_method": "CLRG",
            "clearing_system": "FDW",
            "from": "BANBUS33XXX",
            "to": "BANCUS33XXX",
            "cover_parties": {
              "debtor": "BANABEBBXXX",
              "debtor_agent": "BANBUS33XXX",
              "creditor_agent": "BANCUS33XXX",
              "creditor": "BANDJPJTXXX"
            },
            "sender_acknowledgement_receipt": "2019-08-30T09:10:00.000Z",
            "received_date": "2019-08-30T09:10:00.000Z",
            "interbank_settlement_amount": {
              "currency": "USD",
              "amount": "1000"
            },
            "interbank_settlement_date": "2019-08-30T00:00:00.000Z",
            "last_update_time": "2019-08-30T09:10:00.000Z"
          }
        ]
      }
    ],
    "next": "cGFzcyB0aGlzIHZhbHVlIGluIHF1ZXJ5IHBhcmFtIGZvciBtb3JlIHZhbHVlcw=="
  }
}
```
