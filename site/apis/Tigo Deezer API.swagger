FORMAT: 1A
HOST: https://test.api.tigo.com/v2/tigo/mobile

# Tigo Deezer API
Provides methods for activation and verification of Deezer accounts associated to Tigo Customers.


#Group Revision History
|`Date`|`Author`|`Comments`|
|------|---------|------|
|Feb 20, 2015|ADS|Initial Release|
|Mar 18, 2015|ADS|Adjusted format of the blueprint.|
|||Response from GET method for Activation Status now returns information about the underlying music product|


#Group Summary
- Unless otherwise specified on this blueprint, common information is defined in the [Common API Guidelines][apistandards]
- All API invocations requires the calls to be authenticated. Please refer to [Authentication][clientCredentials]

[apistandards]:  <http://docs.opentigocommon.apiary.io/>  "API Standards"
[clientCredentials]:  <http://docs.tigooauth.apiary.io/>  "Authentication"
[commonParameters]:  <http://docs.opentigocommon.apiary.io/#commonparameters>  "Common Parameters"


#Group Deezer Activation Status 
Manage customer entitlement for Deezer Music

#### Applies to
`GT` `SV`

#### Response codes
`GT`

|`Code`|`Description`|`purchased`|`requiresActivation`|`HTTP Status`|`Comments`|
|------|-------------|-----------|--------------------|-------------|----------|
|1|Usuario tiene paquete de datos sin música ilimitada|false|false|200|
|2|Usuario no tiene paquete de datos ni de música ilimitada|false|false|200|
|3|Usuario tiene paquete de datos PREMIUM con música ilimitada pero no ha activado deezer|true|true|200|
|4|Usuario tiene paquete de datos PREMIUM con música ilimitada y ya activó deezer|true|false|200|
|5|Usuario tiene paquete de datos FREE con música ilimitada y no ha activado deezer|true|true|200|
|6|Usuario tiene paquete de datos FREE con música ilimitada y ya activó deezer|true|false|200|
|7|No tiene paquete de datos pero si tiene aun música ilimitada|false|false|200|
|8|El usuario tiene un paquete de música ilimitada, pero es de duración menor a otro que compro y por tanto se debe reaprovisionar su música|true|true|200|

`SV`

|`Code`|`Description`|`purchased`|`requiresActivation`|`HTTP Status`|`Comments`|
|------|-------------|-----------|--------------------|-------------|----------|
|2|Usuario no tiene paquete de datos ni de música ilimitada|false|false|200|
|3|Usuario tiene paquete de datos PREMIUM con música ilimitada pero no ha activado deezer|true|true|200|


#### Error codes
`GT`

|`Code`|`Message`|`Developer Message`|`HTTP Status`|
|------|---------|-------------------|-------------|
|1-COM|Servicio no disponible|No se puede establecer Comunicación con el Servicio Legado|503|
|2-COM|Servicio no disponible|No se puede establecer Comunicación con el esquema de Base de Datos|503|
|3-MSG|Error en el formato de mensaje|Error en el formato de mensaje|400|
|4-NEG|El número de teléfono no es Tigo|El número de teléfono no es Tigo|404|
|5-NEG|El número no es prepago o kit|El número no es prepago o kit|403|



##/{country}/deezer360/subscribers/{msisdn}/activationStatus
### Retrieve Activation Status [GET]
Verify the Deezer Activation Status for the specified MSISDN

The following properties are supported by this API:

####Response Body
- **requiresActivation**: (boolean, required) see table `Response Codes`
- **purchased**: (boolean, required) see table `Response Codes`
- **responseCode**: (string, required) see table `Response Codes`
- **responseMessage**: (string, required) see table `Response Codes`
- **productPackages**: (array of **productPackage**) contains zero or more music products the Customer is entitled to / subscribed to. [
                

Each **productPackage** contains the following attribute:
- **startDate**: (date, required, ISO 8601 format) date the product was granted to the customer.
- **endDate**: (date, required, ISO 8601 format) expiration date of the product. 
- **tigoProductSku**: (string, required) internal product SKU for Tigo. 
- **musicProductSku**: (string, optional) external music platform SKU related to the **tigoProductSKU** if available. 


+ Parameters
    + msisdn (required, string, `595983662854`) ... msisdn. See Common Parameters.
    + country (required, string, `GT`) ... country. See Common Parameters.

+ Response 200 (application/json)
    
    + Body
            
            {
                "requiresActivation": true,
                "purchased": true,
                "responseCode": "see table",
                "responseMessage": "see table"
            },
            productPackages [
                {
                    "startDate" : "2014-06-28T00:48:35.145",
                    "endDate" : "2015-01-12T09:48:35.145",
                    "tigoProductSku" : "ABC123",
                    "musicProductSku" : "123ABC"
                }
            ]
            
+ Response 400 (application/json)

    + Body
            
            {
                "statusCode": 400 (see value in Errorcodes table)
                "code": see Code in Errorcodes table,
                "message": "see Description in Errorcodes table",
                "developerMessage": "",
                "errorURL" : null
            }



### Set Activation Status [PUT]
Set the Deezer Activation Status for the specified MSISDN

The following properties are supported by this API:

####Request Body
- **activationStatus**: (boolean, required) sets Deezer activation status

#### Error codes
`GT`

|`Code`|`Message`|`Developer Message`|`HTTP Status`|
|------|---------|-------------------|-------------|
|1-COM|Servicio no disponible|No se puede establecer Comunicación con el Servicio Legado|503|
|2-COM|Servicio no disponible|No se puede establecer Comunicación con el esquema de Base de Datos|503|
|3-MSG|Error en el formato de mensaje|Error en el formato de mensaje|400|
|4-NEG|El número de teléfono no es Tigo|El número de teléfono no es Tigo|404|
|5-NEG|El número no es prepago o kit|El número no es prepago o kit|403|

+ Parameters
    + msisdn (required, string, `595983662854`) ... msisdn. See Common Parameters.
    + country (required, string, `GT`) ... country. See Common Parameters.
    
+ Request (application/json)

    + Headers

    + Body
            
            {
                "activationStatus": false
            }
    
+ Response 204

+ Response 500 (application/json) 

    + Body
            
            {
                "statusCode": see HTTP Status in Errorcodes table
                "code": see Code in Errorcodes table,
                "message": see Description in Errorcodes table,
                "developerMessage": "",
                "errorURL" : null
            }
            


+ Response 400 (application/json) 

    + Body
            
            {
                "statusCode": see HTTP Status in Errorcodes table
                "code": see Code in Errorcodes table,
                "message": see Description in Errorcodes table,
                "developerMessage": "",
                "errorURL" : null
            }
 
