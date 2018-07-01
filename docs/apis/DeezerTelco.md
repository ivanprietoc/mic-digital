FORMAT: 1A

# Deezer Telco
Deezer Telco API proxy is a *Restful implementation bridge* to the deezer telco API.

It serves as a proxy which our oauth can secure, and hides the implementation details such as operator_id, token signing, secrets, etc.

Parameters and parameter names should conform to the original deezer documentation, only `operator_id`, `partner_id`, `token` and `action` should be ommited, as they will be automatically added to the API calls.
`country` parameter conforms to the [ISO 3166-1](http://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) two letter country code specification for our operations.

---

Accepted Parameters
-------------------
`subscriber_id` : Represents the `subscriber_id`, which can be either an email, MSISDN with country code, or UUID from the backend. (operator user UUID)
                    
                    this parameter can sometimes be a part of the **URL PATH** of the proxy.


`user_id` : This represents the deezer user identification (UUID) for the entitlement
                    
                    this parameter can sometimes be a part of the **URL PATH** of the proxy.


`password` : encripted password using the shared secret and shared algorithm.


`offer_code`: INT deezer offer code. As defined by deezer ( ex: free is 99.)


`start_date`: Start date of the current offer provisionned to the user.


`end_date`: End Date of the current offer provisionned to the user.


`linked` : linked status of the account. ( link between a deezer USER and a telco subscriber user).


`output`: output format desired. (json|php|xml)


---
Common result payload
---------------------
The result of the operation will contain the direct response from Deezer, this will contain these payload parameters:

`result_code`: result of the operation following : 1 Success, 0 undefined error , anything else error.

`result_label`: textual representation of the previous `result_code`.

# Group Deezer
Users related API calls implemented

## Users Collection [/deezer/telco/v1/{COUNTRY}/users/{user_id}]

### Get User information [GET]

+ Parameters
    + COUNTRY (required , string , `CO`) ... 2 letter ISO country code of the country
    + user_id (required , string , `123`) ... deezer user id of the entity

+ Response 200 (application/json)

        {
        "error": { },
        "results": {
            "operator_id": 13,
            "subscriber_id": "573017128864",
            "customer_id": "",
            "offer_code": "0",
            "start_date": "2013-05-08 18:47:00",
            "end_date": "2014-11-07 15:22:32",
            "linked": 1,
            "link_date": "2013-05-08 23:51:49",
            "user_id": "213069403",
            "active": 1,
            "insert_date": "2013-05-08 23:47:02",
            "update_date": "2014-11-07 15:22:32",
            "type": "user",
            "result_code": 1,
            "result_label": "Success"
            }
        }
        
### Created Deezer User [POST]
+ Parameters
    + COUNTRY (required , string , `CO`) ... 2 letter ISO country code of the country
    + user_id (required , string , `123`) ... deezer user id of the entity

+ Request (application/json)
        
        {
            "name":'test name',
            "password":'encripted password'
        }

+ Response 200 (application/json)
        
        {
            "error": { },
            "results": {
                "user_id": "18470425",
                "type": "user",
                "result_code": 1,
                "result_label": "Success"
            }
        }

 

## Subscribers Collection [/deezer/telco/v1/{country}/subscribers/{subscriber_id}?{url}=]
### Find user by MSISDN [GET]
+ Parameters
    + country (required , string , `CO`) ... 2 letter ISO country code of the country
    + subscriber_id (required , string , `123`) ... deezer subscriber id of the entity
    + url (optional, string , `false|true`) ... return instant login URL

+ Response 200 (application/json)

        {
        "error": { },
        "results": {
            "operator_id": 13,
            "subscriber_id": "573013383387",
            "customer_id": "",
            "offer_code": "139",
            "start_date": "2014-11-14 21:03:14",
            "end_date": "2014-11-29 21:03:14",
            "linked": 1,
            "link_date": "2014-11-14 21:03:14",
            "user_id": "362917483",
            "active": 1,
            "insert_date": "2014-10-27 17:08:56",
            "update_date": "2014-11-15 18:39:53",
            "type": "subscriber",
            "result_code": 1,
            "result_label": "Success"
            }
        }

### link Subscriber to user [PUT]
+ Parameters
    + country (required , string , `CO`) ... 2 letter ISO country code of the country
    + subscriber_id (required , string , `123`) ... deezer subscriber id of the entity
    
+ Request (application/json)
        
        {
        "user_id":"532550443",
        "linked":1
        }
    
+ Response 200 (application/json)
    

### Delete Subscriber [DELETE]
+ Parameters
    + country (required , string , `CO`) ... 2 letter ISO country code of the country
    + subscriber_id (required , string , `123`) ... deezer subscriber id of the entity
+ Request (application/json)
    
+ Response 200 (application/json)
        
        {
            "error": { },
            "results": {
                "operator_id": 13,
                "subscriber_id": "57123",
                "customer_id": "",
                "offer_code": "138",
                "start_date": "2012-09-27 08:26:35",
                "end_date": "2099-12-31 23:59:59",
                "linked": 0,
                "link_date": "0000-00-00 00:00:00",
                "active": 1,
                "insert_date": "2012-09-27 13:26:35",
                "update_date":"2014-11-12 15:51:55",
                "type": "subscriber",
                "result_code": 1,
                "result_label": "Success"
            }
        }