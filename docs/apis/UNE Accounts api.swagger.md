FORMAT: 1A
HOST: http://127.0.0.1/

# UNE Accounts api

Une Accounts API is a simple API set that allows us to leverage the existing UNE ID accounts for Tigo ID.
This would facilitate the user onboarding to new regional products as they would be able to use their current credentials to log into Tigo ID enabled properties.

The idea is for Tigo ID to somewhat loosely sync with UNE id for credentials, having UNE ID as a fallabck master authenticator for the clients that are onboarded.

The flow can be seen [here](https://www.websequencediagrams.com/cgi-bin/cdraw?lz=VGl0bGUgVGlnbyBVbmUgUGlnZ3liYWNrClVzZXItPisAFQVJRDogL1BPU1QvQXV0aGVudGljYXRlLyhVc2VyIGNyZWRlbnRpYWxzKQoAKActPgAvCUNoZWNrIHVzZXIKYWx0IAAuBWlzIHZhbGlkCiAgIAB2BklELT4tVXNlcjogTG9nZ2VkIGluCmVsc2UAKwZub3QAJwtub3RlIHJpZ2h0IG9mADgIOgBIBUEAWAljb25zaWRlcmVkICIANgkiIGlmIGhlIGlzAE4FcHJvdmlzaW9ubmUAgQYGb24gdGhlIGxvY2FsIGRhdGFiYXNlIG9yAC0KACoJZWQsIHdhcyBpbXBvcnRlZCAAgUgFZnJvbSBVTkUgYW5kIGhpcyBwYXNzd29yZCBjdXJyZW50bHkgZG9lAHkGbWF0Y2gAgX8FKFVDOiBjaGFuZ2Ugb2YAKwpvbgBIBXN5c3RlbSkuAIIrBWVuZACBfQUAgi8OK1VuZTogY2hlY2tVc2VyKHVzZXIsAHUIKQCCZAUAgnYJAIJ3BQCBEAoAgk8OICAgAIQFBS0-AIJRCQCDOQVfZXhpc3RzIDoAgUoJX2luACkOAIN0CQCDYQU6IEkAGgYAhBYMAIE8BgCDTwkAGwcAWx4AUBcgAEImVgCBaAVVc2VyAIFPEACCLQVHZXQAhRgFIGluZm9ybWF0aW9uIChob21lX2lkLCBpZiBwb3NzaWJsZSBlbnRpdGxlbWVudHMAgkwGAIIiCi0AgiMKAGcKAIMABV9pbmZvACUKAIIaCgCGGApyZWF0AIRtCACGJAUAEhtidWlsZCByZXNwb25zAIN-BgCCZxQAhjsKAIQsBwplbmQK&s=rose)

All these APIs **MUST** be secured by SSL/TLS comminications (HTTPS).

## User authentication API

This api will allow Tigo ID to to use UNE id as an authenticator in the flow, Tigo ID would then import the user into its own user store for future use.

Four possible responses SHOULD be enabled on this API:
* 200 - credentials were valid
* 401 - Authentication failed | Account does not exist.
* 400 - Invalid Request ( parameter problems).
* 500 - Service Down ( overload, ORM problems).

These three responses would allow us to further customize the experience of the user performing the flow.

## Password update API

This API will enable Tigo ID to notify UNE id when a user that belongs to him updates his password on Tigo ID, so that they can update their records. 


## User account endpoint [/users/password]

### Validate credentials [POST]

+ Parameters
    + email (required, string, `abc@email.com`) ... Email that uniquely identified the client
    + password (required, string, `mypass12345`) ... Plaintext password that was input by the user.
    
+ Request (application/json)

        {
            "email":"{email}"
            "password": "{password}",
        }

+ Response 200 (application/json)

        {
            "status":"authorized",
            "response_code":200,
            "home_id":"CO-123321",
            "entitlements":{
                "tivo":"a",
                "other":"other"
            }
        }
        
+ Response 401 (application/json)

        {
            "status":"unauthorized",
            "response_code":401
        }

+ Response 400 (application/json)

        {
            "status":"bad_request",
            "response_code":400
        }

+ Response 500 (application/json)

        {
            "status":"service_down_with_the_flu",
            "response_code":500
        }

### Update password [PUT]

If a UNE imported user updates his password on UNE properties, for Tigo ID it would be trivial as the fallback mechanism would be activated.
Conversely, if a previously imported user updates his password on Tigo ID, his expectation would be that it is updated on UNE id.
For this, we SHOULD have this API so that we can notify UNE of the update. 

+ Parameters
    + email (required, string, `abc@email.com`) ... Email that uniquely identified the client
    + password (required, string, `mypass12345`) ... Plaintext password that was input by the user.

+ Request (application/json)

        {
            "email": "{email}",
            "password":"{password}"
        }

+ Response 202 (application/json)

    + Headers

    + Body

            {
               "status":"accepted"
            }

## password reset flow start [/users/password/reset]

### Password reset flow start [POST]

+ Parameters
    + email (required, string, `abc@email.com`) ... Email that uniquely identified the client
    
+ Request (application/json)

        {
            "email":"{email}"
        }

+ Response 200 (application/json)

        {
            "status":"sent",
            "response_code":200,
        }

+ Response 404 (application/json)

        {
            "status":"user_not_found",
            "response_code":404
        }
