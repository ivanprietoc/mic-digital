FORMAT: 1A
HOST: https://test.api.tigo.com

# OpenTIGO - Utils
Collection of utility methods provided by OpenTIGO API. 

#Group Summary
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



# Group Utils
## User Activity [/v1/drupal/{country}/REST/useractivity]
### Add User Activity [POST]
Records a single occurence of an user activity.

The following properties are supported by this API:

####Request Body
- **product** (required, string): identifier of the product requesting the user activity log. Examples TigoAPPS, TigoSport, TOL, etc
- **action** (required, string): the action executed by the user. Examples User login !user
- **msisdn** (optional, string): mobile phone number without the country prefix. The number will be validated against the country specified as part of the URL with the `country` parameter. 
- **email** (optional, string): valid email address of the user. 
- **uid** (optional, string): user identifier. Examples 1234, h2au2nadu1sdf72, vlad.tepes 
- **uid_type** (optional, string): type that defines the `uid`. Examples TigoID, Drupal user ID, Tigo Sport UserID

####Response Body
- **status** (string): status of the invocation. OK or ERROR
- **response/result** (string): outcome of the execution. SUCCESSFUL indicates the correct ending of the execution. 
- **response/id_activity** (string): internal id of the transaction logged. 

####Caveats:

- The request body must be encoded in  `multipart/form-data`
- You **MUST** specify either one of `msisdn` or `email`, or you will get an error. 
- When specified, `msisdn` **MUST** be a valid number and will trigger the execution of a second validation proxy to verify 
that the number exists. 
- When `uid` parameter is present, `uid_type` is **mandatory** to fully identify the remote user and platform.  

+ Parameters
    + country (required, string, `co`) ... country.


+ Response 200 (application/xml)
        
    + Body
            
            <?xml version="1.0" encoding="utf-8"?>
            <result>
                <status>OK</status>
                <response>
                    <result>succesful</result>
                    <id_activity>498132</id_activity>
                </response>
            </result>






## SMS  [/v1/tigo/mobile/kannel/sendsms{?from,to,text}]
This API allows to send SMS messages to a single user.
### Send SMS Message [GET]

+ Parameters
    + from (required, string, `595983123123`) ... the number that will appear as the sender of the text message.
    + to (required, string, `5031231232`) ... the destination number for the messsage. 
    The API will determine the country based on the international prefix of the number, so it is 
    mandatory to fully qualify the number with the proper prefix.
    + text (required, string, `hello user!`) ... the text to be sent to the destination number. Avoid special characters
    that cannot be codified as part of the URL format. 


+ Request

    + Headers
    
            Authentication: Bearer {access token}

+ Response 202




