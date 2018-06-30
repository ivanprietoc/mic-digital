Fulfillment Payment Gateway
===========================
This the especific description for the API for a centralized Fulfillment Payment Gateway, this documentation is in swagger-2.0 specification. 

This solution is to be used in all countries, each country will be indentified in the path. This solution covers the registration of a payment to be applied to services or products, and it is agnostic to the provisioning details.
Each country may provide several APIs to cover the wide range of business units and product categories that are offered. Both the business unit and the product category will be part 
of the path. 

The API Proxy will group all the fulfillment methods a country offers, and will be named <b>tigo_{country}_fulfillment_v1</b>

So the base for each proxy wiil be: 

<b>`/v1/tigo/{country}/fulfillment`</b>

And then the path will include the business unit and product type:

<b>`/{businessunit}/{productType}`</b>

Suggested Examples:
* `/v1/tigo/gt/fulfillment/mobile/topups/`
* `/v1/tigo/sv/fulfillment/home/invoices/`
* `/v1/tigo/gt/fulfillment/invoices/` 
[For a convergente payment businessUnit is ommited]

These methods will allow the use of different identifiers for the services and products being paid, since some services will requires the MSISDN, others like Home the contractId.
Even more specific identifiers like billingAccountId or subscriptionNumber may be needed. 
To address this scenerio of multiple possible ids, the path includes two variables: idType and id. 

<b>idType</b>: The type of identification being used expressed in a "domain" form.

<b>id</b>: The unique identifier within the domain.

Common combinations include:
* `/subscribers/{msisdn}` -> also knows as the mobileid in TigoId
* `/contracts/{contractId}` -> also know as the homeid in TigoId
* `/billingaccounts/{billingAccountId}` -> The unique identifier within the billing system
* `/subscriptions/{subscriptionNumber}` -> The unique idenetifier in the provisioning platform

Use of identifications like Cedula or NIT are not recommended since they may be ambiogus on how to apply the payment if the customer have several services.

Full Path Samples:
* `/v1/tigo/gt/fulfillment/mobile/topups/subscribers/3053083937`
* `/v1/tigo/sv/fulfillment/sv/home/invoices/contracts/1234567890`    

We are going to usse HATEOAS Driven REST APIs. 
HATEOAS (Hypermedia as the Engine of Application State) is a constraint of the REST application architecture that keeps the RESTful style architecture unique from most other network application architectures.
What this means is that the body will include links with additional details and actions that can be triggered for this transaction. By providing the links, there is no need to know in advance which are the URLs needed to take those actions.
Examples of these links include
* A link to query information about the payment instrument used. In case of a credit card, masked information about the card can be retrieved in the provided link.
* A link to request a rollback of the payment. Although we want to avoid this situation and we want to manage all rollbacks within the Regional Orchestration Module, if for some reason this is needed, the link to trigger this action will be provided.

<i>This is the MVP. In this section we will be summarizing all the doubts that are raised with the teams of the different teams to remain with the questions and their respective answers.</i>

The details of the related concepts are described in the following document-

https://millicom-my.sharepoint.com/personal/andres_cavallin_millicom_com/_layouts/15/guestaccess.aspx?guestaccesstoken=JvRZ65J8I9FUZpUwLQRYJWRPu8%2fgVvaA2zUCn0BMm4s%3d&docid=2_121c58b7e6f6043a1a37d9ff3edf9a2d5&rev=1


**Version:** 1.0.0

**Terms of service:**  
http://swagger.io/terms/

**Contact information:**  
Armando Umerez  
http://www.millicom.com  
armando.umerez@millicom.com  

**License:** [MIT](http://github.com/gruntjs/grunt/blob/master/LICENSE-MIT)

### Security
---
**backend_auth**  

|apiKey|*API Key*|
|---|---|
|Description|This is the security that must be implemented by the countries, in addition to any authentication mechanism they have, this additional security serves to sign the message. Since the message is signed, the country can be sure the payment is real and that it was not forged by any other party, for example, a developer with access to Apigee.  Another benefit of the Token is that the token can be passed through proxies without the need for those proxies to know the signing details and password.        Use of JWT standard was discarded since JWT allows for for the caller to set the hash algorithm to 'None', effectively bypassing the security. For that reason we are going to force the algorithm to HMAC with SHA-256 using a pre-shared key.  The payload to be signed will include the following values:  'productType' + 'IdType' + 'id' +  'paymentGatewayTransactionId' +  'paymentCurrencyId' + 'paymentAmount' +  'RegistrationDate' + '[pre-shared secret]' |
|Name|Token|
|In|header|

**apigee_auth**  

|oauth2|*OAuth 2.0*|
|---|---|
|Description|This is the security implemented in Apigee Proxy. Any party in possession of a bearer token (a "bearer") can use it to get access to the associated resources (without demonstrating possession of a cryptographic key). To prevent misuse, bearer tokens need to be protected from disclosure in storage and in transport. |
|Flow|accessCode|
|Authorization URL|https://prod.api.tigo.com/oauth/client_credential/accesstoken?grant_type=client_credentials|
|Token URL|https://myapp.tigo.com/tigoid/callback|
|**Scopes**||
|openid|Used to identify this API is compliant with the OpenID Connect 1.0 specification|

### /{productType}/{idType}/{id}/paymentregistrations/
---
##### ***GET***
**Summary:** Get Payment Registrations By IdType And Id

**Description:** Get Payment Registrations. Returns all transactions that were made to the specified id in the domain of idType.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| productType | path | Product Category Name for which this payment registration is intended | Yes | string |
| idType | path | Type of the Unique number of identification in the billing system | Yes | string |
| id | path | Unique number of identification in the billing system | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | List of payments registrations responses | [PaymentRegistrationResponseList](#paymentregistrationresponselist) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `contractId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***POST***
**Summary:** Create Payment Registration By IdType And Id

**Description:** Create a new payment registration for the specified Id in the domain of IdType. Provisioning to be handled by the backend.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| productType | path | Product Category Name for which this payment registration is intended | Yes | string |
| idType | path | Type of the Unique number of identification in the billing system | Yes | string |
| id | path | Unique number of identification in the billing system | Yes | string |
| payment | body | description of the product that they are going to use | Yes | [PaymentRegistrationInfo](#paymentregistrationinfo) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Payment registration successfully received, validated and was processed synchronously by backend. Commit payment. | [PaymentRegistrationResponse](#paymentregistrationresponse) |
| 201 | Payment registration successfully received, validated and will be processed asynchronously by backend. Commit payment. | [PaymentRegistrationResponse](#paymentregistrationresponse) |
| 202 | Payment registration successfully received but has not been validated. Processing by backend may still fail. Don't Commit payment. | [PaymentRegistrationResponse](#paymentregistrationresponse) |
| 403 | Forbidden. Check `error.message` for details. Rollback payment. | [errorBody](#errorbody) |
| 404 | The specified `IdType` and `Id` cannot be processed. Rollback payment. | [errorBody](#errorbody) |
| 409 | Duplicate Payment Registration. Not accepted. Use `Get Payment Registration By Payment Registration Id` to determine course of action. | [errorBody](#errorbody) |
| 412 | Parameters validation failed. Will not accept. Rollback payment. | [errorBody](#errorbody) |
| default | unexpected error. Use `Get Payment Registration By Payment Registration Id` to determine course of action. | [errorBody](#errorbody) |

### /{productType}/{idType}/{id}/paymentregistrations/{paymentRegistrationId}
---
##### ***GET***
**Summary:** Get Payment Registration By IdType And Id And Payment Registration Id

**Description:** Get the Payment Registration specified bu the provided Id. 
If the transaction does not exists a 404 is expected. Payment can be rollbacked.
If the transaction is being processed and has not finished a 202 must be returned. Payment cannot be commited yet.
If the transaction was processed a 200 OK is expected and payment can be commited.


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| paymentRegistrationId | path | This is the id number of the transaction | Yes | string |
| productType | path | Product Category Name for which this payment registration is intended | Yes | string |
| idType | path | Type of the Unique number of identification in the billing system | Yes | string |
| id | path | Unique number of identification in the billing system | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Payment registration was received and payment can be commited. | [PaymentRegistrationResponse](#paymentregistrationresponse) |
| 202 | Payment registration was received but still being processed. Payment cannot be commited yet. | [PaymentRegistrationResponse](#paymentregistrationresponse) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `PaymentRegistrationId` was not found. Payment can be rollbacked. | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### Models
---

### PaymentRegistrationInfo  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| productReference | string | This is the uniqued identifier that may be needed to complement the productType. For example if the productType is "packets", the productReference may be a packet identifier.
Or if the productType is "invoices" then the productReference will be the Invoice Reference Number.
 | No |
| invoiceReferenceNumber | string | This is the uniqued identifier of the INVOICE being paid, some of our countries allow for incomplete amounts | No |
| paymentAmount | number | Amount to be paid for the particular invoice and ContractNumber. | Yes |
| paymentCurrencyId | string | Three digit ISO identifier of the currency in which the payment is being posted. | Yes |
| customerType | string | This is an enumeration of customerTYPES MOBILE HOME B2B | No |
| custumerIdType | string | This is the type of the document that the user have. | No |
| customerId | string | This is the unique identifier of the customer for millicom. In the following way | No |
| paymentGatewayTransactionId | string | This is the TransactionID of our Millicom Payment Gateway | Yes |
| paymentProcessortransactionId | string | This is the TransactionID of the Processing Partner, at the point of writing this documentation this is the Cybersource Payment Gateway transactionID | No |
| paymentProcessorId | string | Id of the processor identification, this must be a descriptive indetificator | No |
| authorizationCode | string | This is the authorization code of the reconciliation | No |
| merchantId | string | Id of the Merchant code registered on the bank institution | No |
| merchantName | string | Friendly name of the Merchant registered on the bank institution | No |
| paymentRegistrationAttemptId | string | Id fulfillmentEngine Transaction | No |
| paymentChannel | string | Channel where the invoice is being marked from. | No |
| registrationDate | date | Date when the payment was registered in ISO 8601 format | Yes |
| purchaseOrderId | string | This is the purchase order number of the app. | No |
| customerEmail | string | An email address associated with this payment | No |
| phoneNumber | string | Phone number associated with this payment registration | No |
| customerIpAddress | string | IP Address from client that submitted the registration, if it was online. | No |
| BillToAddress | [BillToAddress](#billtoaddress) |  | No |
| paymentInstrument | [PaymentInstrument](#paymentinstrument) |  | No |
| ItemDetailList | [ [ItemDetail](#itemdetail) ] | This is an array of the differents items in the purchase | No |
| nameValuePairList | [NameValuePairList](#namevaluepairlist) |  | No |
| links | [ [Link](#link) ] | This is an array with the options that they can operate with the response. This is the aplicatino of HATEOAS | No |

### Link  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| href | string | This is the url of the method, in the first aproach we are going to use get order information and payment information. With this architecture we can use it asynchronous | No |
| rel | string | Description of the action in the method | No |
| method | string | Name of the HTTP method. | No |

### BillToAddress  

This is the information about the billing address

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| firstName | string | This is the name of the item, is the exact name that user must read. | No |
| lastName | string | This is the description of the item. | No |
| country | string | This is the country of the address | No |
| city | string | This is the city of the address | No |
| street | string | This is the street of the address | No |
| postalCode | string | This is the postal code of the address | No |
| state | string | This is the state of the address | No |

### ItemDetail  

This is the detail of the item

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| name | string | This is the name or Id of the item, is the exact name that user must read. | No |
| quantity | number | Quantity of the item | No |
| amount | double | This is the amount in a double | No |

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

### PaymentRegistrationResponseList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| PaymentRegistrationResponseList | array |  |  |

### PaymentRegistrationResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| paymentRegistrationId | string | This is the id of this payment registration in the billing system. | Yes |
| paymentGatewayTransactionId | string | This is the id of the payment on the Payment Gateway. This is id was sent on the Create Payment Registration | Yes |
| registrationDate | date | Date when the payment was registered in ISO 8601 format | Yes |
| paymentCurrencyId | string | Three digit ISO identifier of the currency in which the payment is being posted. | No |
| paymentAmount | number | Amount to be paid for the particular invoice and ContractNumber. | Yes |
| PaymentActionId | string | See PaymentActionName for description. | No |
| PaymentActionName | string | [0-Commit] The Payment Registration was received and validated. Payment must be commited. 
For consistency both HTTP 200 and HTTP 201 must return 0-Commit.
[1-Rollback] The Payment Registration was received but an error ocurred while processing it asynchronously on the backend. Payment must be rollbacked.
For consistency, only transactions that returned HTTP 202 during creation are allowed to return 1-Rollback when queried.
[2-Wait] The Payment Registration was received but still being processed. 
For consistency, only transactions that returned HTTP 202 during creation or transaction that timed out and never returned a response can return the 2-Wait action.
 | No |
| message | string | Success Message from platform. May be ommited. | No |

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