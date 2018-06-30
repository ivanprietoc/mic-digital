FORMAT: 1A
HOST: https://test.api.tigo.com

# Tigo OAuth 2.0 API
All APIs exposed by Tigo require Authentication using OAuth 2.0 Bearer tokens.
Any Application that has been granted access to any Tigo API must authenticate using **client credentials**
as described below.

# Group Pre-requisites
# Client Registration
Any Developer and App must request its own set of Client Credentials thru its Tigo Point of Contact.
For each Developer the following information is needed:

-   Full Name
-   Company Name
-   Email Address

For each Client Application the following information is required:

- Application Name
- Environment requesting access to: **test** and/or **prod**
- API Products it needs to access

It exchange the Developer will receive a **client_id** and **client_secret** for each environment.  
This two parameters are referred to as **client credentials**

# IMPORTANT Security considerations

## Server To Server API access ONLY
Since the only OAuth 2.0 **grant_type** supported for authenticating access to Tigo APIs is **client_credentials**, the Application must be able to store secrets safely.
So a developer must NEVER use this type of authentication from a Native Application or a Web Application than runs on the User-agent, since these are trivial to decompile or peak at the code to obtain the **client_secret**.
In other words, **client_credential** should be used in Server to Server comunications ONLY, where the Application Server is under controlled access.  
If Developer suspect the **client_secret** has been compromised, it must notify inmediately to its Tigo's point of contact to invalidate and generate a new **client_id** and **client_secret**

## Bearer Tokens safety
OAuth 2.0 Bearer Tokens only rely on the presence of a valid **access_token** to grant access to an API, this must be safely stored in a KeyChain or KeyStore on the Client Server.  
Also, they must never be transmitted over clear HTTP. Always use TLS/SSL to access Tigo APIs when using Bearer tokens.

# Group API endpoints
# OAuth token endpoint [/v2/oauth/token]

This API end point allows partner to get a valid `access_token`.  
A new `access_token` must be acquired *before* the Client Application can access any Tigo API.  
Also a new `access_token` must be acquired once a previous `access_token` has expired.  
The Time to live of each token is obtained in the `expires_in` attribute everytime a new token is issued.

## Obtain a token with Client Credentials [POST]

Create a new `access_token` using the developer's App client credentials.

### Parameters

+ **grant_type**: use string `client_credentials`
+ **scope** (optional): list of scopes, separated by a single space character, identifying the APIs & access-level required. Not currently in use, since Tigo is pre-assigning which API Products are accesible to each Developer/App.
+ **client_id**: Client Identifier assigned to the App by Tigo
+ **client_secret**: Client Secret assigned to the App by Tigo

### Paramter Encoding

+ **grant_type** and **scope** must be sent in the HTTP request body in url-encoded format, using header **Content-Type**:`x-www-form-urlencoded`
+ HTTP Basic authentication must be used as specified in [RFC2617](http://tools.ietf.org/html/rfc2617) where: 
    + **client_id** must be used as the *username*
    + **client_secret** must be used as the *password*
    + concatenate **client_id** and **client_secret** with a `:` as separator
    + encode the resulting string with *Base64* encoding
    + Add HTTP header: 
    
        `Authorization: Basic <base64 encoded string here>`
    

### Response Attributes
On succesful authentication, the response will be a JSON Object serialization containing the following attrbiutes:

-   **issued_at**: (string) containing the unix timestamp in milliseconds when the token was issued.  
    Example: `1405620313800`
- **application_name**: (string, uuid) the Client Application internal identifier.  
    Example: `d0734134-0eab-4a2a-91a7-8024c4b7a12e`
- **scope**: (string) granted scopes.  
    Example: `upselling fulfillment`
- **status**: (string) Approval status of the Clien Application.  
    It may be `approved`, `pending` or `rejected`
- **api_product_list**: (string) comma-delimited list of API Products to which this **access_token** grants access to.  
    Example: `[mobile-internet-up-selling-api, product-fulfillment-api, tigo_mobile_kannel_v1-Product]`
- **expires_in**: (string) Time in seconds when this **access_token** will expire, counting from the **issued_at**.  
    Example: `172799` (roughly 48 hours)
- **developer.email**: (string) Developer's email as registered by Tigo.  
    Example: `developer@example.com`
- **organization_id**: (string) Developer's company ID.  
    Example: `0`
- **token_type**: (string) Type of Token.  
    Only one supported is: `BearerToken`
- **client_id**: (string) Client App identifier as registered.  
    Example: `raowlsQ8q2kIcrIlva6HUomzG5kRUay0`
- **access_token**: (string) the access token.  
    Example: `nxa8WSX8T9GL3xnPJdFEy0YsJFwe`
- **organization_name**: (string) Tigo API organization where the API products are available.  
    Example: `millicom-nonprod`
- **refresh_token_expires_in**: (string) Time in seconds when the refresh token is going to expire. refresh_tokens are NOT supported for client_credentials, so ignore.
- **refresh_count**: (string) How many times this token has been refreshed. refresh_tokens are NOT supported for client_credentials, so ignore.

+ Request Valid (application/x-www-form-urlencoded)

    + Headers
    
            Authorization: Basic Base64({client_id}:{client_secret})
    
    + Body 
    
            grant_type=client_credentials&scope={scope}

+ Response 200 (application/json)

    + Body

            {
                "issued_at": "1405620313800"
                "application_name": "d0734134-0eab-4a2a-91a7-8024c4b7a12e"
                "scope": "upselling fulfillment"
                "status": "approved"
                "api_product_list": "[mobile-internet-up-selling-api, product-fulfillment-api, tigo_mobile_kannel_v1-Product]"
                "expires_in": "172799"
                "developer.email": "developer@example.com"
                "organization_id": "0"
                "token_type": "BearerToken"
                "client_id": "raowlsQ8q2kIcrIlva6HUomzG5kRUay0"
                "access_token": "nxa8WSX8T9GL3xnPJdFEy0YsJFwe"
                "organization_name": "millicom-nonprod"
                "refresh_token_expires_in": "0"
                "refresh_count": "0"
            }           

+ Request Invalid (application/x-www-form-urlencoded)

    + Headers
    
            Authorization: Basic Base64({client_id}:WRONG CLIENT_SECRET)
    
    + Body 
    
            grant_type=client_credentials&scope={scope}
    

+ Response 401 (application/json)

    + Body

            {
                "ErrorCode": "invalid_client"
                "Error": "Client credentials are invalid"
            }
