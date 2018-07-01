FORMAT: 1A
HOST: https://test.api.tigo.com/v2/tigo

# OpenTIGO - Billing
2nd Gen Tigo API.


# Group Billing
##Usage Details - Data [/mobile/{country}/billing/subscribers/{msisdn}/usage/data{?limit,offset,start_date,end_date}]
###Get Customer Data Usage [GET]

The following properties are supported by this API:

####Response Body
- **targetNumber**: destination number of the event
- **targetCompany**: destination company of the event
- **eventType**: type of event.
- **eventDescription**: description of the event type.
- **eventDateTime**: date and time of the event
- **eventDuration**: duration of the event in seconds. 

+ Parameters
    + country (required, string, `co`) ... country.
    + msisdn (required, string, `595981654321`) ... suscriber phone number
    + start_date (optional, date, `20150101`) ... show events only from this date. must be paired with `end_date` parameter.
    + end_date (optional, date, `20153001`) ... show events until this date. must be paired with `start_date` parameter. 
    + limit (optional, number, `5`) ... limit. See Pagination.
    + offset (optional, number, `10`) ... offset. See Pagination.


+ Response 200 (application/json)
        
    + Body
            
            {
                "dataUsage" : [
                    {
                        "targetNumber": "********4528",
                        "targetCompany": "TigoCO",
                        "eventType": "GPRS",
                        "eventDescription": "Navegacion",
                        "eventDateTime": "2015-01-23T10:38:16-05:00",
                        "eventDuration" : 1
                    },{
                        "targetNumber": "********5336",
                        "targetCompany": "TigoCO",
                        "eventType": "GPRS",
                        "eventDescription": "Navegacion",
                        "eventDateTime": "2015-01-23T10:38:16-05:00",
                        "eventDuration" : 1
                    }
                ]
            }


+ Response 400 (application/json)

    + Body
    
            {
                "error": 
                {
                    "statusCode": 404
                    "code": "1",
                    "message": "no data was found for the specified range",
                    "developerMessage": "not found exception: no data",
                    "errorURL" : null
                }
            }


##Usage Details - Text Message [/mobile/{country}/billing/subscribers/{msisdn}/usage/text_message{?limit,offset,start_date,end_date}]
###Get Customer SMS - Text Message Usage [GET]

The following properties are supported by this API:

####Response Body
- **targetNumber**: destination number of the event
- **targetCompany**: destination company of the event
- **eventType**: type of event.
- **eventDescription**: description of the event type.
- **eventDateTime**: date and time of the call
- **eventDuration**: duration of the event in seconds. equals to 1 for SMS event types

+ Parameters
    + country (required, string, `co`) ... country.
    + msisdn (required, string, `595981654321`) ... suscriber phone number
    + start_date (optional, date, `20150101`) ... show events only from this date. must be paired with `end_date` parameter.
    + end_date (optional, date, `20153001`) ... show events until this date. must be paired with `start_date` parameter. 
    + limit (optional, number, `5`) ... limit. See Pagination.
    + offset (optional, number, `10`) ... offset. See Pagination.


+ Response 200 (application/json)
        
    + Body
            
            {
                "smsUsage" : [
                    {
                        "targetNumber": "********4528",
                        "targetCompany": "TigoCO",
                        "eventType": "S",
                        "eventDescription": "SMS OFFNET",
                        "eventDateTime": "2015-01-23T10:38:16-05:00",
                        "eventDuration" : 1
                    },{
                        "targetNumber": "********5336",
                        "targetCompany": "TigoCO",
                        "eventType": "S",
                        "eventDescription": "SMS OFFNET",
                        "eventDateTime": "2015-01-23T10:38:16-05:00",
                        "eventDuration" : 1
                    }
                ]
            }


+ Response 400 (application/json)

    + Body
    
            {
                "error": 
                {
                    "statusCode": 404
                    "code": "1",
                    "message": "no data was found for the specified range",
                    "developerMessage": "not found exception: no data",
                    "errorURL" : null
                }
            }


##Usage Details - Voice [/mobile/{country}/billing/subscribers/{msisdn}/usage/voice{?limit,offset,start_date,end_date}]
###Get Customer VOICE Usage [GET]

The following properties are supported by this API:

####Response Body
- **targetNumber**: destination number of the event
- **targetCompany**: destination company of the event
- **eventType**: type of event.
- **eventDateTime**: date and time of the event
- **eventDuration**: duration of the event in seconds. 

+ Parameters
    + country (required, string, `co`) ... country.
    + msisdn (required, string, `595981654321`) ... suscriber phone number
    + start_date (optional, date, `20150101`) ... show events only from this date. must be paired with `end_date` parameter.
    + end_date (optional, date, `20153001`) ... show events until this date. must be paired with `start_date` parameter. 
    + limit (optional, number, `5`) ... limit. See Pagination.
    + offset (optional, number, `10`) ... offset. See Pagination.


+ Response 200 (application/json)
        
    + Body
            
            {
                "voiceUsage" : [
                    {
                        "targetNumber": "********4528"
                        "targetCompany": "TigoCO",
                        "eventType": "ONNET",
                        "eventDateTime": "2015-04-19T12:59:23Z",
                        "eventDuration": 16
                    },{
                        "targetNumber": "********5336"
                        "targetCompany": "TigoCO",
                        "eventType": "ONNET",
                        "eventDateTime": "2015-04-19T12:59:23Z",
                        "eventDuration": 125
                    }
                ]
            }

+ Response 400 (application/json)

    + Body
    
            {
                "error": 
                {
                    "statusCode": 404
                    "code": "1",
                    "message": "no data was found for the specified range",
                    "developerMessage": "not found exception: no data",
                    "errorURL" : null
                }
            }


##Invoice [/mobile/{country}/billing/subscribers/{msisdn}/invoices/{invoice_id}{?cycle,invoice_serial,invoice_type,service_type,date}]
###Get Customer Invoice by Invoice ID [GET]

Get a representation of the customer invoice. Valid formats are:
- **PDF**: Portable Data Format. Specify header `Accept` with `application/pdf`

+ Parameters
    + country (required, string, `co`) ... country.     
    + invoice_id (required, string, `123456`) ... the unique id of the invoice.
    + cycle (required, string, `D`) ... the billing cycle of the invoice.
    + invoice_serial (required, string, `J`) ... the invoice serial digit
    + service_type (required, string, `TELEFONIA`) ... type of service the invoice belongs to
    + date (required, date, `2014-10-31`) ... issue date of the invoice format YYYY-MM-DD
    + msisdn (required, string, `595981654321`) ... suscriber phone number

+ Request
    
    + Headers
    
            Accept: application/pdf

+ Response 200 (application/pdf)

    + Headers

+ Response 404
    
    + Body
            
            {
                "error": 
                {
                    "statusCode": 404
                    "code": "1",
                    "message": "no invoice was found with the provided criteria",
                    "developerMessage": "not found exception: no data",
                    "errorURL" : null
                }
            }


##Invoice Collection [/mobile/{country}/billing/subscribers/{msisdn}/invoices]
###Get Customer Mobile Invoices by MSISDN [GET]

The following properties are supported by this API:

####Response Body
- **type**: type of the invoice
- **serial**: invoice serial number
- **number**: invoice number
- **amount**: amount of the invoice
- **balance**: pending amount of the invoice
- **currency**: invoice currency
- **status**: current state of the invoice
- **cycle**: billing cycle of the line
- **expirationDate**: expiration date of the invoice. 
- **billingInfo** : invoice billing information. Contains the following attributes:
    - **cycle** : an internal cycle indicator. 
    - **startDate**: initial date of the billing cycle. 
    - **endDate**: end date of the billing cycle. 
- **contact**: information that is printed on the invoice. Contains the following attributes:
    - **name**: name on the invoice.
    - **address**: address on the invoice.
    - **phone**: phone on the invoice.
    - **document**: document number for the invoice.
    - **documentType**: type of the **document** attribute. 

+ Parameters
    + msisdn (required, string, `595983662854`) ... msisdn. 
    + country (required, string, `co`) ... country. 

+ Response 200 (application/json)

    + Body
        
            {
                "invoices" : [
                    {
                        "type": "CR",
                        "serial": "J",
                        "number": "1191091",
                        "amount": 39703.0,
                        "balance": 39703.0,
                        "currency": "PYG",
                        "status": "PC",
                        "expirationDate" : "2015-04-19",
                        "billingInfo": {
                            "cycle" : "D",
                            "startDate": "2015-03-05",
                            "endDate": "2015-04-04"
                        },
                        "contact" : {
                            "name" : "courage the cowardly dog",
                            "address" : "the middle of nowhere",
                            "phone" : "1-800-COURAGE",
                            "document" : 123456789,
                            "documentType" : "RUC"
                        }
                    },{
                        "type": "CR",
                        "serial": "F",
                        "number": "1827839",
                        "amount": 64884.0,
                        "balance": 0.0,
                        "currency": "PYG",
                        "status": "CA",
                        "cycle" : "D",
                        "expirationDate" : "2015-04-19",
                        "billingInfo": {
                            "cycle" : "D",
                            "startDate": "2015-03-05",
                            "endDate": "2015-04-04"
                        },
                        "contact" : {
                            "name" : "courage the cowardly dog",
                            "address" : "the middle of nowhere",
                            "phone" : "1-800-COURAGE"
                            "document" : 123456789,
                            "documentType" : "RUC"
                        }
                    }
                ]
            }

+ Response 404

    + Body
            
            {
                "statusCode": 404
                "code": "1",
                "message": "The specified number has no invoices",
                "developerMessage": "provided MSISDN has no invoices",
                "errorURL" : null        
            }
            
            
            
            
##Subscriber Debt [/mobile/{country}/billing/subscribers/{msisdn}/debtStatus]
###Get Customer Debt Status [GET]

The following properties are supported by this API:

####Response Body
- **expirationDate**: due date of the debt
- **pendingBalance**: pending amount of the debt (due balance)
- **lastBillAmount**: amount of the last emitted bill
- **contract**: contract number
- **lastInvoiceNumber**: id of the last emitted invoice
- **unpaidInvoicesCount**: count of unpaid invoices

+ Parameters
    + msisdn (required, string, `595983662854`) ... msisdn. 
    + country (required, string, `co`) ... country. 

+ Response 200 (application/json)

    + Attributes(object)
        + expirationDate: 2015-08-12 (required,string) - due date of the debt
        + pendingBalance: 50.00 (required,number) - amount in local currency of the debt (due balance)
        + lastBillAmount: 406.00 (optional,number) - amount of the last emitted bill
        + contract: 123456 (required,string) - contract number
        + lastInvoiceNumber: 123456 (required,string) - last emitted invoice id
        + unpaidInvoicesCount: 1 (optional,number) - count of emitted unpaid invoices.

+ Response 404

    + Body
            
            {
                "statusCode": 404
                "code": "1",
                "message": "The specified number has no invoices",
                "developerMessage": "provided MSISDN has no invoices",
                "errorURL" : null        
            }

