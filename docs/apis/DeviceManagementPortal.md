FORMAT: 1A
HOST: https://test.api.tigo.com/v1/tigo/home/co/dmp

# Device Management Portal 


## Group Customers
## Parental Rating [/customers/{customerId}/parentalRating]

Este método permite crear, consultar, y modificar el los atributos asociados al parental Rating

dado un partnetCustomerID.


+ Parameters
    
    + customerId : `CO0001`(string) - Customer ID
    

    
### Obtain Parental Rating [GET]

+ Request 
 
   + Headers
       

             Authorization : Bearer Jfy4Q2sZXtQ5
+ Response 200 (application/json)

        { 
            "code": 200,
            "message": "Datos encontrados", 
            "params": 
            {
            "hideAdults": true, 
            "ratingLimits": "COLOMBIA.21" 
            } 
      
          }

+ Response 404 (application/json)

        {
            "error": 
            {
                "statusCode": 404,
                "code": "e01",
                "message": "Datos no encontrados",
                "developerMessage": "Non success response"
            }
        }

### Create Parental Raiting [POST]

+ Request 
 
   + Headers
       

             Authorization : Bearer Jfy4Q2sZXtQ5 
 + Body

            {
            "hideAdults":false,
            "ratingLimits":"COLOMBIA.15"
            }



+ Response 200 (application/json)

        {
            "code": 200, 
            "message": "Datos almacenados" 
        }

### Update Parental Raiting [PUT]

+ Request 
 
   + Headers
       

             Authorization : Bearer Jfy4Q2sZXtQ5
 + Body

            {
            "hideAdults":false,
            "ratingLimits":"COLOMBIA.15"
            }



+ Response 200 (application/json)

        {
            "code": 200, 
           "message": "Datos actualizados" 
        }


## Group Customer Devices

## Obtain Customer Devices [/customers/{customerId}/devices]

+ Parameters

    + customerId: `CO0001` (string) - Customer Id
    
### List Customer Devices [GET]
+ Request 
 
   + Headers
       

             Authorization : Bearer Jfy4Q2sZXtQ5
+ Response 200 (application/json)

        { 
        "code": 200,
        "message": "OK",
        "devices": 
        [ 
            { 
                "tsn": "D6A100005000055", 
                "name": "Prueba EDGE", 
                "type": "STB" },
            {   "tsn": "D6A100005000056",
                "name": "Sala Comedor", 
                "type": "MOVIL" } 
            
        ]
        }

## Delete Customer Device [/customers/{customerId}/devices/{deviceId}]

+ Parameters

    + customerId: `CO0001` (string)
    + deviceId:`D6A100005000055`(string)
    
    
### Delete Customer Device [DELETE]
+ Request 
 
   + Headers
       

             Authorization : Bearer Jfy4Q2sZXtQ5
+ Response 200 (application/json)

        { 
        "code": 200,
        "message": "OK" 
        }


## Group Devices

## Update FriendlyName [/devices/{deviceId}/friendlyName]

+ Parameters

    + deviceId:`D6A100005000055` (string) - Identifier SBT

### Update FriendlyName [PUT]


+ Request 
 
   + Headers
       

             Authorization : Bearer Jfy4Q2sZXtQ5 
 + Body

            {
            "name":"COMEDOR SALA"
            }


+ Response 200 (application/json)

            { 
                "code": 200,
                "message": "OK" 
            }

## Reset Pin [/devices/{deviceId}/pin]

+ Parameters

    + deviceId: `D6A100005000055` (string) - Identifier SBT
    
### Update Pin [PUT]
+ Request 
 
   + Headers
       

             Authorization : Bearer Jfy4Q2sZXtQ5

+ Response 200 (application/json)
    
        {
            "code": 200,
            "message": "OK",
            "pin": "6639"
        }