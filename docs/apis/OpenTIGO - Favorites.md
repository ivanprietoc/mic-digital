FORMAT: X-1A

HOST: https://test.api.tigo.com/v2/tigo/mobile


#OpenTIGO - Favorites
Favorite management API.


#Group Revision History
|`Date`|`Author`|`Comments`|
|------|---------|------|
|Mar 2, 2015|ADS|Initial Release|
|Mar 9, 2015|ADS|Added an identifier that determines if the favorite number obtained belongs to ATP or not|
|Mar 30, 2015|ADS|Added parameter favoritePlanCode to GET method for favoritePlans as the ATP variant requires it as input|

#Group Summary
- Unless otherwise specified on this blueprint, common information is defined in the [Common API Guidelines][apistandards].
- All API invocations requires the calls to be authenticated. Please refer to [Authentication][clientCredentials].


[apistandards]:  <http://docs.opentigocommon.apiary.io>  "API Standards"
[clientCredentials]:  <http://docs.tigooauth.apiary.io/>  "Authentication"
[commonParameters]:  <http://docs.tigoapigeneric.apiary.io/#commonparameters>  "Common Parameters"
[pagination]:  <http://docs.opentigocommon.apiary.io/#pagination>  "Paginating Results"
[versioning]: <http://docs.opentigocommon.apiary.io/#versioning> "Resource Versioning"   
[rateLimit]: <http://docs.opentigocommon.apiary.io/#ratelimiting> "Rate Limited Resources"
[commonErrors]: <http://docs.opentigocommon.apiary.io/#commonerrors> "Common Errors"
[caching]: <http://docs.opentigocommon.apiary.io/#caching> "Caching"


#Group Applies to
`CO`

#Group Favorites
APIs for working with favorite numbers

##/{country}/atpa/favorites/{msisdn}/favoritePlans{?favoriteClass,favoritePlanCode}
###GET



Retrieve the list of favorite plans for the specified user. 

####Specifics
|`Country`|`Comments`|
|------|---------|------|
|CO|Favorite plan list is a combination of methods **getFavoriteNumbersPlans** and **getCombos**|
|CO|favoriteClass ( _Enumeration_ ): DEFAULT,ATP|



####Response Body
- **links**: (array of **link**) contains internal representations of the root or related objects
- **favoritePlans**: (array of **favoritePlan**) contains one or more favorite numbers previously added to the plan.

Each **link** contains the following attributes:
- **rel**: the relationship of the retrieved object (the body) and the link. **self** indicates always that is the retrieved object.
- **href**: the url pointing to the parent, sibling or embedded resource. 

Each **favoritePlan** contains the following attributes:
- **favoritePlan**: the id of the favorite plan
- **name**: a short name of the favorite plan
- **description**: a description of the favorite plan. usually contains the plan benefits.
- **maxFavorites**: how many favorite entries are supported by this plan.
- **favoriteClass**: classifier of the favorite.Enumerated. 

+ Request 
    + Headers
    
            Authorization: Bearer 213123132132132


+ Parameters
    + country (required, string, `gt`) ... country code. see Common Parameters
    + msisdn (required, string, `50240600425`) ... msisdn. see Common Parameters
    + favoritePlan (required, string, `322`) ... favorite plan number.
    + favoriteClass (optional, string, `ATP`) ... classifier of the favorite. Enumerated. 
    + favoritePlanCode (string) ... define the plan to use as a filter for getting the plans. 
    mandatory when favoriteClass = `ATP`

+ Response 200 (application/json)

    + Body

            {
                "links" : [
                    {   
                        "rel": "self",
                        "href": "/{country}/favorites/{msisdn}/favoritePlans/"
                    }
                ],
                "favoritePlans" : [
                    {   "favoritePlan" : "group_basic4_31", 
                        "name": "group_basic4_31", 
                        "description": "36000 Seg  TDest (600 min)+ Mjes TDest Ilim+4.0GB+(2) Smart;con: (5)Fav Tigo ilim",
                        "maxFavorites" : 5,
                        "favoriteClass": "DEFAULT"
                    },
                    {   "favoritePlan" : "group_basic4_32", 
                        "name": "group_basic4_32", 
                        "description": "36000 Seg  TDest (600 min)+ Mjes TDest Ilim+4.0GB+(2) Smart;con: (3)Fav TDest con 30000 Seg (500 min)",
                        "maxFavorites" : 3,
                        "favoriteClass": "ATP" 
                    }
                ]
            }
       

##/{country}/atpa/favorites/{msisdn}/favoritePlans/{favoritePlan}/favoriteNumbers
###GET
Retrieve the list of favorite numbers added to the specified favorite plan number

####Response Body
- **links**: (array of **link**) contains internal representations of the root or related objects
- **favoriteNumbers**: (array of **favoriteNumber**) contains one or more favorite numbers previously added to the plan.

Each **link** contains the following attributes:
- **rel**: the relationship of the retrieved object (the body) and the link. **self** indicates always that is the retrieved object.
- **href**: the url pointing to the parent, sibling or embedded resource. 

Each **favoriteNumber** contains the following attributes:
- **favoriteNumber**: the favorite number
- **idType**: the type of the identified favorite number
- **status**: the status of the favorite number
- **favoriteClass**: classifier of the favorite.Enumerated. 

+ Request 
    + Headers
    
            Authorization: Bearer 213123132132132
+ Parameters
    + country (required, string, `gt`) ... country code. see Common Parameters
    + msisdn (required, string, `50240600425`) ... msisdn. see Common Parameters
    + favoritePlan (required, string, `322`) ... favorite plan number.     

+ Response 200 (application/json)

    + Body

            {
                "links" : [
                    {   
                        "rel": "self",
                        "href": "/v2/tigo/mobile/{country}/favorites/{msisdn}/favoritePlans/{favoritePlan}/favoriteNumbers"
                    },{
                        "rel": "parent",
                        "href": "/v2/tigo/mobile/{country}/favorites/{msisdn}/favoritePlans/{favoritePlan}"
                    
                    }
                ],
                "favoriteNumbers" : [
                    { "favoriteNumber" : "1234567890", "idType": "MSISDN", "status": "ACTIVATED","favoriteClass": "ATP"},
                    { "favoriteNumber" : "0987654321", "idType": "MSISDN", "status": "ACTIVATED","favoriteClass": "DEFAULT" }
                ]
            }
       


###POST
Add a number to the list of customer's favorites under the specified Favorite Plan.

####Request Body

- **favoriteNumber**: the number to add to the favorites list. string, required, example: 7864314567
- **favoriteClass**: classifier of the favorite.Enumerated. 

####Response Body
- **links**: (array of **link**) contains internal representations of the root or related objects

Each **link** contains the following attributes:
- **rel**: the relationship of the retrieved object (the body) and the link. **self** indicates always that is the retrieved object.
- **href**: the url pointing to the parent, sibling or embedded resource. 

            
            
+ Parameters
    + country (required, string, `PY`) ... country code. see Common Parameters
    + msisdn (required, string, `595981333567`) ... msisdn. see Common Parameters
    + favoritePlan (required, string, `group_basic4_29`) ... favorite plan number.     

+ Request


    + Headers
    
            Authorization: Bearer 213123132132132

    + Body
    
            {
                "favoriteNumber": "7864314567",
                "favoriteClass": "ATP" 
            }

+ Response 201 (application/json)
    + Headers
            
            ETag: 686897696a7c876b7e
         
    + Body

            {
                "links" : [
                    {   
                        "rel": "self",
                        "href": "/{country}/favorites/{msisdn}/favoritePlans/{favoritePlan}/favoriteNumbers/{favoriteNumber}"
                    }
                ]
            }
            
+ Response 400 (application/json)

    + Body

            "error": {
                "code": "<internal code>",
                "message": "Cannot add more favorite numbers to the plan",
                "developerMessage": "No more slots are available for the specified plan",
                "errorURL": null
            }
            

##/{country}/atpa/favorites/{msisdn}/favoritePlans/{favoritePlan}/favoriteNumbers/{favoriteNumber}
###DELETE
Delete an existing number from the list of customer's favorites under the specified Favorite Plan.

+ Request 
    + Headers
    
            Authorization: Bearer 213123132132132
            
+ Parameters
    + country (required, string, `gt`) ... country code. see Common Parameters
    + msisdn (required, string, `50240600425`) ... msisdn. see Common Parameters
    + favoritePlan (required, string, `322`) ... favorite plan code
    + favoriteNumber (required, string, `123456789`) ... favorite plan number

+ Response 204
