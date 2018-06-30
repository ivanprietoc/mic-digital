FORMAT: 1A
HOST: http://test.api.tigo.com/

# opentigosmartapps-tigoExchange

This service is exposed by the local Operation, to be used to update information about smartapps.



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
