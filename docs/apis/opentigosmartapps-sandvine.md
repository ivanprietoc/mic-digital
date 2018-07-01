FORMAT: 1A
HOST: https://test.api.tigo.com/

# opentigosmartapps-sandvine

Momac/Sandvine allows Millicom/Tigo to adjust or query the ExchangeSubscription of TigoExchange users that are adminsitrated 
within the Momac/sandvice platform.

## Get Offers [/v1/tigo/mobile/sandvine/{countryCode}/{msisdn}/offers]

+ Parameters
    
    + msisdn: `50230063392` - msisdn with countryPrefix)
    + countryCode: `gt` - country code

### Get AvailableOffers [GET]

This service will  retun all services  which are available for the given MSISDN. The services are filtered with 
the following filters:

-Country
-Plan/SKU
-MSISDN blacklisting
-Current service subscription
-Trial subscription

+ Request

    + Headers

        Authorization Bearer xrOVV0UxSMnP4Zd6p0b2lCu2oX0O
        
+ Response 200 (application/json)

    + Attributes(getOffers)


## Sync Msidns [/v1/tigo/mobile/sandvine/{countryCode}/{msisdn}/sync]

+ Parameters
    
    + msisdn: `50230063392`- msisdn with countryPrefix
    + countryCode: `gt` -CountryCode
    

### Synchronize [POST]

This service will create/update users plan/bundle subscription status in Momac Database, so it is in sync
with the situaction in Tigos Database

 + Request

    + Headers
    
        Authorization Bearer xrOVV0UxSMnP4Zd6p0b2lCu2oX0O

        
 + Response 200 (application/json)

    + Attributes 
      
      + bundles:(array[bundles])


## Get Customer Status [/v1/tigo/mobile/sandvine/{countryCode}/{msisdn}/status{?startDate,endDate}]

+ Parameters
    
    + msisdn: `50230063392` msisdn with countryPrefix
    + countryCode: `gt`  
    + startDate: `2012-02-21`
    + endDate:`2012-03-10`

### QueryCustomerStatus [GET]

This service will return all customer subscriptions and their current status for the given MSISDN
between the given timeframe. (longest duration of any service is currently 1 year)

+ Request
    
    + Headers

        Authorization Bearer xrOVV0UxSMnP4Zd6p0b2lCu2oX0O
        
        
+ Response 200 (application/json)

  + Attributes (array[statusResponse])


## Cancel All Subscriptions [/v1/tigo/mobile/sandvine/{countryCode}/{msisdn}/subscriptions{?immediate}]



### Cancell All Subscriptions [DELETE]

This service is intended to terminate all running subscriptions for the given MSISDN. The subscriptions
can be stopeed immediately (no access) or scheduled (stopping all planned renewals)

Note: Is very important to understand when calling the CancelSubscriptionAPI, Momac only updates the Momac 
and the Service Provider systems. There are no call done to Tigo to remove any SKUS from the 
Tigo Subscription engine by Momac.

+ Request
    
    + Headers
        
        Authorization Bearer xrOVV0UxSMnP4Zd6p0b2lCu2oX0O
        
+ Response 204


## UnscheduleCancellation [/v1/tigo/mobile/sandvine/{countryCode}/{msisdn}/schedules]


### Unschedule Cancellation [DELETE]

This service is intended to cancel a previously (scheduled) cancelAllSubscriptions request.
It is not possible to terminate a CancelAllSubscriptions request that was already executed (e.g due to the immediate 
flag in CancellAllSubscriptions). It might happen that some subscriptions are already cancelled when
the UnscheduleCancellation request is issued. When this happen, the method will cancel
only the pending scheduled cancellations and return ok

+ Request
    
    + Headers
        
        Authorization Bearer xrOVV0UxSMnP4Zd6p0b2lCu2oX0O
        
+ Response 204


## ChangeNumber [/v1/tigo/mobile/sandvine/{countryCode}/{msisdn}/numbers]

### Change Number [PUT]

This service is intened to be used when a user's MSISDN has changed and the configured
services need to be migrate to his new MSISDN.

+ Parameters
    
    + msisdn: `50230063392` - msisdn with countryPrefix
    + countryCode: `gt` - CountryCode

+ Request(application/www-url-formencoded)

    + Headers
        
            Authorization Bearer xrOVV0UxSMnP4Zd6p0b2lCu2oX0O

toMsisdn=50230063391

+ Response 204


## Send Subscriptions [/v1/tigo/mobile/sandvine/{countryCode}/{msisdn}/subscriptions]


### Send Subscription[POST]

This service is intended to provision a subscriber from the Tigo Colombia CRM to MOMAC. This service should only be 
used by Colombia, does not have the getTigoExchangeSubscriptionInfo API call available in the SubscriptionEngineAPI


+ Parameters
    
    + msisdn: `50230063392` - msisdn with countryPrefix
    + countryCode: `gt` - CountryCode

+ Request (application/json)
    
    + Headers
        
         Authorization Bearer xrOVV0UxSMnP4Zd6p0b2lCu2oX0O
        

    + Attributes 
      + planType:POS
      + subscriptions:(array[subscriptions])


+ Response 204


## Send Push [/v1/tigo/mobile/sandvine/{countryCode}/{msisdn}/push]

### Send Push [POST]

A push message can be delivered to an individual enduser that has the SmartappsAndroid app
installed (and opened at least once) on his device via the Send Push Message API. This will be a API
similar to the existing, but using http post XML method allowing enriched push notifications to be sent.

+ Request(application/json)

    + Headers
        
         Authorization Bearer xrOVV0UxSMnP4Zd6p0b2lCu2oX0O

  + Attributes (pushSimple)


## Add Services [/v1/tigo/mobile/sandvine/{countryCode}/{msisdn}/services]

+ Parameters
    
    + msisdn: `50230063392` - msisdn with countryPrefix
    + countryCode: `gt` - CountryCode


### Activate Service[POST]

This service will activate the given service for the given MSISDN. 
If any of the following check fails, the API will respond with an error code and error message describing
the error:

-Does MSISDN exist
-User record not locked
-Is given service already activate
-MSISDN not blacklisted for the given service
-MSISDN has no had trial service activate before
-Is there a slot available
-Does available slot allow the selected service

+ Request (application/x-www-form-urlencoded)

    + Headers
        
         Authorization Bearer xrOVV0UxSMnP4Zd6p0b2lCu2oX0O

serviceCode=deezerrc


+ Response 200 (application/json)

   + Attributes(activateService)





# Data Structures

## statusResponse (object)

  + activatedOn:`2013-08-08 12:12:21` (string) - date of activation `2013-08-08 12:12:21`
  + activeUntil: `2013-09-08 12:12:21` (string) - maximum date of activation
  + creditsRemaining:2 (number) - left credits
  + deactivatedOn:`2013-09-08 12:12:21`  (string)    - 
  + isBasedOnCredits :"(string)
  + servicePlanId:1 (number) 1
  + serviceProviderId:2 (number) 2
  + serviceProdiverName:`deezer` (string) 


## activateService(object)

 + serviceName:Deezer (string)
 + serviceCode:deezer (string)
 + countryCode:GT (string)
 + startDatetime:`2016-01-15 08:10:02`
 + endDatetime:`2016-02--14 08:10:02`
 + prolong:no (string),
 + duration:30
 + associationUrl:https://acme
 + sandvineTransactionId:12321
 

## getOffers(object)

 + serviceName:Deezer (string)
 + serviceCode:deezer (string)
 + countryCode:HN (string)
 + duration:30
 + minimumDuration:2
 + isTrial:no
 + prolongable:1
 + description:Escucha mas de 30 millones de canciones
 + activationText:Escucha más de 30 millones de canciones 
 + confirmationText:a
 + disabledText:a
 + associationUrl:http://dezer.com
 + associationUrlAndroid:"
 + associationUrlIos:"
 + genre:musica,
 + serviceProviderName":Deezer
 + logoUrl:http://logo_dezzer.jpg
 

## bundles(object)

 + sku:005 (string)
 + action:no change (string)

## subscription(object)

 + code:010
 + status:Active
 + activeUntil:`2016-02-12 12:12:21`


## subscriptions(object)
 + code:010
 + status:Active
 + activeUntil:`2016-02-12 12:12:21`

  
## pushSimple(object)

 + message(object)
  + title:Prueba (string) Prueba
  + body : Mensaje (string) Push Mensaje

## button (object)
 
 + icon:uno.jpg
 + link:`https://1.tigo.com`
 + title:cosas

 
## pushComplex(object)

 + message(object)
  + title:Prueba title
  + body:Para el push
  + expandedStyle:BigText
  + expandedBody:Hola
  + buttons:(array[button])    