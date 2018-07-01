FORMAT: 1A
HOST: https://test.api.tigo.com/

# OpenTIGO - Lend
Tigo Lend Platform API. 

#Group Summary

**See Also**
- Unless otherwise specified on this blueprint, common information is defined in the [Common API Guidelines][apistandards].
- All API invocations requires the calls to be authenticated. Please refer to [Authentication][clientCredentials].

[apistandards]:  <http://docs.opentigocommon.apiary.io>  "API Standards"
[clientCredentials]:  <http://docs.tigooauth.apiary.io/>  "Authentication"
[commonParameters]:  <http://docs.opentigocommon.apiary.io/#commonparameters>  "Common Parameters"
[pagination]:  <http://docs.opentigocommon.apiary.io/#pagination>  "Paginating Results"
[versioning]: <http://docs.opentigocommon.apiary.io/#versioning> "Resource Versioning"   
[rateLimit]: <http://docs.opentigocommon.apiary.io/#ratelimiting> "Rate Limited Resources"
[commonErrors]: <http://docs.opentigocommon.apiary.io/#commonerrors> "Common Errors"
[caching]: <http://docs.opentigocommon.apiary.io/#caching> "Caching"
[uit]: <http://docs.opentigocommon.apiary.io/#useridentifiertype> "User Identifier Type"


#Group Applies to
|Country|Comments|
|-------|--------|
|CO||
|GT||
|SV||

#Group Noncompliance 
- Loan Profile: 
    - url should  be _/subscriber_profiles/{msisdn}_
    - response body missing `currency` attribute
    - response body using non-normalized attribute _accountType_
    - response body _ debtAge_ datatype confusing?. casted to string currently
    - response body _ emergencyCallsAvailable_ confusing. if the value is in minutes, the attribute should be something like `emergencyCallMinutesLeft`
    - response body _emergencyDataAvailable_ must be accompanied of a measure unit, something like `emergencyDataUnit`
- Loans:
    - response body missing `currency` attribute
    - response body using non-normalized attribute _status_
    - response body using non-normalized attribute _productType_ 


#Group Methods
## Loan Profiles [/v2/tigo/mobile/{country}/zero_balance/subscribers/{msisdn}]
### Get Profile [GET]
Obtain Tigo Lend customer profile information. 

### Common Errors
The following table depicts the errors this API can return. The `message` and `developerMessage` attributes of the 
body will contain the specific message condition.

|Error|Condition|Fix|
|------|---------|------|
|404|the specified MSISDN was not found or the user does not have a profile| 


+ Parameters
    + country (required, string, `PY`) ... country code.
    + msisdn (required, string, `595982555639`) ...  msisdn number identifier. 

+ Request
    
    + Headers
        
            Accept: application/json
    
+ Response 200 (application/json)

    + Attributes(object)
        + creditLimit:  100 (number, required) - maximum amount (in local currency) this customer can have in debt at any given time. 
        + scoring: A (string, required) - local grade for scoring. Country Specific.
        + accountType: PREPAGO (string, required) - type of mobile account (Prepaid, Postpaid, Control, etc.)
        + totalDebt: 1000 (number, required) - total debt (in local currency), including fees at the time of the query.
        + debtAge: 2014-09-11 12:10:36 (string, optional) - date of the oldest pending debt.
        + creditAvailable: 10000 (number, optional) - amount (in local currency) left to request new loans.
        + emergencyCallsAvailable: 2 (number, optional) - number of emergency calls available left (in minutes).
        + emergencySmsAvailable: 4 (number, optional) - number of emergency SMS left.
        + emergencyDataAvailable: 1 (number, optional) - number of emergency data (in Mbytes) left.
        

+ Response 404 (application/json)

    + Body
    
            {
                "error": {
                    "statusCode": 404
                    "code": "1",
                    "message": "see errors table",
                    "developerMessage": "see errors table",
                    "errorURL": null
                }
            }



## Loans [/v2/tigo/mobile/{country}/zero_balance/subscribers/{msisdn}/loans]
### Get Loans [GET]
Allows to obtain historic information of loans of the customer. 


+ Parameters
    + country (required, string, `PY`) ... country code.
    + msisdn (required, string, `595982555639`) ...  msisdn number identifier. 

+ Response 200 (application/json)

    + Attributes(object)
        + loandID: 12323edefeef (string, optional) - unique identifier generated for the loan. 
        + issueDate: `2014-09-11 12:10:36` (string, required) - the timestamp when the loan was granted
        + loanAmount: 8.30 (number, required) - amount (in local currency) of the loan, excluding the Fee
        + fee: 1.0 (number,required) - lending fee (in local currency)
        + pendingAmount: 20.0 (number, required) - how much (in local currency) of this loan has not being paid to this date
        + totalPaid: 6.40 (number,required) - how much (in local currency) of this loan was already paid 
        + lastPaymentDate: `2014-09-11 12:10:36` (string, optional) - last date a payment was made to this loan
        + lastPaymentAmount: 3.20 (number, optional) - last payment (in local currency) made to this loan.
        + status: PAID (string, required) - discrete loan status as PAID, PENDING, OVERDUE.
        

### Add Loan [POST /v2/tigo/mobile/{country}/zero_balance/subscribers/{msisdn}/loans/{productId}]
Allows the client application to request a loan for the customer, including loans of type Balance, Emergency or Packages.

Applies to:

|Country|Comments|
|-------|--------|
|SV|Is the only country that provides a separate API for creating a Loan. For the other countries, see Fulfillment API / VAS Provisioning|



+ Parameters
    + country (required, string, `PY`) ... country code.
    + msisdn (required, string, `595982555639`) ...  msisdn number identifier. 
    + productId (required, string, `123` ) ... unique identifier of the product to loan. should match the value obtained by using /products endpoint. 

+ Response 200 (application/json)

    + Attributes(object)
        + resultMessage: `Se te han acreditado 2 SMS de emergencia para lo que necesites.         
        Se descontara de tu prox recarga $0.20. Marca *725 SEND y consulta tu saldo` (string, required) - human readable messsage for a successful request. 


## Products [/v2/tigo/mobile/{country}/zero_balance/subscribers/{msisdn}/products]
### Get Products [GET]
Allows a client application to obtain a list of available lending products for the customer. 


+ Parameters
    + country (required, string, `PY`) ... country code.
    + msisdn (required, string, `595982555639`) ...  msisdn number identifier. 

+ Response 200 (application/json)

    + Attributes(object)
        + productID: 123 (number, required) - unique identifier of the product. 
        + productName: `Prestamito de 60` (string, required) - human readable name of the offered product. 
        + productDescription: `Incluye 10 minutos a Tigo y 20 MB` (string, required) - verbose description of the offered product. 
        + price: 60 (number,required) - price (in local currency) of the product
        + lendingFee: 20.0 (number, required) - additional fee (in local currency)        
        + productType: `paquetigo` (string,required) - to differentiate if the offer is a Emergency Offer, Paquetigo or Saldo
        + productCategory: `combo` (string, required) - category of the product such as: Minutos, SMS, Internet, Combo, etc. Country Specific.
        + validityNumber: `1` (number, optional) - Duration of the Product (i.e. validity or expiration)
        + validityType: `DAY` (string, optional) - Duration Time Units of the Product, such as `DAY`, `WEEK`, `MONTH`, `HOUR`

    + Body

            [
              {
                "productID": 123,
                "productName": "Prestamito de 60",
                "productDescription": "Incluye 10 minutos a Tigo y 20 MB",
                "price": 60,
                "lendingFee": 20,
                "productType": "paquetigo",
                "productCategory": "combo"
              },
              {
                "productID": 456,
                "productName": "Prestamito de 90",
                "productDescription": "Incluye 20 minutos a Tigo y 80 MB",
                "price": 90,
                "lendingFee": 15,
                "productType": "paquetigo",
                "productCategory": "combo"
              }
            ]
