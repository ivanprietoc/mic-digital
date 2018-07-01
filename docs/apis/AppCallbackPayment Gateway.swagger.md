App Callback Payment Gateway
============================
This is the specification that, any App integrating payment gateway functionalities, must implement in order to receive call backs for two events.
<ul>
<li>Processing Completed</li>
<li>Fulfillment Completed</li>
</ul>

This callbacks will enable asynchronous processing of the payment, so the App does not need to keep polling for the result. Although APIs to poll the result will be provided too.
It is expected that the App host these callbacks in their App Servers supporting HTTPS.

The base path expressed here is relative to the App Server URL. Meaning that if for example the App Server handle all API calls in this URL:

`https://micuenta.tigo.com.sv/api/`

the base path expresed here will be added at the end that URL. This will be the suggested base path:

`/v1/paymentgateway/callbacks/`

So the combined base path for the example will be

`https://micuenta.tigo.com.sv/api/v1/paymentgateway/callbacks/`

This solution is to be used in all countries, since it is assumed each country host each App Server in a different URL, the country will be simply part of the callback URL and we don't need a parameter for that.

Apps like "Mi Tigo", also known as "Mi Cuenta" may need to have different types of payments within the same App. 
For example they may need to offer invoice payment for mobile phone, invoice payments for the home business, core balance top-up for hybrid-accounts and even directly selling some on demand content.
Each one of this product types have:
  * Different fulfillment APIs in the countrie's billing system
  * Different rules for minimum amount, maximum amount and velocity
  * May even have different payment methods available, some may be too expensive for a $1 topup
  * Different fraud prevention rules like for example the acceptance of international credit cards

For these reasons, each different product type will have its own App entity in the Payment Gateway and so, will have its own set of callback URL for both payemnt and fulfillment, 
so any information about the business unit and product can be part of the url as a fixed hierarchy. For example:

* `/v1/paymentgateway/callbacks/home/invoices`
* `/v1/paymentgateway/callbacks/mobile/topups`
* `/v1/paymentgateway/callbacks/convergent/invoices`

And finally all callbacks will receive the Order Id as part of the callback URL, plus the type of callback as the resource being modified.
So notify about payment information of an order this will be method used:

`/orders/{purchaseOrderId}/payment`

And to notify about fulfillment information of an order this will be the method used:

`/orders/{purchaseOrderId}/fulfillment`

Here are two example of full callback URLs.

Sample URL to notify the App Server that a payment was processed. The App may consider this the final step and notify the user that the payment was approved. And trust the Payment Gateway to complete the fulfillment on the billing systems asyncrhonously.

`https://micuenta.tigo.com.sv/api/v1/paymentgateway/callbacks/home/invoices/orders/{purchaseOrderId}/payment`

Sample URL to notify the App Server that the fulfillment was completed. In a topup scenario, the fulfillment is more important than the payment, because if the payment is approved but the topup cannot be completed because the number was invalid or any other reason, the user needs to know as soon as possible that the transaction was not completed (and payment was rollbacked).

`https://shop.tigo.com.hn/api/v1/paymentgateway/callbacks/mobile/topups/orders/{purchaseOrderId}/fulfillment`

<i>This is the MVP. In this section we will be summarizing all the doubts that are raised with the teams of the different teams to remain with the questions and their respective answers.</i>

The details of the related concepts are described in the following document-

https://millicom-my.sharepoint.com/personal/andres_cavallin_millicom_com/_layouts/15/guestaccess.aspx?guestaccesstoken=JvRZ65J8I9FUZpUwLQRYJWRPu8%2fgVvaA2zUCn0BMm4s%3d&docid=2_121c58b7e6f6043a1a37d9ff3edf9a2d5&rev=1


**Version:** 1.0.0

**Terms of service:**  
http://swagger.io/terms/

**Contact information:**  
Andr�s Cavallin  
http://www.millicom.com  
andres.cavallin@millicom.com  

**License:** [MIT](http://github.com/gruntjs/grunt/blob/master/LICENSE-MIT)

### Security
---
**backend_auth**  

|apiKey|*API Key*|
|---|---|
|Description|This is the security that must be implemented by the countries, in addition to any authentication mechanism they have, this additional security serves to sign the message. Since the message is signed, the App Server can be sure the payment is real and that it was not forged by any other party, for example, a developer with access to the callback API.  Another benefit of the Token is that the token can be passed through proxies without the need for those proxies to know the signing details and password.  Use of JWT standard was discarded since JWT allows for for the caller to set the hash algorithm to 'None', effectively bypassing the security. For that reason we are going to force the algorithm to HMAC with SHA-256 using a pre-shared key.  The payload to be signed will include the following values (Note: paymentRegistrationId is only included in the Fulfillment callback):  'productType' + 'IdType' + 'id' +  'purchaseOrderId' + 'paymentCurrencyId' + 'paymentAmount' +  'paymentApproved' + 'paymentGatewayTransactionId' +  'RegistrationDate' + 'paymentRegistrationId' + '[pre-shared secret]' |
|Name|Token|
|In|header|

### /{productType}/orders/{purchaseOrderId}/payment
---
##### ***PUT***
**Summary:** Update Payment Information By purchaseOrderId

**Description:** Payment Information including final result and validation token for the specied purchaseOrderId

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| productType | path | Product Category Name for which this payment registration is intended | Yes | string |
| purchaseOrderId | path | Unique identification of the Order being updated. Known as purchaseOrderId for the PaymentGateway. | Yes | string |
| payment | body | Information about the payment processing result | Yes | [PaymentInfo](#paymentinfo) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 204 | Information about the order specified by Order Id was received |  |
| 403 | Forbidden or Invalid Token. Check `error.message` for details. Log error and trigger notification. Don't Retry. | [errorBody](#errorbody) |
| 404 | The specified `purchaseOrderId` does not exists. Log error and trigger notification. Don't Retry. | [errorBody](#errorbody) |
| 409 | Duplicate update callback. Not accepted. Log error and trigger notification. Don't Retry. | [errorBody](#errorbody) |
| 412 | Parameters validation failed. Will not accept. Log error and trigger notification. Don't Retry. | [errorBody](#errorbody) |
| default | unexpected error. Callback must be retried in a few seconds. | [errorBody](#errorbody) |

### /{productType}/orders/{purchaseOrderId}/fulfillment
---
##### ***PUT***
**Summary:** Update Fulfillment Information By purchaseOrderId

**Description:** Fulfillment Information including final result and validation token for the specied purchaseOrderId

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| productType | path | Product Category Name for which this payment registration is intended | Yes | string |
| purchaseOrderId | path | Unique identification of the Order being updated. Known as purchaseOrderId for the Payment Gateway. | Yes | string |
| fulfillment | body | Information about the fulfillment registration result | Yes | [PaymentInfo](#paymentinfo) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 204 | Information about the order specified by Order Id was received |  |
| 403 | Forbidden or Invalid Token. Check `error.message` for details. Log error and trigger notification. Don't Retry. | [errorBody](#errorbody) |
| 404 | The specified `purchaseOrderId` does not exists. Log error and trigger notification. Don't Retry. | [errorBody](#errorbody) |
| 409 | Duplicate update callback. Not accepted. Log error and trigger notification. Don't Retry. | [errorBody](#errorbody) |
| 412 | Parameters validation failed. Will not accept. Log error and trigger notification. Don't Retry. | [errorBody](#errorbody) |
| default | unexpected error. Callback must be retried in a few seconds. | [errorBody](#errorbody) |

### Models
---

### PaymentInfo  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| idType | string | Type of the Unique number of identification in the billing system | No |
| Id | string | The account Id or account number of type idType | No |
| paymentAmount | number | Amount to be paid for the particular invoice and ContractNumber. | Yes |
| paymentCurrencyId | string | Three digit ISO identifier of the currency in which the payment is being posted. | Yes |
| paymentApproved | boolean |  | Yes |
| paymentResultCode | number |  | No |
| paymentGatewayTransactionId | string | This is the TransactionID of our Millicom Payment Gateway | Yes |
| paymentProcessorTransactionId | string | This is the TransactionID of our Payment Gateway, at the point of writing this documentation this is the Cybersource Payment Gateway transactionID | No |
| authorizationCode | string | This is the authorization code of the reconciliation | No |
| paymentProcessorId | string | Id of the processor identification, this must be a descriptive indetificator | No |
| merchantId | string | Id of the Merchant code registered on the bank institution | No |
| merchantName | string | Friendly name of the Merchant registered on the bank institution | No |
| registrationDate | date | Date when the payment was registered in ISO 8601 format | Yes |
| fulfillmentSucceded | boolean | True if the fulfillment was completed sucessfully. Not available on payment callback, only on fulfillment callback. | No |
| paymentRegistrationId | string | This is the id of this payment registration in the billing system. Not available on payment callback, only on fulfillment callback. | No |
| customerIpAddress | string | IP Address from client that submitted the registration, if it was online. | No |
| paymentInstrument | [PaymentInstrument](#paymentinstrument) |  | No |
| nameValuePairList | [NameValuePairList](#namevaluepairlist) |  | No |
| links | [ [Link](#link) ] | This is an array with the options that they can operate with the response. This is the aplicatino of HATEOAS | No |

### Link  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| href | string | This is the url of the method, in the first aproach we are going to use get order information and payment information. With this architecture we can use it asynchronous | No |
| rel | string | Description of the action in the method | No |
| method | string | Name of the HTTP method. | No |

### NameValuePairList  

An array of Name and Value pair to pass generic data

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| NameValuePairList | array | An array of Name and Value pair to pass generic data |  |

### NameValuePair  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| name | string | This is the name of the of data | No |
| value | string | this is the value | No |

### PaymentInstrument  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| paymentMethodId | number | Id of the Payment Instrument used for the payment | No |
| paymentMethodName | string | Friendly Name of the Payment Instrument used for the payment | No |
| maskedAccountId | string | For credit cards, first 4 and last 6. For other payment types, the accountid masked according to security best practices. For MFS it could be the MSISDN | No |
| expirationDate | date |  | No |
| bankName | string | The bank institution associated witht he payment | No |
| cardBrand | string | Franchise or Brand of the registered card | No |
| tokenized | boolean | True if the credit card information came from a token and not from user input | No |

### Error  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| code | integer |  | Yes |
| message | string |  | Yes |

### errorBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| code | integer |  | Yes |
| message | string |  | Yes |