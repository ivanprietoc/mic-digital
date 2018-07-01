FORMAT: 1A
HOST: https://test.api.tigo.com/v1/tigo/mobile/msisdnAuth

# Tigo MSISDN Identification API
## Group Introduction
## Purpose
The purpose of these APIs is to enable Tigo and Partner's applications to 
securely identify the MSISDN of the Tigo User, 
when accesing the Application from a Mobile Device.

## MSISDN Identification
The MSISDN is the Mobile Phone number in International format 
of a particular Tigo customer.  
Applications running in the Mobile device or in a Mobile Web App 
might need to reliably know the MSISDN of the subscriber to access Tigo APIs.  
Even when the SIM Card and the Address Book in the Mobile Device 
might contain the user's phone number, this is just data configured 
by the end user and cannot be trusted.  
The Mobile Phone itself does NOT have access to its own phone number 
in a reliable way, since the main Network identifier between the Deivce 
and the Network is the IMSI.  
this is why the Mobile Network is the only one that knows the MSISDN 
of the user reliably.

## Methods for identifying the MSISDN
The API provides 2 ways to identify the Tigo user MSISDN:  

### Network Header Enrichment
When the user is connected to the Tigo Mobile Network, it is possible to identify the MSISDN without user intervention at Tigo Network.  
This is done in 2 steps:  

 1. The App calls **net_code** API endpoint using HTTP without TLS/SSL. If the user is on the Tigo Network the MSISDN will be extracted from the HTTP headers (which in turn, where added by the Network) and if verified, will return an OAuth 2.0 authorization `code` to the App.  
 2. The App calls the **token** endpoint API using HTTPS with TLS/SSL to exchange the authorization `code` for an `access_token`. The **token** API response will also include the user's verified `msisdn`.

### SMS One Time Passwords
Where the user is connected to any other Network (WiFi, other Mobile Operators, etc.), and it is not possible to ask Tigo Network to identify the MSISDN.  
This is done in 3 steps:  

 1. the App request the User to supply his/her claimed MSISDN.
 2. the App calls **sms_otp** API endpoint to generate a "One Time Password". This temporary password is sent to the claimed MSISDN via SMS but never revealed to the App.
 3. the App then requests the user to supply the "One Time Password" he should have received in a SMS (only if the claimed MSISDN is actually in his/her possesion).
 4. then, the App calls **sms_code** API endpoint to verify the user supplied "One Time Password". If the temporary passwords match, an OAuth 2.0 authorization `code` is returned to the App.
 5. finally, the App calls the **token** endpoint API using HTTPS with TLS/SSL to exchange the authorization `code` for a OAuth 2.0 `access_token`. The token will also include the user's verified `msisdn`.

## Availability
The following Tigo Markets support Network Header Enrichment:

- Bolivia
- Paraguay
- Guatemala
- El Salvador
- Colombia

## Client Application Requirements
All Applications (Clients) must be registered at Tigo API platform before 
attempting to use this API.  
The Client Application must provide the following information to Tigo:  

- **Application Name and Description**
- **Developer Name**
- **Developer Email** (main point of contact)
- **Application Redirect URI**: All API responses will redirect to this URI.
 - for Web Applications a normal URI can be supplied, like: `https://example.com/callback`
 - for Native Applications, a custom protocol schema URI may be used, like: `com.example.myapp://callback`

In exchange, Tigo must provide the Application Developer with the following parameters:

- `client_id`: this is a OAuth 2.0 client_id, and is considered safe to store on your Application.
- `client_secret`: this is a OAuth 2.0 client_secret and should be protected and kept secret.  

 > **WARNING**:
 > Avoid hard-coding the `client_secret` in Native Applications code.  
 > Store and use from the Server Side of your application, NOT from the User's Device.

- `redirect_uri`: the same Application Redirect URI supplied by the App Developer to Tigo.

# Group Obtain Authorization Code
## Network Authorization Code [/net_code{?client_id,response_type,scope,state,redirect_uri}]
Grants an authorization code to the requesting Client application ONLY if the MSISDN can be identified by the Tigo Network automatically.  

**Usage guidelines**:  

- Call this endpoint only using HTTP *without* TLS/SSL encryption, otherwise the network cannot detect the request.
- Call this endpoint only from the User's Device or the User-agent (Browser)...not from your backend server.  

 > **WARNING**: 
 > Verify that the user's Device is actually connected to a Mobile Network before calling this endpoint.  
 > The user might be connected via WiFi/Bluetooth using the Hotspot of another Tigo User! so the API may identify the Hotspot's user MSISDN not the end-user MSISDN.

### Obtain Authorization Code from Network Header Enrichment [GET]
+ Parameters
    + client_id (required, string, `cAGOBtZREWM2SRXmP3JQZ8uhBDJQzA7Y`) ... Application `client_id` that identifies the Client Application.
    + response_type (required, string, `code`) ... OAuth 2.0 `response_type` parameter. Always use `code` at this endpoint.
    + scope (optional, string, `balance`) ... Optional OAuth 2.0 `scope` parameter to specify the level of access requested. NOT used.
    + state (required, string, `msisdn_detected`) ... Recommended OAuth 2.0 `state` parameter. Supply a meaningful string to keep *state* in your application logic. this will be returned by the API to your registerd `redirect_uri` as supplied. Use to avoid known security vulnerabilities.
    + redirect_uri (required, string, `https://qa.api.tigo.com/v1/tigo/diagnostics/callback`) ... Your Application's redirection URI, URL encoded, where this API will callback and send the authorization code or an error. MUST match exactly as the one registered with Tigo API platform.

+ Request Valid

+ Response 302 (application/json)

    + Headers
    
            Cache-Control: no-store
            Pragma: no-cache
            Location: {redirect_uri}?code={code}&state={state}

    + Body

            {
                "code":"{code}"
            }


+ Request Error when Network could not validate MSISDN

+ Response 302  (application/json)

    + Headers
    
            Cache-Control: no-store
            Pragma: no-cache
            Location: {redirect_uri}?error=access_denied&error_description=Invalid%20MSISDN%20header%20from%20Tigo%20Network&state={state}

    + Body

            {
                "error":"access_denied",
                "error_desription":"Invalid MSISDN Headers in request",
                "state":"{state}"
            }
        
## SMS One Time Password [/sms_otp]
Generates a new One Time Password for a `msisdn` that will be send over SMS to a Tigo Customer.  

**Usage guidelines**:  

- Call this endpoint only using HTTPS *with* TLS/SSL encryption.
- You may Call this endpoint from the User's Device or the backend server.
- Everytime this API is called a new SMS One Time Password is generated and sent via SMS to Mobile Subscriber.

### Generate new One Time Password [POST]

**Input Parameters**  

- *client_id* (required, string, Example: `cAGOBtZREWM2SRXmP3JQZ8uhBDJQzA7Y`) Application `client_id` that identifies the Client Application.
- *msisdn* (required, string, Example: `50378832010`) The MSISDN number supplied by the end user and that we want to verify.
- *state* (required, string, Example: `sms_sent`) Recommended OAuth 2.0 `state` parameter. Supply a meaningful string to keep *state* in your application logic. this will be returned by the API to your registerd `redirect_uri` as supplied. Use to avoid known security vulnerabilities.

**Succesful response**  

The API will reply with HTTP Status code `302` on Success  
The `Location` header will contain the registered `redirect_uri` with the following additional parameters in the query string:  

- *result* will contain string `OK`, just to confirm that now you can ask the user for the SMS One Time Password.
- *msisdn* the `msisdn` supplied in the input parameters
- *state* the `state` supplied in the input parameters. Always Check on you Application that the `state` in the response was the same as the one in the request.

After receiving this response your Application should:

1. Instruct the User to check for a new SMS containing a one time password.
2. Ask the user to Input the one time password received by SMS.
3. Call the **sms_code** API to verify the one time password and get an Authorization `code` in return.

**Error Handling**

The API will reply with HTTP Status code `302`  
The `Location` header will contain the registered `redirect_uri` with the following additional parameters in the query string:  

- *error* will contain one of:
 - `server_error`
 - `invalid_request`
- *error_description* will contain a more verbose description of the error.
- *state* the `state` supplied in the input parameters. Always Check on you Application that the `state` in the response was the same as the one in the request.

the API may also reply with a HTTP Status code in the range `4XX` and `5XX` if an unexpected error ocurred.

+ Request Valid (application/x-www-form-urlencoded)

    + Body
    
            client_id={client_id}&msisdn={msisdn}&state={state}
        
+ Response 302 (application/json)

    + Headers
    
            Cache-Control: no-store
            Pragma: no-cache
            Location: {redirect_uri}?result=OK&msisdn={msisdn}&state={state}
    + Body
    
            {
                "result":"OK",
                "message":"SMS with temporary user credentials sent to your Mobile {msisdn}",
                "expires_in":300,
                "msisdn":"{msisdn}",
                "state":"{state}"
            }

## SMS Authorization Code [/sms_code{?client_id,msisdn,sms_password,response_type,scope,state,redirect_uri}]
This endpoint will return an OAuth 2.0 authorization `code` 
ONLY if the `msisdn` and `sms_password` supplied in the inputs 
matches the one time password sent to the Mobile user via SMS in 
a previous API call to [Send new One Time Password](#/sms_otp)  

> **NOTICE**
> that authorization `code` have a very brief lifetime (less than 5 minutes).  
> So you must exchange `code` for a `access_token` before it expires.

### Obtain Authorization Code from SMS One Time Password [GET]

+ Parameters
    + client_id (required, string, `cAGOBtZREWM2SRXmP3JQZ8uhBDJQzA7Y`) ... Application `client_id` that identifies the Client Application.
    + msisdn (required, string, `50378832010`) ... The MSISDN number supplied by the end user and that we want to verify.
    + sms_password (required, string, `123456`) ... The SMS password supplied by the end user that we want to verify against the one time password sent via SMS.
    + response_type (required, string, `code`) ... OAuth 2.0 `response_type` parameter. Always use `code` at this endpoint.
    + scope (optional, string, `balance`) ... Optional OAuth 2.0 `scope` parameter to specify the level of access requested. NOT used.
    + state (required, string, `sms_password_verified`) ... Recommended OAuth 2.0 `state` parameter. Supply a meaningful string to keep *state* in your application logic. this will be returned by the API to your registerd `redirect_uri` as supplied. Use to avoid known security vulnerabilities.
    + redirect_uri (required, string, `https://qa.api.tigo.com/v1/tigo/diagnostics/callback`) ... Your Application's redirection URI, URL encoded, where this API will callback and send the authorization code or an error. MUST match exactly as the one registered with Tigo API platform.

+ Request Valid

+ Response 302 (application/json)

    + Headers
    
            Cache-Control: no-store
            Pragma: no-cache
            Location: {redirect_uri}?code={code}&state={state}

    + Body

            {
                "code":"{code}"
            }


+ Request Error when Wrong MSISDN or sms_password

+ Response 302  (application/json)

    + Headers
    
            Cache-Control: no-store
            Pragma: no-cache
            Location: {redirect_uri}?error=access_denied&error_description=Wrong%20MSISDN%20or%20SMS%20password&state={state}

    + Body

            {
                "error":"access_denied",
                "error_desription":"Wrong MSISDN or SMS password",
                "state":"{state}"
            }
            
# Group Obtain token and MSISDN
After an authorization `code` has been obtained from either **net_code** or **sms_code** 
now you can exchange the `code` for a valid OAuth 2.0 `access_token` 
which will also provide the valid `msisdn` identity of the Mobile User.

## token [/token]
Obtain an `access_token` in exchange of a valid authorization `code`.
Along with the response you will also receive the validated `msisdn`.

### Obtain access_token [POST]
### Authentication
You must supply your `client_id` and `client_secret` credentials using HTTP Basic Authentication by including the HTTP Request Header:  

`Authorization: Basic Base64( {client_id}:{client_secret} )`  

### Input Paramters  
Sin this is a `POST` HTTP request, All input parameters must be sent in the HTTP request **body** encoded as `Content-Type: application/x-www-form-urlencoded`  

+ **grant_type** (required, string, example: `authorization_code`) ... Always use `authorization_code`
+ **redirect_uri** (required, string, example: `https://qa.api.tigo.com/v1/tigo/diagnostics/callback`) ... Your Application's redirection URI, URL encoded, where this API will callback and send the authorization code or an error. MUST match exactly as the one registered with Tigo API platform.
+ **code** (required, string, example: `4ksu1PhM`) ... the OAuth 2.0 authorization `code`

### Successful Response
The API will respond with a HTTP Status Code `200`
with a JSON serialized Object containing the following properties:

- *issued_at*: TimeStamp in milliseconds since epoch. example: `1408064062980`
- *msisdn_identification_method*: How the MSISDN was verified, any of:
    - `network header`
    - `sms code`
- *scope*: requested OAuth scopes
- *application_name*: Application GUUID registered in Apigee. example: `42eefff1-e43c-41a1-b505-02381043b3c8`
- *refresh_token_issued_at*: TimeStamp in milliseconds since epoch. ex: `1408064062980`
- *msisdn_verified_at*: TimeStamp in milliseconds since epoch. ex: `1408064037436`
- *msisdn_valid*: should always be `true`
- *status*: should always be `approved`
- *msisdn*: the actual MSISDN of the Tigo Customer. ex: `595981400007`
- *refresh_token_status*: should always be `approved`
- *api_product_list*: Array with all API products which this access_token has given permissions to access. ex: `[mobile-internet-up-selling-api, product-fulfillment-api, tigo_mobile_kannel_v1-Product]`
- *expires_in*: expiration time in seconds for the access_token. ex: `3599`
- *country*: ISO code for the country of the MSISDN. ex: `PY`
- *developer.email*: Developer Email. ex: `roberto.navas@millicom.com`
- *organization_id*: Apigee organization ID. ex: `0`
- *token_type*: type of access_token. expect `BearerToken`
- *refresh_token*: refresh token. ex: `x0xMDAa8hAe475RPH89AoldoRQ8XHu9Y`
- *client_id*: App client id. ex: `cAGOBtZREWM2SRXmP3JQZ8uhBDJQzA7Y`
- *access_token*: the OAuth token. ex: `licqaD7XTrUacjzISu4OqzjUTRkx`
- *organization_name*: Apigee organization name. ex: `millicom-nonprod`
- *refresh_token_expires_in*: expiration time in seconds for the refresh_token. ex: `3599`
- *refresh_count*: time the token has been refreshed. (not currently supported). ex: `0`


+ Request Valid (application/x-www-form-urlencoded)

    + Headers
    
            Authorization: Basic Base64("{client_id}:{client_secret}")

    + Body

            code={code}&grant_type=authorization_code&redirect_uri={redirect_uri}

+ Response 200 (application/json)

    + Body

            {
                "issued_at" : "1408064062980",
                "msisdn_identification_method" : "network header",
                "scope" : "{scope}",
                "application_name" : "42eefff1-e43c-41a1-b505-02381043b3c8",
                "refresh_token_issued_at" : "1408064062980",
                "msisdn_verified_at" : "1408064037436",
                "msisdn_valid" : "true",
                "status" : "approved",
                "msisdn" : "{msisdn}",
                "refresh_token_status" : "approved",
                "api_product_list" : "[mobile-internet-up-selling-api, product-fulfillment-api, tigo_mobile_kannel_v1-Product]",
                "expires_in" : "3599",
                "country" : "PY",
                "developer.email" : "roberto.navas@millicom.com",
                "organization_id" : "0",
                "token_type" : "BearerToken",
                "refresh_token" : "x0xMDAa8hAe475RPH89AoldoRQ8XHu9Y",
                "client_id" : "cAGOBtZREWM2SRXmP3JQZ8uhBDJQzA7Y",
                "access_token" : "licqaD7XTrUacjzISu4OqzjUTRkx",
                "organization_name" : "millicom-nonprod",
                "refresh_token_expires_in" : "3599",
                "refresh_count" : "0"
            }