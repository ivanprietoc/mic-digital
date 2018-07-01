FORMAT: 1A
HOST: http://test.api.tigo.com/

# Tigo Mobile Ecommerce Order


## Orders Collection [/v1/tigo/mobile/py/ecommerce/orders]

### Create Order [POST]

+ Request (application/json)

     +  Attributes(Order)

+ Response 200 (application/json)

        {
  "Envelope": {
    "Header": {},
    "Body": {
      "createOrderResponse": {
        "ResponseHeader": {
          "GeneralResponse": {
            "correlationID": {},
            "status": "OK",
            "code": "00000",
            "codeType": "NEG",
            "description": "Ejecucion exitosa"
          }
        }
      }
    }
  }
}

+ Response 500 (application/json)

    {
  "error": {
    "statusCode": 500,
    "code": "soap-env:Server",
    "message": "El mensaje no cumple con la especificacion del esquema",
    "developerMessage": "output.soap.error.codeType$-El mensaje no cumple con la especificacion del esquema"
  }
}


# Data Structures


Declaración de los distintos tipos de respuestas a ser entregeados por el API.


## Order (object)

+ customer (object)
  + documentId: 3509333
  + documentType: CI
  + nationality: PY
  + name:   Javier 
  + lastName:  Kovacs 
  + phoneNumber: 595984234432
  + email: javier@gmail.com 
  + notifyEmail: false
  + state: Capital
  + city: Lambare
  + streetAddress: Mi calle 888
  + district:  Centro
  + order (object)
     + orderNumber: 43432
     + orderDate: 2017-01-22T10:01:01
     + contactTime: A,
     + requestIp: 192.168.0.1
     + subTotalAmount: 100000,
     + discountAmount: 0 ,
     + shippingCost:0,
     + currency:PYG,
     + taxes:0,
     + referer:algo
     + promotionCode:12321
     + shippingMethod:"22",
     + totalAmount:200000,
     + utmSource:"majel",
     + utmCampaign:"majelmajel",
     + utmTerm:"na",
     + utmContent:"all",
     + orderDetails (array[OrderDetail])



## OrderDetail (object)
 + productCode:"PCC",
 + productName:"Paquete de compra",
 + productType:"Generic",
 + quantity:2,
 + unitPrice:50000,
 + discountAmount":0,
 + taxAmount:0,
 + netPrice":100000

