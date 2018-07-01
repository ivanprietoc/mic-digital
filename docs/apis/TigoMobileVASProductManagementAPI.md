FORMAT: 1A
HOST: https://qa.api.tigo.com/v1/tigo/mobile/gt/vas

# Tigo Mobile VAS Product Management API
Provides access to the Value Added Services (a.k.a. VAS) product catalog for Tigo Mobile customers, 
allowing them to acquire or subscribe a specific product.

# Authentication
1. Each Client application MUST register and request its client credentials from Tigo/Millicom.  
2. With your client credentials, an **access_token** needs to be obtained.
   Please see http://docs.tigooauth.apiary.io on how to obtain access tokens using your client credentials.
3. In each request, you need to present the **access_token** in the HTTP **Authorization** header like this:  
   `Authorization: Bearer <access_token goes here>`  
4. Beware of the **access_token** expiration, you should obtain a new one *before* it expires.

# Market availability
This API is avaialable in the following markets:
* **GT** Tigo Guatemala
* **CO** Tigo Colombia (Soon!)

# Group Product Catalog
These are the resources related to the particular Products Tigo Mobile Subscribers can acquire
or subscribe.

## Products Collection [/subscribers/{msisdn}/products{?category,planType,deviceVendor,deviceModel,deviceOperatingSystem}]
Returns the Collection of **products** that may be acquired or subscribed by 
a particular Tigo Mobile Subscriber identified by its `msisdn`
filtered by a specific product `category`

### Response HTTP Status

|HTTP Status|Meaning|
|-----------|-------|
|200 OK|Succesful query|
|404 Not Found|No product matches the requested inputs|
|4XX|Application level error, inspect JSON property `error` for details|
|5XX|Unexpected Error,  inspect JSON property `error` for details|

### Response Payload

Expect a JSON serialized object `Content-Type: application/json` with the following properties:

|JSON Property|Type|Contents|GT |CO |
|-------------|----|--------|---|---|
|action|string|always `get`|x|x|
|category|string|same `category` provided in the request|x|x|
|msisdn|string|same `msisdn` provided in the request|x|x|
|deviceModel|string|same `deviceModel` provided in the request or `*` if not specified|x|N/A|
|deviceOperatingSystem|string|same `deviceOperatingSystem` provided in the request or `*` if not specified|x|N/A|
|deviceVendor|string|same `deviceVendor` provided in the request or `*` if not specified|x|N/A|
|planType|string|same `planType` provided in the request or `*` if not specified|x|N/A|
|products|array|array of *products* or `null` if no products are elegible|x|x|

Each **product** has the following attributes:

|JSON Property|Type|Contents|GT |CO |
|-------------|----|--------|---|---|
|**packageId**|string|unique identifier of the product. ex: `18`, <code>face201&#124;pack40mb</code>|x|x|
|**name**|string|Name of the product. ex: `Paquetigo Roaming USA 199Q`|x|x|
|**description**|string|Verbose description of the product. ex: `Paquetigo Roaming USA 199Q`|x|x|
|**type**|string|Type of Product, has any of the following values:<ul><li>`PACKAGE`: is a package with a fixed validity (i.e. it expires after some time)</li><li>`SUBSCRIPTION`: is a product that has a recurrent benefit and recurrent charge (i.e. it is active until the customer unsubscribes)</li></ul>|x|x|
|**recurrencyType**|string|Indicates if there is a recurrent charge for the product, contains any of the values:<ul><li>`ONESHOT`</li><li>`RECURRENT`</li></ul>|x|x|
|**validityNumber**|string|Amount of time the product will be active after purchase, an integer, ex: `1`|x|x|
|**validityType**|string|units for the amount of time the product will be active after purchase, a localized string, ex: `Semana`|x|x|
|**purchaseDate**|ISO Date string|When the product was last purchased or subscribed by the customer. ex: null, `2014-09-04T10:32:00Z`|x| |
|**activationDate**|ISO date string|When the product was activated by the customer. ex: null, `2014-09-04T10:33:00Z`|x| |
|**expirationDate**|ISO date string|When the product will be expired from the customer. ex: null, `2014-09-04T10:32:00Z`|x| |
|**priority**|Number|Consumption priority??? ex: `0`|x| |
|**category**|string|Product Category, ex: `VOZ`, `SMS`, `INTERNET`|x|x|
|**subcategory**|string|Product Sub-Category, ex: `A Tigo`, `A otras redes`, `INTERNET`|x|x|
|**filter**|string|Filter???, ex: `TODOS`|x| |
|**cost**|Number|Activation Price, in local currency, ex: `175.00`|x|x|
|**status**|string|Current subscription status, any of the followings:<ul><li>`UNSUBSCRIBED`: Tigo Customer has not yet subscribed to this product.</li><li>`SUBSCRIBED`: Tigo Customer is already subscribed to this product.</li></ul>|x| |
|**consumptionPercentage**|Number|How much of the resources are already consumed, percentage number, ex: `0`|x|x|
|**price**|Number|Total Price to be paid by customer, in local currency, ex: `200.00`| |x|
|**keyword**|String|Keyword used to acquire the product over SMS, ex: `40MB`| |x|
|**shortCode**|String|Short Code used to acquire the product over SMS, ex: `face201`| |x|
|**price**|Number|Total Price to be paid by customer, in local currency, ex: `200.00`| |x|
|**loan**|JSON Object|If present, this means the Product is a Loan. It contains the following properties specific to the Loan:<ul><li>**category**: Lending Product category</li><li>**name**: Lending Product Name</li><li>**cost**: Base Price of the Lending product to be charged on next Top-Up</li><li>**fee**: Lending Fee to be charged on next Top-Up</li><li>**shortCode**</li><li>**keyword**</li><li>**description**</li></ul>| |x|


Products are grouped in several `category`. Classification is country specific, as follows:
### Tigo Guatemala `category` values:
- `1` INTERNET
- `2` VOZ
- `3` SMS
- `4` DIARIO
- `5` SEMANAL
- `6` MENSUAL
- `7` DIAS
- `8` HORA
- `9` HOY
- `10` BBI PREPAID
- `11` SUGERIDOS 1
- `12` SUGERIDOS 2
- `13` SUGERIDOS 3
- `14` COMBOS

### Tigo Colombia `category` values:
In Colombia, the `category` is just a Regular Expression Filter, for example:
- `.*` matches all products in *any* category
- `INTERNET` will match any product with `category` contains `INTERNET` for example: `INTERNET y MUSICA`
- `^LLAMADAS` will match any product with `category` starts with `LLAMADAS` for example: `LLAMADAS y SMS` but not `SMS y LLAMADAS`

## Query Available Products for Subscriber [GET]
Returns an `application/json` object with all input parameters in the response in addition to the **products** array.
Note, that **products** could be `null` in the cases where there are no elegible products for a particular **msisdn**, 
this could mean, that the **msisdn** is already subscribed to a product in the same `category`.

+ Parameters
    + msisdn (required, string, `50259050065`) ... Mobile number of tigo subscriber in international format.
    + category (required, integer, `1`) ... Filter products by Category, specific for each country.
        + Values for Tigo Guatemala:
            - `1` INTERNET
            - `2` VOZ
            - `3` SMS
            - `4` DIARIO
            - `5` SEMANAL
            - `6` MENSUAL
            - `7` DIAS
            - `8` HORA
            - `9` HOY
            - `10` BBI PREPAID
            - `11` SUGERIDOS 1
            - `12` SUGERIDOS 2
            - `13` SUGERIDOS 3
            - `14` COMBOS
        + Values for Tigo Colombia:
            - any valid regular expression. Example: `.*`
    + planType (optional, string, `PREPAGO`) ... Filter products by Plan type.
    + deviceVendor (optional, string, `Blackberry`) ... Filter products by Device Maker.
    + deviceModel (optional, string, `Bold`) ... Filter products by Device Model.
    + deviceOperatingSystem (optional, string, `BBOS10`) ... Filter products by Device Operating System.

+ Request

    + Headers
    
            Authorization: Bearer {access_token}

+ Response 200 (application/json)

        {
            "action": "get", 
            "category": "2", 
            "deviceModel": "*", 
            "deviceOperatingSystem": "*", 
            "deviceVendor": "*", 
            "msisdn": "50245891846", 
            "planType": "*", 
            "products": [
                {
                    "activationDate": null, 
                    "category": "VOZ", 
                    "consumptionPercentage": 0, 
                    "cost": 175, 
                    "description": "Paquetigo Roaming USA 199Q", 
                    "expirationDate": null, 
                    "filter": "TODOS", 
                    "name": "Paquetigo Roaming USA 199Q", 
                    "packageId": 18, 
                    "priority": 0, 
                    "purchaseDate": null, 
                    "recurrencyType": "ONESHOT", 
                    "status": "UNSUBSCRIBED", 
                    "subcategory": "VOZ", 
                    "type": "PACKAGE", 
                    "validityNumber": 1, 
                    "validityType": "Semana"
                }, 
                {
                    "activationDate": null, 
                    "category": "VOZ", 
                    "consumptionPercentage": 0, 
                    "cost": 125, 
                    "description": "Paquetigo Roaming USA 125Q", 
                    "expirationDate": null, 
                    "filter": "TODOS", 
                    "name": "Paquetigo Roaming USA 125Q", 
                    "packageId": 17, 
                    "priority": 0, 
                    "purchaseDate": null, 
                    "recurrencyType": "ONESHOT", 
                    "status": "UNSUBSCRIBED", 
                    "subcategory": "VOZ", 
                    "type": "PACKAGE", 
                    "validityNumber": 1, 
                    "validityType": "Semana"
                }, 
                {
                    "activationDate": null, 
                    "category": "VOZ", 
                    "consumptionPercentage": 0, 
                    "cost": 99, 
                    "description": "Paquetigo Roaming USA 99Q", 
                    "expirationDate": null, 
                    "filter": "TODOS", 
                    "name": "Paquetigo Roaming USA 99Q", 
                    "packageId": 16, 
                    "priority": 0, 
                    "purchaseDate": null, 
                    "recurrencyType": "ONESHOT", 
                    "status": "UNSUBSCRIBED", 
                    "subcategory": "VOZ", 
                    "type": "PACKAGE", 
                    "validityNumber": 1, 
                    "validityType": "Semana"
                }
            ]
        }

# Group Subscriber's VAS Products
## Subscriber VAS Products [/subscribers/{msisdn}/products/{packageId}]
Represents a specific Product, identified by `packageId` that can be acquired or is already subscribed by a particular 
Tigo Mobile subscriber identified by its `msisdn`.

+ Parameters
    
    + msisdn (required, string, `50259050065`) ... Mobile number of tigo subscriber in international format.
    + packageId (required, string, `2`) ... Product identifier to be acquired or unsubscribed.

## Subscribe a Product [POST]
Acquire or Subscribe a Product identified by `packageId` for Subscriber identified by `msisdn`

**On Success** reponse will be:
- HTTP Response Status code: `201` Created
- HTTP payload will be a `application/json` object with properties:
    - **action**: always `post`,
    - **msisdn**: requested `msisdn`
    - **productId**: requested `packageId`
    - **transactionId**: unique message ID generated at Apigee API layer
    - **correlationID**: timestamp
    - **responseCode**: 100 for succesful
    - **responseMessage**: end User message
 
**On Failure** reponse will be:
- HTTP Response Status code: `403` Forbidden 
- HTTP payload will be a `application/json` object with properties:
    - **error** which will contain:
        - **code**: expect `999`
        - **codeType**: expect `DES`
        - **message**: end User Reason why the product cannot be subscribed

+ Request (application/x-www-form-urlencoded)

    + Headers
    
            apikey: cAGOBtZREWM2SRXmP3JQZ8uhBDJQzA7Y

+ Response 201 (application/json)

        {
          "action" : "post",
          "msisdn" : "50259050065",
          "productId" : "2",
          "transactionId": "jahdf92hrh8wd1982",
          "correlationID": "1234",
          "responseCode" : "0",
          "responseMessage" : "Gracias"
        }

+ Response 403 (application/json)

        
        {
            "error": {
                "code": "999",
                "codeType": "DES",
                "message": "Tu numero no es valido para esta promocion, para ver promociones disponibles marca *123#"
            }
        }

## UnSubscribe a Product [DELETE]
Un-Subscribe a Product identified by `packageId` for Subscriber identified by `msisdn`

**On Success** reponse will be:
- HTTP Response Status code: `200` OK
- HTTP payload will be a `application/json` object with properties:
    - **action**: always `delete`,
    - **msisdn**: requested `msisdn`
    - **packageId**: requested `packageId`
    - **transactionId**: unique message ID generated at Apigee API layer
    - **correlationID**: timestamp
    - **responseCode**: 100 for succesful
    - **responseMessage**: end User message
 
**On Failure** reponse will be:
- HTTP Response Status code: `403` Forbidden 
- HTTP payload will be a `application/json` object with properties:
    - **error** which will contain:
        - **code**: expect `999`
        - **codeType**: expect `DES`
        - **message**: end User Reason why the product cannot be unsubscribed

+ Request (application/x-www-form-urlencoded)

    + Headers
    
            Authorization: Bearer {access_token}

+ Response 201 (application/json)

        {
          "action" : "delete",
          "msisdn" : "50259050065",
          "productId" : "2",
          "transactionId": "jahdf92hrh8wd1982",
          "correlationID": "442424242424",
          "responseCode" : "0",
          "responseMessage" : "Gracias"
        }

+ Response 403 (application/json)

        
        {
            "error": {
                "code": "999",
                "codeType": "DES",
                "message": "Tu numero no es valido para esta promocion, para ver promociones disponibles marca *123#"
            }
        }
