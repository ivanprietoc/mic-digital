FORMAT: 1A
HOST: https://qa.api.tigo.com/v1/tigo/mobile/eventAnalytics/

# Sim Swap Events
Sim swap events is an API for tigo self care application to track when the customers *swap out* a sim card on their phones.
In order to consume this API the application must have a valid Bearer token. If you need help in finding said token please visit the [oauth]('http://docs.oauthtoken.apiary.io/') page.

# Group SIMSwapEvents
SIM swap event related resources of the **SIMSwapEvents**

## SIMSWapEvents  [/SIMSwapEvents]
### Create a SIMSwap Event [POST]
Some parameters are optional as they are not available in all platforms, when available please provide them in order to have more complete data available for analysis.
SIMSwapEvent has the following parameters:

 **mcc** (mandatory,INT) represents the [Mobile Country Code](http://en.wikipedia.org/wiki/Mobile_country_code)
 
 **mnc** (Mandatory,INT) represents the [Mobile Network code](http://en.wikipedia.org/wiki/Mobile_country_code)
 
 **iso-country-code** (Mandatory,String) Two letter ISO country code as defined [here](http://en.wikipedia.org/wiki/ISO_3166-1_alpha-2)
 
 **imsi** (Optional, String) the SIM IMEI as available from android with [this](http://developer.android.com/reference/android/telephony/TelephonyManager.html#getDeviceId() ) API call
 
 **msisdn** (Optional, String) Represents the users MSISDN, available from header enrichment or logged in user information.
 
 **device-id** (Optional,String) Same Identifier used for Push notifications 
 
 **carrier-name** (Optional,String) Carrier name as available from [IOS](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Reference/CoreTelephonyFrameworkReference/_index.html#//apple_ref/occ/instp/CTCarrier/carrierName) and [android](http://developer.android.com/reference/android/telephony/TelephonyManager.html#getNetworkOperatorName())

+ Request (application/json)

        {
            "mcc":"001",
            "carrier-name":"Tigo" ,
            "mnc":"001", 
            "imsi":"12345", 
            "msisdn":"3013383387", 
            "device-id":"123",
            "iso-country-code":"CO"
        }

+ Response 201 (application/json)

        { "reponse": "ok" }


