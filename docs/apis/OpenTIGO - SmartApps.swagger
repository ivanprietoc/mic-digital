FORMAT: 1A
HOST: https://test.api.tigo.com

# OpenTIGO - SmartApps

# Deprecated API
# PLEASE !!! REFER TO:

# http://docs.opentigosmartappssandvine.apiary.io/
## This api will expose all the services provided by SANDVINE in RESTFULL-WAY 

---
---

# http://docs.opentigosmartappstigoexchange.apiary.io/#
## This api will expose all the funcionality from the Regional/ESB Server

#Group Summary
This API allows the consumer to work with Smart Apps platform.

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


#Group Error Codes Mapping

|Platform Code|HTTP Code|Explanation (Mapped to DeveloperMessage)|
|-------------|---------|----------------------------------------|
|0|200,204|No response usually needed.|
|100|404|Missing customer msisdn|
|101|404|Missing target msisdn for change msisdn|
|102|404|Unknown user|
|103|400|Missing start date|
|104|400|Missing end date|
|105|400|Invalid start date|
|106|400|Invalid end date|
|107|400|Invalid msisdn|
|110|500|SubscriptionEngine API Error|
|999|500|Generic Exception|

#Group REST MOMAC

This is recommended way to access/call services from MOMAC(sandvine)

##Offers [/v1/tigo/mobile/momac/rest/{countryCode}/{msisdn}/offers]
### Get Offers [GET]
+ Parameters
    + countryCode (required,string,`GT`)... countryCode
    + msisdn (required,string,`50230063392`)... msisdn

+ Request
      + Headers
        
            Authorization: Bearer 9wyLI80A9svAM4tRuJAahwSuairX
    
+ Response 200(application/json) 

  + Attributes(array[offers])

##Services [/v1/tigo/mobile/momac/rest/{countryCode}/{msisdn}/services]
### Activate Services [POST]

+ Parameters
    + countryCode (required,string,`GT`)... countryCode
    + msisdn (required,string,`50230063392`)... msisdn

+ Request(application/x-www-form-urlencoded)
        
    + Headers
    
            Authorization: Bearer 9wyLI80A9svAM4tRuJAahwSuairX        
        
    + Body
    
            serviceCode=deezer_cr

+ Response 200(application/json)

    + Attributes(activateServiceResponse)

##SyncMsisdn [/v1/tigo/mobile/momac/rest/{countryCode}/{msisdn}/sync]
### Sync Msisdn [GET]
+ Parameters
    + countryCode (required,string,`GT`)... countryCode
    + msisdn (required,string,`50230063392`)... msisdn

+ Request
      + Headers
        
            Authorization: Bearer 9wyLI80A9svAM4tRuJAahwSuairX
    
+ Response 200(application/json) 

  + Attributes(array[invocationResult])
  
#Group Methods
## Subscribers [/v2/tigo/mobile/{country}/smartapps/subscribers/{msisdn}]
### Change Subscriber [PUT]
Update a subscriber information.

The following attributes may be updated:

|Attribute|Consequence|
|---------|-----------|
|msisdn|update the main user identifier. After successfully  updating a customer msisdn, all invocations to the previous number will fail.|

+ Parameters
    + country (required, string, `PY`) ... country code.
    + msisdn (required, string, `595982555639`) ...  msisdn number identifier. 

+ Request (application/json)

    + Attributes(object)
        + msisdn: 595984123456 (required, string) - the new msisdn to update to. this will change the identity of the subscriber.  

+ Request (application/x-www-form-urlencoded)
   
    + Attributes(object)
        + msisdn: 595984123456 (required, string) - the new msisdn to update to. this will change the identity of the subscriber.  

    + Body
    
            msisdn=595984123456

+ Response 204
    
    + Headers
    
            Location: /subscribers/{newMsisdn}




## Subscriptions [/v2/tigo/mobile/{country}/smartapps/subscribers/{msisdn}/subscriptions{?immediate}]
### Cancel Subscriptions [DELETE]
Cancel all service subscriptions the customer currently has configured. 
The timing of the cancellation is determined by the parameter `immediate`: true means cancel all, immediately; false means wait until 
the service subscription is due and then cancel the subscription. 

+ Parameters
    + country (required, string, `PY`) ... country code.
    + msisdn (required, string, `595982555639`) ...  msisdn number identifier.
    + immediate (optional,boolean,`true`) ... indicates if the cancellation should happen immediately instead of waiting until the subscription due date. Defaults to `false`

+ Response 204

### Cancel subscription removal schedule [DELETE /v2/tigo/mobile/{country}/smartapps/subscribers/{msisdn}/pendingRemovals]
This call will stop any scheduled service subscription cancellation that was initiated by the Cancel Subscriptions API. 
It might happen that some subscriptions are already cancelled when the
request is issued. When this happens, the method will cancel only the
pending scheduled cancellations and return ok.
    
+ Parameters
    + country (required, string, `PY`) ... country code.
    + msisdn (required, string, `595982555639`) ...  msisdn number identifier. 
    
+ Response 204


### Get Services  [GET /v2/tigo/mobile/{country}/smartapps/subscribers/{msisdn}/services{?startDate,endDate}]
This service will return all customer subscriptions and their current status for the given MSISDN
between the given timeframe. Service subscriptions which are scheduled to start or scheduled to
stop outside of the timeframe will not be returned. In order to get all service subscriptions it is
advised to use an end date of at least 1 year in the future (as the longest duration of any service is
currently 1 year).
Since the SKU’s and services are not directly linked to each other, the API can only return the ‘last’
SKU (lowest in SKU family tree).


+ Parameters
    + country (required, string, `PY`) ... country code.
    + msisdn (required, string, `595982555639`) ...  msisdn number identifier.
    + startDate (required, string, `2015-07-01`) ... start date of the query.  
    + endDate (required, string, `2015-07-10`) ... end date of the query.


+ Response 200 (application/json)

    + Attributes
        + activatedOn (required,string) - date the subscription was started or is scheduled to start.
        + activeUntil (required,string) -  date the subscription will end / renew.
        + deactivatedOn (optional,string) - date the user or the system as deactivated this service (by using `immediate` flag)
        + serviceProviderId (required,number) - internal SKU of the service on the SmartApps platform.
        + serviceProviderName (required,string) - name of the service provider.
        + servicePlanId (optional,string) - SKU of the last bundle

    + Body

            "serviceSubscriptions" : [
                  {
                    "activatedOn" : "2013-08-08 12:12:21",
                    "activeUntil" : "2013-09-08 12:12:21",
                    "deactivatedOn" : "2013-08-31 19:07:48",
                    "serviceProviderId" : 341674,
                    "serviceProviderName" : "deezer"
                  },
                  {
                    "activatedOn" : "2011-08-08 12:12:21",
                    "activeUntil" : "2012-09-08 12:12:21",
                    "deactivatedOn" : "2014-08-31 19:07:48",
                    "serviceProviderId" : 123456,
                    "serviceProviderName" : "microsoft"
                  }
            ]

### Add  Service [POST /v2/tigo/mobile/{country}/smartapps/subscribers/{msisdn}/services]
Send a provision request to the Smartapps Platform, that will grant the customer 
one or more services with the provided details.

####Applies to:

|Country|Comments|
|-------|--------|
|CO| This service should only be used by Colombia, as Colombia does not have the
getTigoExchangeSubscriptionsInfo API call available in the SubscriptionEngine API.|


+ Parameters
    + country (required, string, `PY`) ... country code.
    + msisdn (required, string, `595982555639`) ...  msisdn number identifier.

+ Request (application/json)

    + Attributes(object)
        + planType: POS/PRE (required, string) - the type of plan.
        + productCode (required,string) - the product SKU
        + status : ACTIVE, CANCELED (required, string ) - the new status of the subscription.
        + activeUntilTS (required,string) - a valid date (UNIX timestamp) representing when to deactivate (CANCELED) or activate (ACTIVE) the subscription. 


    + Body

            
            {
               "planType": "POS/PRE",
                "subscriptions" : [
                    {
                        "productCode": null,
                        "status": "ACTIVE",
                        "activeUntilTS": null
                    },
                    {
                        "productCode": null,
                        "status": "CANCELED",
                        "activeUntilTS": null
                    }
                ]
            }


+ Response 204


### Synchronize Services [POST /v2/tigo/mobile/{country}/smartapps/subscribers/{msisdn}/syncServices]
**Disclaimer**: although this api tries to be agnostic of the backend platform for smart apps, this method is only
relevant to `MOMAC`


####Applies to:

|Platform|Comments|
|-------|--------|
|MOMAC|this method is only relevant to the MOMAC Smartapps platform provider.|


|Country|Comments|
|-------|--------|
|All, except Colombia(CO)|CO does not have the local method to query the status of the subscription|


#### Excerpt from MOMAC Documentation:
This service will create/update a user’s plan/bundle subscription status in Momac’s database so it is
in sync with the situation in Tigo’s database.
This service is available to all territories, except for Colombia, as Colombia does not have the
getTigoExchangeSubscriptionsInfo API call available in the SubscriptionEngine API.
Note the following order of operation when utilizing the SyncMSISDN service:

1. Tigo updates a user’s plan code.
2. Tigo removes SKUs from subscription engine.
3. Tigo ads new SKUs to subscription engine (optional).
4. Tigo calls the SyncMSISDN service.
5. Momac calls getClientBasicInfo (and stores the new plan code).
6. Momac calls getSubscriptionInfo:


- If SKUs are available:
    Momac updates records in Momac Engine accordingly (including removal of SKUs in Momac’s engine)

- If empty:
    Momac adds bundle SKUs per plan table using addSusbcriptionInfo (including
    removal of SKUs in Momac’s engine)
    NOTE: There are no calls done to Tigo to remove any SKUs from the Tigo subscription engine by
    Momac. Also, Momac never removes any bundled SKUs. The Tigo system is always leading.


+ Parameters
    + country (required, string, `PY`) ... country code.
    + msisdn (required, string, `595982555639`) ...  msisdn number identifier.
    
+ Response 200 (application/json)

    + Attributes
        + sku (required,string) - SKU of the plan/bundle
        + action: added, deleted or *no change* (required,string) -  action taken over the SKU

    + Body
        
             "bundles" : [
                      {
                            "sku" : "1234567890",
                            "action" : "added"
                      },
                      {
                            "sku" : "878654",
                            "action" : "deleted"
                      },{
                            "sku" : "9962",
                            "action" : "no change"
                        }
                ]




### Get Offers [GET /v2/tigo/mobile/{country}/smartapps/subscribers/{msisdn}/offers]

This service will return all srevices which are avaialable for the given MSISDN. 

The service will return trial services even though the premium service is already active. This is to indicate that the 
trial service is still available for the MSISDN. However, activating the trial service
while the premium service is active will fail.


+ Parameters
    + country (required, string, `PY`) ... country code.
    + msisdn (required, string, `595982555639`) ...  msisdn number identifier.
    
    
+ Response 200 (application/json)
  + Attributes(array[offers])


# Group Subscriptions TigoExchange


This endpoint will request directly to the country endpoint 


##  TigoExchange Collection [/v2/tigo/mobile/{country}/smartapps-em/subscribers/{msisdn}/subscriptions]


### Basic Info [GET /v2/tigo/mobile/{country}/smartapps/em/subscribers/{msisdn}/info]


####Applies to:

|Country|Comments|
|-------|--------|
|GT |require info from TigoExchangeManagement.|


Obtain info from wsdl:


+ Parameters
    + country (required, string, `gt`) ... country code.
    + msisdn (required, string, `50230063392`) ...  msisdn number identifier.

+ Request 

    + Headers
     
            Authorization: Bearer WtGWqlyx1mhibnoTDnGiif0AgwGK


+ Response 200 (application/json)

    + Attributes(infoResponse)


### GET Subscription TigoExchange [GET /v2/tigo/mobile/{country}/smartapps/em/subscribers/{msisdn}/subscriptions]

Obtain Subscriptions info from wsdl https://services.tigo.com.gt/ExchangeManagement/TigoExchangeManagement/V1

####Applies to:

|Country|Comments|
|-------|--------|
|GT |require info from TigoExchangeManagement.|


+ Parameters
    + country (required, string, `gt`) ... country code.
    + msisdn (required, string, `50230063392`) ...  msisdn number identifier.


+ Request 

    + Headers
     
            Authorization: Bearer WtGWqlyx1mhibnoTDnGiif0AgwGK


+ Response 200 (application/json)

    + Attributes
        + subscriptions (array[subscriptions])




### Post Subscription TigoExchange [POST /v2/tigo/mobile/{country}/smartapps/em/subscribers/{msisdn}/subscriptions/{productId}]

+ Parameters
    + country (required, string, `gt`) ... country code.
    + msisdn (required, string, `50230063392`) ...  msisdn number identifier.
    + productId (required,string,`010`)... product Code

+ Request 

    + Headers
     
            Authorization: Bearer WtGWqlyx1mhibnoTDnGiif0AgwGK
        
+ Response 204 


### Delete Subscription TigoExchange [DELETE /v2/tigo/mobile/{country}/smartapps/em/subscribers/{msisdn}/subscriptions/{productId}]



+ Parameters
    + country (required, string, `gt`) ... country code.
    + msisdn (required, string, `50230063392`) ...  msisdn number identifier.
    + productId (required,string,`010`)... product Code

+ Request 

    + Headers
     
            Authorization: Bearer WtGWqlyx1mhibnoTDnGiif0AgwGK
            
+ Response 204 


# Data Structures

## subscriptions (object)

+ status:ACTIVE (string)- "Status Product"
+ type: PLAN_BUNDLED (string)- "PLAN_BUNDLED"
+ code: 005 - "005"

## offers (object)

 + serviceName: Deezer,
 + serviceCode: deezer,
 + countryCode: GT,
 + duration: 30,
 + minimumDuration: "",
 + isTrial: "",
 + prolongable: 1,
 + description: Escucha m&aacute;s de 30 Millones de canciones en tu smartphone Tigo.,
 + activationText: Escucha m&aacute;s 30 millones de canciones en tu smartphone Tigo.,
 + confirmationText: "",
 + disabledText: El Servicio de Deezer no est&aacute; disponible en tu plan actual, para activarlo comun&iacute;cate con nuestro equipo de servicio al cliente a la l&iacute;nea *611,
 + associationUrl: http://www.tigomusic.gt/deezer/inicio,
 + associationUrlAndroid: "",
 + associationUrlIos: "",
 + genre: M&uacute;sica,
 + serviceProviderName: Deezer,
 + logoUrl: http://smart.tigo.com.gt/resources/logo_deezer.png

## activateServiceResponse(object)

+ serviceName: Bookmate,
+ serviceCode: bookmate,
+ countryCode: GT,
+ startDatetime: `2016-03-23 13:42:40`,
+ endDatetime: `2016-04-23 12:42:40`,
+ prolong: yes,
+ duration: month,
+ associationUrl: `http://bm.gg/tigo`,
+ sandvineTransactionId: 36937

## productsInfo (object)

+ planCode: 103,
+ planType: POS

## infoResponse (object)

+ status:ACTIVE(string) - "Status Product"
+ products:(array[productsInfo])
