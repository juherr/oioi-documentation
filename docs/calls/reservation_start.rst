.. highlight:: js

.. _calls-reservationstart-docs:

Reservation Start
=================

Request
-------

``"reservation-start"`` identifies the call as a reservation-start call.

Fields
~~~~~~

connector-id
   The EVSE ID that identifies the connector where the session should take place (string).

identifier
   array of objects containing EVCO ID and UID (optional)

   evco-id (string)
       The EVCO-ID of the Customer.
   rfid (string) (optional)
       RFID (UID) of the Customer.

Response
--------

Fields
~~~~~~

time
   Indicates the time in seconds from now till the reservation window closes (integer).

HTTP Status codes
~~~~~~~~~~~~~~~~~

200 OK
    The request was processed successfully.

Result codes
~~~~~~~~~~~~
0
    Success
181
    EVSE not found
330
    EVSE does not support reservation
190
    EVCO ID error
191
    EVCO ID unknown
194
    EVCO ID has another active reservation
323
    EVSE already reserved

Examples
--------

Request::

    {
        "reservation-start": {
            "connector-id": "DE*8PS*ETABCD*1",
            "identifier": [
                {
                  "evco-id": "DE*8PS*156456730*9",
                  "rfid": "12345678ABCDEF"
                },
                {
                  "evco-id": "DE*8PS*156454730*2"
                }
            ]
        }
    }

Successful Response::

    {
        "reservation-start": {
            "time": 300,
        },
        "result": {
            "code": 0,
            "message": "Success."
        }
    }

Error response::

    {
        "result": {
            "code": 194,
            "message": "EVCO ID has another active reservation."
        }
    }
