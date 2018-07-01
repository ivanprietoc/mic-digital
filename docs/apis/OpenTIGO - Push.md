FORMAT: 1A
HOST: https://test.api.tigo.com/v2/tigo/push

# OpenTIGO - Push
Push Notifications API. 

#Group Summary
Provides a common way to send PUSH Notification to customers. 

- Synchronous operation. It waits for the message to be accepted on the backend before returning a valid response.
- Abstraction of more than one backend PUSH platform. The Backend Engine will be automatically selected based on the application specified. 
- More engines can be added. Migration of an Application to another engine is transparent to invoking clients. 
- Can send specific payloads to some types of engines if they support different payloads. These payloads can be created by the consuming client. 
- Support for Anti SPAM policies, configured at the proxy level. 
- Support user blacklisting, to prevent a customer to receive further messages. 


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

#Group Methods
## Push Notification [/apps/{appId}/users/{userId}/notifications{?userIdentifierType}]
### Send notification [POST]
Send a push notification to a customer.
The underlying platform for sending the notification will be automatically selected, as is dependant on the application.

### Common Errors
The following table depicts the errors this API can return. The `message` and `developerMessage` attributes of the 
body will contain the specific message condition.

|Error|Condition|Fix|
|------|---------|------|
|400|You didn't specified at least one of `message` or `payload` for the `application/json` request type |specify either `message` or `payload` or use the `x-www-form-urlencoded`version that requires only `message`| 
|403|The customer is not able to receive the message for being either blacklisted or outside the allowed configured valid timeframe|confirm if the customer is unwilling to receive messages. try to send the message on another time|
|403|The backend is not able to process a payload instead of a message.|use a message property and specify a null payload| 
|404|The `appId` was not found|the application is a fixed list and must be a previous existing one. make sure you have the proper application id|
|404|The `userId` was not found|the specified user id is invalid, non existent, or not valid to receive a notification for the specified application|

+ Parameters
    + appId (required, string, `tigoSportsPY`) ... name of the application. must be registered and configured to 
    receive push notifications.
    + userId (required, string, `595982555639`) ...  user identifier, not blacklisted and configured as belonging for the application  
    + userIdentifierType (optional, string, ``) ... determines the type of customer id specified on the URL. this is optional and the type will default to MSISDN
    This effectively redefine the `msisdn` parameter and specifies the identifier type used.  
    
+ Request (application/json)

    + Attributes(object)
        + message (required, string) - text message to send to the subscriber. 
        + expire (required, number, ) - (UNIX Timestamp) date time that defines push message expiration. Expiration feature depends on support of the underlying platform. If not supported, it will be gracefully ignored and message won't expire 
        + payload (optional, object) - an optional payload that overrides the content of `message` attribute and allows to send messages with attributes specific to the underlying Push platform.
        If the underlying platform does not accept payloads, an error will be raised (See error table).
        Payload must be a valid JSON object. 

    + Body
    
            {
                "message": "message to be sent to the customer",
                "expire": 1434727327,
                "payload": {
                    {}
                }
            }


+ Request (application/x-www-form-urlencoded)
   
    + Attributes(object)
        + message (string, required) - text message to send to the subscriber
        + expire (number, required) - Date time that defines push message expiration. Format is UNIX Time. Expiration feature depends on support of the underlying platform. If not supported, it will be gracefully ignored and message won't expire 

    + Headers

    + Body
        
            message=this+is+a+message+to+be+sent+to+customer&expire=1434727327

+ Response 204


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



## Blacklists [/apps/{app_id}/blacklisted_users{?userId,userIdentifierType}]
### Retrieve All Blacklisted Users [GET]
Get a list of blacklisted users for the application 


+ Parameters
    + app_id (required, string, `tigoSportsPY`) ... name of the application. must be registered and configured to 
    receive push notifications.
    + userId (optional, string, `595982555639`) ... user identifier for filtering  
    + userIdentifierType (optional, string, ``) ... user identifier type for filtering. 
    mandatory if `userId` is different than `MSISDN`


+ Response 200

    + Attributes(object)
        + application (string, required) - the application name
        + blacklist (array, required) - array containing blacklisted numbers
        + blacklist.userId (string, required) - the user id
        + blacklist.userIdentifier_type (string, required) - the user identifier type. 

    + Body
    
            {
                "application" : "tigo shop co",
                "blacklist" : [ 
                    {
                        "userId" : "595982555639",
                        "userIdentifierType" : "MSISDN"
                    },
                    {
                        "userId" : "courage@nowhere.com",
                        "userIdentifierType" : "email"
                    }
                ]
            }

### Blacklist User [POST /apps/{appId}/blacklisted_users/{userId}{?userIdentifierType}]
Add a User to the application's blacklist


+ Parameters
    + appId (required, string, `tigoSportsPY`) ... name of the application. must be registered and configured to 
    receive push notifications.
    + userId (required, string, `xxx@yyy.com`) ... user identifier, not blacklisted and configured as belonging for the application 
    + userIdentifierType (optional, string) ... determines the type of customer id specified on the URL. 
    This effectively redefine the `msisdn` parameter and specifies the identifier type used.  

+ Response 201

    + Headers
    
            Location: /apps/{appId}/blacklisted_users/{userId}{?userIdentifierType}
        

### Remove User from Blacklist [DELETE /apps/{appId}/blacklisted_users/{userId}{?userIdentifierType}]
Remove a User to the application's blacklist

+ Parameters
    + appId (required, string, `tigoSportsPY`) ... name of the application. must be registered and configured to 
    receive push notifications.
    + userId (required, string, `595982555639`) ... user identifier, not blacklisted and configured as belonging for the application 
    + userIdentifierType (optional, string, ``) ... determines the type of customer id specified on the URL. 
    This effectively redefine the `msisdn` parameter and specifies the identifier type used. Mandatory when the user identifier is not `MSISDN`

+ Response 200




# Group Customized Payloads
Depending on the backend, the `payload` attribute can contain one or more standard values that can be used
by the specific implementation to modify the message to be sent to the customer

The backend is dynamically selected based on the application that will be notified (using the `appId` attribute)



|Backend|Attribute|Type|Required|Comment|
|-------|---------|----|--------|-------|
|JUVO|message|string|true|overrides the default `message` attribute|
||product_category|string|true|identifies a product category inside the application|
||product_id|string|true|an specific product targeted for the message. application specific|
|APIGEE BAAS||||See documentation of custom payload notification at http://apigee.com/docs/app-services/content/creating-and-managing-notifications|



