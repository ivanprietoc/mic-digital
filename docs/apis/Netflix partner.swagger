FORMAT: 1A

# Netflix partner
An API to connect to the netflix partner API
---


Accepted Parameters
-------------------
`cid` : Represents the `customer_id`, which can be either an email, MSISDN with country code, or UUID from the backend. (operator user UUID)
                    
                    this parameter is agreed upoin with Tigo, with specific origin (Tigo ID) for home and mobile users

# Group Netflix
Netflix related calls.

## Netflix Subscribers Collection [/v1/netflix/subscriptions/{cid}/status]

### Get User information [GET]

+ Request 

    + Headers
    
        apikey :authorized-api-key

+ Parameters
    + cid (required , string , `CO-1234`) ... customer identifier
    

+ Response 200 (application/json)

        {
            "status": "ok",
            "promotions": [
                {
                    "promotionID": "f10cae9e-d39b-4f97-9b7b-d4da86b7980e"
                }
            ]
        }
        
+ Response 404 (application/json)

        {
            "status": "Not Found."
        }
        
## Netflix Token endpoint [/v1/netflix/subscriptions/{country}/token]

+ Parameters

    + country (required , string , `CO`) ... 2 letter ISO country code
    + type (required ,string, `Promo`) ... string promo
    + error_url (required,string,`http://www.dilbert.com`) ... URL to which we should send the user after an error in redemption.
    + channel (required,string,`Mobile`) ... channel on which the action is happening. mobile for now.
    + promo (required,string,`promoid`) ... promotion identifier. given by Netflix.
    + cid (required,string,`mic123`) ... agreed upon unique customer identifier
    
### Create Promotion token [POST]

+ Request (application/json)
    
    + Headers
        
        apikey: authorized-api-key
    
        {
            "type": "Promo",
            "error_url": "http://www.dilbert.com/",
            "channel": "Mobile",
            "promo": "promo_id",
            "cid": "mic123"
        }

+ Response 201(application/json)
    
        {
            "status": 201,
            "token": "prS8V6qP4wWTTKhY6q8U-KiuGso",
            "expires_in": "20160418T144145+0000",
            "description": "New token was created successfully",
            "redirect_uri": "https://www.sandbox.netflix.com/partner/home?ptoken=prS8V6qP4wWTTKhY6q8U-KiuGso"
        }

###