FORMAT: 1A
HOST: http://prod.api.tigo.com/v1/tigo/mobile/co/balance_management

# OpenTigo Balance Management

Balance Management is a simple API that allows consumers to buy and transfer balance.

Requires `enriched token` to validate ownership of msisdn.

## TopUp [/{msisdn}/topup]

### TopUp Balance [POST]

Request new topup for msisdn. Provide amount, transaction id and institution id.

+ Request (application/json)

        {
            "amount": 501,
            "transactionId": 8003,
            "institutionId": 4073
        }

+ Response 200 (application/json)

        {
            "state": "OK",
            "amount": 501,
            "transactionCost": 0
        }

## Transfer [/{msisdn}/transfer]

### Transfer Balance [POST]

Request new transfer. Provide debit msisdn, transaction id and amount.

+ Request (application/json)

        {
            "debtMsisdn": "3016224691",
            "amount": 501,
            "transactionId": 8004
        }

+ Response 200 (application/json)

        {
            "state": "OK",
            "amount": 501,
            "transactionCost": 0
        }
