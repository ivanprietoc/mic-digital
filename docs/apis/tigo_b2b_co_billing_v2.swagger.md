tigo_b2b_co_billing_v2
======================
This is the Standard API related to Billing in Version 2


**Version:** 2.0.0

**Terms of service:**  
http://swagger.io/terms/

**Contact information:**  
Carlos Carvallo  
https://edge.com.py  
carlos.carvallo@edge.com.py  

**License:** [MIT](http://github.com/gruntjs/grunt/blob/master/LICENSE-MIT)

### Security
---
**application**  

|oauth2|*OAuth 2.0*|
|---|---|
|Token URL|https://test.api.tigo.com/oauth/client_credential/accesstoken?grant_type=client_credentials|
|Flow|application|
|**Scopes**||
|read|contracts|

### /contracts/{contractId}
---
##### ***GET***
**Summary:** Find Contracts By Contract Id

**Description:** Return a Contract associated to the requested ContractId


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Contract Identifier | Yes | number |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Succesful response | [contractsDetails](#contractsdetails) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unathorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /customers/{idType}/{identification}/contracts
---
##### ***GET***
**Summary:** Find Contracts By Customer Identification and his Id Type

**Description:** Return a list of Contracts associated to the Customer Identification and the Id Type


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| idType | path | Identification Type | Yes | string |
| identification | path | Unique Identifier for the Customer | Yes | number |
| reg_ini | query | Number of Pages | No | number |
| num_reg | query | Number of Records | No | number |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Succesful response | [contractsDetails](#contractsdetails) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unathorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /customers/contracts/{contractId}/bills
---
##### ***GET***
**Summary:** Find Customer Bills History by Contract Id

**Description:** Return a list of Bills associated to the Contract Identification Number


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Contract Identifier | Yes | number |
| quantity | query | Number of Bills | No | number |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Succesful response | [BillsCollection](#billscollection) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unathorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /customers/contracts/{contractId}/bills/{billNo}/payments
---
##### ***GET***
**Summary:** Find Customer Payments by ContractId and Bill number

**Description:** Return Payments associated to the Contract Identification Number

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Contract Identifier | Yes | number |
| billNo | path | Bill register number | Yes | string |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Succesful response | [Payment](#payment) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unathorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /customers/{idType}/{identification}/contracts/{contractId}/characteristics
---
##### ***GET***
**Summary:** Find Party Characteristics by Identification and Contract Id

**Description:** Return Party Characteristics associated to the Identification and the Id Type


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Contract Identifier | Yes | number |
| idType | path | Identification Type | Yes | string |
| identification | path | Unique Identifier for the Customer | Yes | number |
| fields | query | At least one of the fields separated by commas, role (Party role), plus (Is plus customer) example, ?fields=role,plus | Yes | string |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Succesful response. | [PartyCharacteristics](#partycharacteristics) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unathorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource. | [errorBody](#errorbody) |

### /customers/{idType}/{identification}/payments/checkout
---
##### ***POST***
**Summary:** This resource allows to create a transaction flow for one or many bill payments

**Description:** This resource allows create a transaction flow to make payments for one or many bills


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| idType | path | Identification Type | Yes | string |
| identification | path | Unique Identifier for the Customer | Yes | number |
| paymentDetails | body | The details about the Payment including the intent, client information, bills data, payment data and confirmation Url | Yes | [CheckoutPaymentRequest](#checkoutpaymentrequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | The succesfully response includes the signature of the payment and the url and some description if it exists  | [CheckoutPaymentResponse](#checkoutpaymentresponse) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unathorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource. | [errorBody](#errorbody) |

### /customers/{idType}/{identification}/payments/register
---
##### ***POST***
**Summary:** This resource allows register previously payments for one or many bill payments

**Description:** This feature allows to insert (register) previously made payments that did not use the UNE payment gateway, support a collection of Bills, client information and payment data


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| idType | path | Identification Type | Yes | string |
| identification | path | Unique Identifier for the Customer | Yes | number |
| paymentDetails | body | The details about the Payment including the intent, client information, bills data, payment data and confirmation Url | Yes | [CheckoutPaymentRequest](#checkoutpaymentrequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successfully response include the boolean confirmation of every bill requested for register | [RegisterPaymentResponse](#registerpaymentresponse) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unathorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource. | [errorBody](#errorbody) |

### /payments/{paymentId}/validate
---
##### ***GET***
**Summary:** validate a Payment Transaction by using the signature value

**Description:** This resource returns information about the payment using it signature, previously made through the payment gateways


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| paymentId | path | paymentId is the default value and is the signature value of the transaction | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Succesfull response related to the payment validated | [ValidatePaymentResponse](#validatepaymentresponse) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unathorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource. | [errorBody](#errorbody) |

### /payments/{couponId}/{id}/validate
---
##### ***GET***
**Summary:** validate a Payment Transaction by using coupon or signature value

**Description:** This resource returns information about the payment using it coupon, previously made through the payment gateways


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| couponId | path | Referred to a Coupon id type | Yes | string |
| id | path | The coupon number | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Succesfull response related to the payment validated | [ValidatePaymentResponse](#validatepaymentresponse) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unathorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource. | [errorBody](#errorbody) |

### Models
---

### CheckoutPaymentRequest  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| intent | string |  | No |
| clientInformation | [ClientInformation](#clientinformation) |  | No |
| billsCollection | [BillListRequest](#billlistrequest) |  | No |
| confirmationUrl | string |  | No |
| paymentData | object |  | No |

### BillListRequest  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| BillListRequest | array |  |  |

### CheckoutPaymentResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| description | string |  | No |
| error | integer |  | No |
| signature | string |  | No |
| url | string |  | No |

### RegisterPaymentResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| 909501941-90 | boolean |  | No |
| 910911145-94 | boolean |  | No |

### ValidatePaymentResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| payment_id | string |  | No |
| partner | string |  | No |
| refSale | string |  | No |
| state | string |  | No |
| startDate | string |  | No |
| amount | string |  | No |
| taxValue | string |  | No |
| baseTax | string |  | No |
| description | string |  | No |
| pay_method | string |  | No |
| trazabilityCode | string |  | No |
| email | string |  | No |
| document | number |  | No |
| documentType | string |  | No |
| userName | string |  | No |
| userLastName | string |  | No |
| userTelephone | string |  | No |
| bankName | string |  | No |
| franchise | string |  | No |
| cycleNumber | number |  | No |
| solicitedDate | string |  | No |

### ClientInformation  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| email | string |  | No |
| firstName | string |  | No |
| lastName | string |  | No |
| phone | string |  | No |
| userIp | string |  | No |

### contractsDetails  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| identification | string | Business identification | Yes |
| organization | object | Organization Details | Yes |
| contractsCollection | [ [contractsItem](#contractsitem) ] |  | Yes |

### contractsItem  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| contractId | string | Unique Identifier for the Contract | No |
| contractCharacteristics | [ContractCharacteristicsList](#contractcharacteristicslist) |  | No |
| localAddress | [LocalAddress](#localaddress) |  | No |
| billsCollection | [BillsCollection](#billscollection) |  | No |

### ContractCharacteristicsList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| ContractCharacteristicsList | array |  |  |

### ContractCharacteristics  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| cycle | string |  | No |
| deliveryMethod | string |  | No |

### LocalAddress  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| address | string |  | No |
| geographicPlace | object |  | No |

### BillsCollection  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| BillsCollection | array |  |  |

### BillList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| billNo | string |  | No |
| billDate | string |  | No |
| billAmount | string |  | No |
| paymentDueDate | string |  | No |
| billClaimStatus | string |  | No |
| billStatus | boolean |  | No |
| billingSystem | string |  | No |
| referencePayment | string |  | No |
| localAddress | [LocalAddress](#localaddress) |  | No |

### Payment  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| paymentDay | string |  | No |
| paymentMethod | string |  | No |
| bankingEntity | string |  | No |

### PartyCharacteristics  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| plusCustomer | boolean |  | Yes |
| webBillStatus | string |  | No |
| contactPhone | string |  | No |
| contactEmail | string |  | No |

### errorBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error | object |  | No |