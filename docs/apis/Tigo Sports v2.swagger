FORMAT: 1A
HOST: https://test.api.tigo.com/v2/tigo/tigosports

# Tigo Sports v2
To enable premium access to the Live Matchcast inside the TIGOSPORTS App,
needs to be provisioned by each Tigo country when the Offer is activated.
To enable this, each Tigo Operation will implement a client to a provisioning API (Web Service) 
that will be exposed by Tigo regional team in Apigee Gateway (Tigo Cloud infrastructure).
In this page will keep track of all relevant documentation related to the user provisioning API.

---------------------------
For **HOME USER**

Entitlement is requested by the API 

Api:

-`toolbox_auth_v1`

See documentation [toolbox][toolbox]


---------------------------


This API use the **LOG SERVER**

- Documentationa about using this api could be found in [Common API Guidelines][apistandards].

[apistandards]:  <http://docs.opentigocommon.apiary.io>  "API Standards"
[toolbox]:<https://app.apiary.io/toolboxautv1> "Toolbox"

# Group Susbscriber

Obtain info from a subscriber Id

## Subscribers Collection [/{countryCode}/{businessUnit}/subscriber/{subscriberId}]

+ Parameters
    + countryCode (string)- PY
    + businessUnit (string) -movil
    + subscriberId (string) -5958123132

### Subscriber [GET]


####Response Body

- **status** : OK (string) - Response Status
- **error**  (string, nullable, required) - Value of this field can be either unset or of the `string` type
- **result**:(object)
 - **subscriberId**: PYMOVIL.595982997707 (string) - Identifier IP subscribers 
 - **businessUnit**: movil (string) - Could be `home|other|movil`
 - **country**: py (string) - Code representing country
 - **channel**: USSD, (string) - Local sales channel Could be : `USSD,TIGOSHOP,SMARTAPPS`  
 - **customerId**: 595982997707 (string) - For Country purpose Ex:crm-id, ()
 - **insertDate**: `2015\-01\-09 18:06:21` - Register Date
 - **updateDate**: `2015\-01\-30 00:36:24` - Update date
 - **userId** - UUID unique from backend
 - **URNs**:(array) 
        - **resource_id**:Identifier (string)- "urn:tve:tigosports"
        - **access**: true (boolean)- true
        - **startDate**: `2015-08-30 00:36:24` UTC 
        - **endDate**: `2015-09-30 00:36:24`  UTC
- **type**:subsriberId (string)

+ Request 
    + Headers
    
            Authorization: Bearer 213123132132132

+ Response 200 (application/json)

    + Attributes(subscriberWithURN)

  

# Group Susbscriber Carrier


## Carrier Subscribers Collection [/carrier/subscriber/{subscriberId}{?operatorId}]

The following paths, will modify or retrieve the  current state of the subscriberId.


+ Parameters

    + subscriberId: 5958123132  (string) -5958123132

### Get Subscriber [GET]
Obtain subscribers

+ Parameters

    + operatorId: NMSKY3432423432NMNB4324  (string) -
    
+ Response 200 (application/json)

    + Attributes(subscriberWithURN)


### Add Subscriber [POST] 
Create and store new subscriberId.

Use Case
----
If user doesn't exist, is mandtory the field `urn` with the specific schema.

If user already exists,subscriber  will be **updated** with the content of the request.
----
    
+ Request (application/json)

    + Attributes(subscriberPost)
 
+ Response 200 (application/json)

    + Attributes(subscriberWithURN)

### Remove Subscriber [DELETE]

Remove existing subscriberId.

+ Request (application/json)

    + Attributes(object)
        + operatorId:NMSKY3432423432NMNB4324 (required,string)
    


+ Response 200 (application/json)

    + Attributes
    
         + status: OK (string) - Response Status
         + error (string, nullable, required) - Value of this field can be either unset or of the `string` type
         + result (object)
           + message: deactivated (string)-
           + subscriberId: 595982997707 (string)
     
### Update Subscriber [PUT]

Update field from subscriberId


+ Request (x-www-form-urlencoded)

    + Attributes
        + newSubscriberId:595981654321

   

+ Response 200 (application/json)

    + Attributes(subscriberWithURN)
      


## Entitlements [/carrier/subscriber/{subscriberId}/entitlements{?operatorId}]



### Retrieve entitlements [GET] 

Retrieve the array of Urns associated with the subscriberId.


PATH DOES NOT APPLY TO

---

BussinesUnit: `HOME`
COUNTRY: `PY`

---


####ResponseBody####
- **Urns**(array)
    - **resource**_id:Identifier (String) - "urn:tve:tigosports"
    - **access**: true (boolean)- true
    - **startDate**: `2015-08-30 00:36:24`
    - **endDate**: `2015-09-30 00:36:24`

+ Parameters

    + subscriberId: 5958123132  (string) -5958123132
    + operatorId: NMSKY3432423432NMNB4324



+ Response 200 (application/json)

    + Attributes 
     + urn:(array[urns])



### Update entitlements [PUT]

Modify the array of entitlements will add `urn` for the current collection.

`Urn` property is **required** For empty entitlements `urn:[]`

 `OperatorId` should be included in body payload


PATH DOES NOT APPLY TO

---

BussinesUnit: `HOME`
COUNTRY: `PY`

---

+ Parameters

    + subscriberId: 5958123132  (string) -5958123132

 
+ Request(application/json)
    + Attributes 
        + operatorId:CL6AWg8YJaDUKTyvtDAZAlmQTNkJmoEZ (string,required),
        + urn:(array[urns],required)

+ Response 200 (application/json)
   
    + Attributes(subscriberWithURN)

  


## Entitlement [/carrier/subscriber/{subscriberId}/entitlements/{urn}{?operatorId}]


    
### Retrieve entitlement [GET]

Retrieve entitlement
+ Parameters

    + subscriberId: 5958123132  (string) -5958123132
    + urn: tve:tigosports
    + operatorId: NMSKY3432423432NMNB4324 (required)

    
Retrieve the request urn Object

+ Response 200 (application/json)

    + Attributes (urns)

### Delete entitlement [DELETE]


Remove specific entitlement

+ Parameters

    + subscriberId: 5958123132  (string) -5958123132
    + urn: urn:tve:tigosports


+ Request(application/json)
    + Attributes 
      + operatorId:An7VxwzVYPldilMUdT8Woq1rMiBDwOfF (string,required)
      
      
+ Response 200 (application/json)

    + Attributes (urns)



# Data Structures


Declaración de los distintos tipos de respuestas a ser entregeados por el API.


## urns (object)

+ resource_id:Identifier (string)- "urn:tve:tigosports"
+ access: true (boolean)- true
+ startDate: `2015-08-30 00:36:24`
+ endDate: `2015-09-30 00:36:24`


## urns2 (object)

+ resource_id:Identifier (string)- "urn:tve:tigosports-lbf"
+ access: true (boolean)- true
+ startDate: `2015-11-30 00:36:24`
+ endDate: `2015-12-30 00:36:24`




## multiObject (object)

+ action: set,
+ subscriberId: 595983394460,
+ channel: 1,
+ externalId: 595983394460
+ urn: (array[urns2])

## subscriber (object)

+ status: OK (string) - Response Status
+ error (string, nullable, required) - Value of this field can be either unset or of the `string` type
+ result (object)
 + subscriberId: 595982997707 (string) - Identifier subscribers
 + businessUnit: movil (string) - Could be `home|other|movil`
 + country: py (string) - Code representing country
 + userId: 37693e5a-982a-11e4-b632-79bafe29d13e (string) - 
 + externalId:pry-123123
 + channel: 1 (number) -
 + insertDate: `2015\-01\-09 18:06:21` - Register Date
 + updateDate: `2015\-01\-30 00:36:24` - Update date
 + type:subscriber


## subscriberWithURN (object)


+ status: OK (string) - Response Status
+ error (string, nullable, required) - Value of this field can be either unset or of the `string` type
+ result (object)
 + subscriberId: 595982997707 (string) - Identifier subscribers
 + businessUnit: movil (string) - Could be `home|other|movil`
 + country: py (string) - Code representing country
 + exteberkUd: 595982997707 (string) - 
 + userId: 37693e5a-982a-11e4-b632-79bafe29d13e (string) - 
 + channel: 3 (number) -
 + insertDate: `2015\-01\-09 18:06:21` - Register Date
 + updateDate: `2015\-01\-30 00:36:24` - Update date
 + URNs (array[urns],required) - URN\'s owned by subscriber
 + type:subscriberId

## deactivate (object)

+ status: OK (string) - Response Status
+ error (string, nullable, required) - Value of this field can be either unset or of the `string` type
+ result (object)
  + message: deactivated (string)-
  + subscriberId: 595982997707 (string)

## subscriberPost(object)

   + channel:1 (required,number)
   + externalId:pry-9999 (required,string)
   + operatorId:NMSKY3432423432NMNB4324 (required,string)
   + urn:(array[urns,urns2],required) - Should be an *array* of entitlement
   

## subscriberUpdate(object)
    
  + channel:1
  + externalId:pry-9999
  + operatorId:NMSKY3432423432NMNB4324 (required,string)


# Group Provisioning Carrier

## Provisioning Multi Collection [/carrier-multi]

### Provisioning [POST]

To be used for massive registration of subscribersId's.


Ensure you send the **Basic Authorization** 

+ Request 
 
   + Headers
       
             Content-Type : application/json
             Authorization : Basic asdasd

    + Attributes (array[multiObject])
        


+ Response 200 (application/json)

    + Attributes (array[subscriber,deactivate])

