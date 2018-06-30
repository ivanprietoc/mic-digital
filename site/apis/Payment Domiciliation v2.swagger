FORMAT: 1A
HOST: https://test.api.tigo.com/v2/tigo/mobile/co/domiciliation

# Payment Domiciliation v2


# Group Info about CreditCards

## Identification [/creditCards/{identificationId}]


### Get Credit Card By Identification [GET]

Consultar la información de las tarjetas de crédito asociadas a un pagador 


 + Parameters
 
      + identificationId (required, string, `75000001`) ... indentification.
    
 + Request
            
    + Headers
        
                Authorization: Bearer 213123132132132

 + Response 200 (application/json)

    + Attributes (cards)
 
  

# Group CreditCards


## CreditCards Collection [/creditCards]


### Add Credit Card [POST]

Registrar tarjeta de crédito para hacer pagos de facturas

+ Request(application/json) 

    + Headers
    
            Authorization: Bearer 213123132132132

    + Attributes(payer)
    
+ Response 200 (application/json)

    + Attributes(creditCard)



### Delete Credit Card [DELETE]

Eliminar tarjeta de crédito  para hacer pagos de facturas

+ Request(application/json)


   + Attributes(deleteRequest)
      

    + Headers
    
            Authorization: Bearer 213123132132132

+ Response 200 (application/json)

    + Attributes(creditCard)


## CreditCards Payment OneClick [/creditCards/payments/oneClick]
Definir tarjeta de crédito con pago en un clic para hacer pagos de facturas 
### Payment Credit Card OneClick [POST]

+ Request  (application/json)

    + Attributes(creditCardOneClick)
    
+ Response 200 (application/json)

    + Attributes(creditCardOneClickResponse)

# Group Payments


## Query Payments Collection [/payments/{identificationId}/{filterPayment}]

Consultar historial de pago


### Get Payments by Transactions [GET]

Se realiza la búsqueda por medio número de transacción.

+ Parameters

    + identificationId (required,string `7509783322`)... transaction Id 
    + filterPayment (required, string, `transaction`) ... transaction.

+ Request
   + Headers

            Authorization : Bearer UjvkkqZ3eFLyLl7fkc4tkLfZkjWe


+ Response 200 (application/json)

    + Attributes(transactionPago)

### Get Payment by Reference Code [GET]

Se realiza la búsqueda por medio referencia de pago.

+ Parameters

    + identificationId (required,string `30289706`)... referencia de pago 
    + filterPayment (required, string, `reference`) ... referencia de pago


+ Response 200 (application/json)

    + Attributes(referencePago)


### Get Payment by Identification Code [GET]

Se realiza la búsqueda por medio del identificador del pagador.

+ Parameters

    + identificationId (required,string `750978701`)... identificador Id
    + filterPayment (required, string, `identification`) ... identification


+ Response 200 (application/json)

    + Attributes(identificationPago)





# Data Structures
## token (object)
+ correlationId:`61f40251-26d7-46bc-95bc-4347e8e7db43`

## token2 (object)
+ correlationId:`431das40251-26d7-46bc-95bc-4347e8e7232143`


## deleteRequest (object)
+ dni:2321312312
+ tokens(array[token,token2])


## payer(object)

+ payer(object):
  + fullName:APPROVED,
  + email:juan.villarraga@mail.tigo.com.co,
  + contactPhone:8001811,
  + dni:75000001,
  + dniType:CC,
  + street1:Calle 34 # 25 - 50,
  + street2:Calle 34 # 25 - 51,
  + city:Manizales,
  + state:Caldas,
  + country:Colombia,
  + postal:1112,
  + phone:8001812
+ cc(object):
 + name:Carlos Andres Grisales2,
 + number:4916140783532244,
 + expirationDate:2018/12,
 + securityCode:356,
 + paymentMethod:VISA,
 + paymentOnClick:0

## cards (object)

  + Envelope(object):
    + Header(object):
        + transactionResponseHeader(object):
           + transactionId: 750978411
    + Body(object):
       + getCreditCardsByIdentificationResponse(object):
          + TransactionResponse(object):
             + code: 100,
             + description: Transacción enviada con éxito
          + CreditCard (object);
             + creditCardExpirationDate: {},
             + creditCardNumber: 368687****1993,
             + creditCardSecurityCode: {},
             + paymentMethod: DINERS,
             + name: APPROVED,
             + paymentOnClic: true,
             + maskedNumber: {},
             + country: CO,
             + tokenCorrelationId: 2498ad03-6869-4f37-9c02-4501bb695145

## creditCard (object)

  + Envelope(object):
    + Header(object):
      + transactionResponseHeader(object):
         + transactionId: 750978419
    + Body(object):
      + addCreditCardResponse(object):
          + TransactionResponse(object):
             + code: 100,
             + description: Transacción efectuada correctamente.
         + tokenCorrelationId: 0d84c4e2-09c3-47d2-8272-332b17dc6b5e,
         + paymentMethod: VISA,
         + maskedNumber: 491614******2244,
         + fullName: Carlos Andres Grisales2,
         + identificationNumber: 75000001
      

## transactionPago (object)

  + Envelope (object)
    + Header(object)
      + transactionResponseHeader(object)
         + transactionId: 750978415
    + Body(object)
       + getPaymentsByTransactionIdResponse(object)
          + TransactionResponse(object)
            + code: 100,
            + description: Transacción enviada con éxito
          + Payments(object)
            + operation_dateTime: {},
            + orderId: 7666639,
            + platformName: 2,
            + paymentResponseCode: {},
            + pendingReason: {},
            + state: APPROVED,
            + submit_dateTime: `2015-12-07T00:00:00-05:00`,
            + transactionId: 750978700,
            + payuTransactionId: `5106179d-7d34-4aa7-b277-548089cad8a4`,
            + paymentMethod: DINERS,
          + buyerData(object)
             + fullName: APPROVED,
             + emailAddress: liliana.bejarano@mail.tigo.com.co,
             + contactPhone: 8001813,
             + dniNumber: 243316051,
             + dniType: CC,
             + street1: `Calle 34 # 25 - 52",
             + street2: `Calle 34 # 25 - 53",
             + city: Manizales,
             + state: Caldas,
             + country: Colombia,
             + postalCode: 1113,
             + phone: 8001814
          + payerData(object)
             + fullName": APPROVED,
             + emailAddress": liliana.bejarano@mail.tigo.com.co,
             + contactPhone": 8001811,
             + dniNumber": 75000001,
             + dniType":  CC,
             + street1": `Calle 34 # 25 - 50`,
             + street2": `Calle 34 # 25 - 51`,
             + city": Manizales,
             + state": Caldas,
             + country": Colombia,
             + postalCode": 1112,
             + phone": 8001812
          + accountId : {},
          + tokenCorrelationId : `2498ad03-6869-4f37-9c02-4501bb695145`
        }
      }
    }
  }
}

## referencePago(object)
  + Envelope (object)
    + Header(object)
      + transactionResponseHeader(object)
        + transactionId: 750978415
    + Body(object)
      + getPaymentsByReferenceResponse(object)
        + TransactionResponse(object)
          + code: 100,
          + description: Transacción enviada con éxito
        + Payments(object)
           + operation_dateTime: {},
           + platformName: 2,
           + paymentResponseCode: {},
           + pendingReason: {},
           + state: {},
           + submit_dateTime: `2015-12-04T00:00:00-05:00`,
           + transactionId: 750978274,
           + paymentMethod: MASTERCARD,
           + buyerData(object)
             + fullName: APPROVED,
             + emailAddress: liliana.bejarano@mail.tigo.com.co,
             + contactPhone: 8001813,
             + dniNumber: 243316051,
             + dniType: CC,
             + street1: `Calle 34 # 25 - 52`,
             + street2: `Calle 34 # 25 - 53`,
             + city: Manizales,
             + state: Caldas,
             + country: Colombia,
             + postalCode: 1113,
             + hone: 8001814
          + payerData(object)
             + fullName: APPROVED,
             + emailAddress: liliana.bejarano@mail.tigo.com.co,
             + contactPhone: 8001811,
             + dniNumber: 75000001,
             + dniType: CC,
             + street1: `Calle 34 # 25 - 50`,
             + street2: `Calle 34 # 25 - 51`,
             + city: Manizales,
             + state: Caldas,
             + country: Colombia,
             + postalCode: 1112,
             + phone: 8001812
          + accountId: {},
          + tokenCorrelationId: f01c277c-f7bd-4168-959c-82ce23ce3a62

        
## identificationPago(object)

  + Envelope (object)
     + Header (object)
      + transactionResponseHeader(object)
         + transactionId: 750978415
     + Body(object)
       + getPaymentsByIdentificationResponse(object)
          + TransactionResponse(object)
              + code: 100,
              + description: Transacción enviada con éxito
          + Payments:(array[paymentOne,paymentOne])

## paymentOne(object)
+ operation_dateTime: {},
+ platformName: 2,
+ paymentResponseCode: {},
+ pendingReason: {},
+ state: {},
+ submit_dateTime: `2016-01-11T00:00:00-05:00`,
+ transactionId: 75097841213,
+ paymentMethod: MASTERCARD,
+ buyerData(object)
   + fullName: APPROVED,
   + emailAddress: liliana.bejarano@mail.tigo.com.co,
   + contactPhone: 8001813,
   + dniNumber: 243316051,
   + dniType: CC,
   + street1: `Calle 34 # 25 - 52`,
   + street2: `Calle 34 # 25 - 53`,
   + city: Manizales,
   + state: Caldas,
   + country: Colombia,
   + postalCode: 1113,
   + phone: 8001814
+ payerData(object)
  + fullName: APPROVED,
  + emailAddress: liliana.bejarano@mail.tigo.com.co,
  + contactPhone: 8001811,
  + dniNumber: 75000001,
  + dniType: CC,
  + street1: `Calle 34 # 25 - 50`,
  + street2: `Calle 34 # 25 - 51`,
  + city: Manizales,
  + state: Caldas,
  + country: Colombia,
  + postalCode: 1112,
  + phone: 8001812
  + accountId: {},
  + tokenCorrelationId: `f01c277c-f7bd-4168-959c-82ce23ce3a62`
          

## deleteCard (object)
+ Envelope(object): 
   + Header(object):
      + transactionResponseHeader(object): 
         + transactionId": 750978418
   + Body(object):
      +deleteCreditCardResponse(object):
        +TransactionResponse(object):
          +code: 100,
          +description: "Transacción efectuada correctamente."
        
        +CreditCard(object):
          +tokenCorrelationId: "7d103c02-1a1c-4d38-abf9-9fdc5ebc2485"
   

## creditCardOneClick (object)
 + payerDni:75000001,
 + msisdn:3015321100,
 + account:"",
 + correlationId:`f01c277c-f7bd-4168-959c-82ce23ce3a6`
 

 
## creditCardOneClickResponse(object)

+ Envelope(object)
   + Header(object)
       + transactionResponseHeader(object)
          + transactionId: 7509784122
   + Body (object)
       + creditCardSelectedOneClickPaymentResponse(object)
           + TransactionResponse(object)
              + code: 100,
              + description: Transacción enviada con éxito