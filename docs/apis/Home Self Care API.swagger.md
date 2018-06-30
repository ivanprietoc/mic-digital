Home Self Care API
==================
This is the standard API for Self Care functions related to TV, Internet, Voice and all other Home services for Tigo including TigoSTAR and UNE. 
We use swagger-2.0 specification
    
What is a ContractId? This is a unique identifier for a relation between our company and our customer.
Some customers may have more than one Contract, for example they can have one contract for their vacation home at the beach,
and other contract for their everyday home. Most resourcers require a ContractId value on the path.
Many methods have a counterpart method that use a compound key using a document type and a document number. 
Those methods that are queried by doc-type and customerId (the document number) will return data
from several contracts.

Additionally, one contract may have different products associated. For example "Internet", "TV", "Telefon�a Fija".
Each Product will have a base offering and additional offerings that are part of the product. for example the base offering can be "Basic Plan TV" and a second offering can be "HBO".
Each offering may have a list of devices associated, typically only the main offer has devices.

The Product Hierarchy is like this <br>
ProductList -> Product -> OfferingList -> Offering -> DeviceList -> Device    


**Version:** 1.0.0

**Terms of service:**  
http://swagger.io/terms/

**Contact information:**  
Andres Cavallin  
http://www.millicom.com  
andres.cavallin@millicom.com  

**License:** [MIT](http://github.com/gruntjs/grunt/blob/master/LICENSE-MIT)

### /billing/contracts/{contractId}/invoices/
---
##### ***GET***
**Summary:** Get Invoices by contractId

**Description:** [NOTE] Asking for more than 3 invoices may have an impact on time and accuracy of information.

Returns a list of up to 5 most recent invoices for the contractId specified.
If this customerId has more than one contract, query each one by contractId to obtain them.        


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |
| limit | query | number of invoices to return | No | integer |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Invoices associated with provieded contractId were found | [InvoiceList](#invoicelist) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `contractId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***POST***
**Summary:** Create Invoice by contractId

**Description:** Creates a new invoice for the provided contract and for the amount provided in the body. 
This may serve to create invoices for partial payments where available.


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |
| body | body |  | Yes | object |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | Invoice associated with provieded contractId sucessfully created | object |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `contractId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /billing/contracts/{contractId}/invoices/{invoiceId}
---
##### ***GET***
**Summary:** Get Invoice by contractId and invoiceId

**Description:** Returns the invoice details that matches the corresponding invoiceId and is associated with provided contractId

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |
| invoiceId | path | Unique identifier for the Invoice | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested Invoice was found | [Invoice](#invoice) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `invoiceId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /billing/contracts/{contractId}/invoices/{invoiceId}/paymentInfo
---
##### ***GET***
**Summary:** Get Invoice Payment Info by contractId and invoiceId

**Description:** If referenced invoice was payed, this method will retorn details about the payment

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |
| invoiceId | path | Unique identifier for the Invoice | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested Invoice was found | [paymentInfo](#paymentinfo) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `invoiceId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /billing/contracts/{contractId}/recurringBillingInfo
---
##### ***GET***
**Summary:** Get Recurring Billing Info by contractId

**Description:** If referenced contract is subscribed to recurring billing, this method will return details about it

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested Recurring Billing Information was found | [RecurringBillingInfo](#recurringbillinginfo) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `invoiceId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***POST***
**Summary:** Create Recurring Billing Info by contractId

**Description:** If referenced contract is not subscribed to recurring billing, this method will add the required payment information

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |
| body | body |  | Yes | [RecurringBillingInfoRequest](#recurringbillinginforequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | Recurring Billing was successfully created | [successBody](#successbody) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `contractId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***DELETE***
**Summary:** Delete Recurring Billing Info by contractId

**Description:** If referenced contract is subscribed to recurring billing, this method will end the subscription

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |
| body | body |  | Yes | [cardTokenizationRequest](#cardtokenizationrequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Recurring Billing was successfully deleted | [successBody](#successbody) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `contractId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***PUT***
**Summary:** Update Recurring Billing Info by contractId

**Description:** Update referenced contract recurring billing, will overwrite current information

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |
| body | body |  | Yes | [RecurringBillingInfoRequest](#recurringbillinginforequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Recurring Billing was successfully updated | [successBody](#successbody) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `contractId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /billing/contracts/{contractId}/paperlessInvoiceInfo
---
##### ***GET***
**Summary:** Get Paperless Invoice Info by contractId

**Description:** If referenced contract is subscribed to paperless Invoice, this method will return email and other details

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested Invoice was found | [paperlessInvoiceInfo](#paperlessinvoiceinfo) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | The specified `contractId` is not subscribed to Paperless Invoice | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***PUT***
**Summary:** Update Paperless Invoice Info by contractId

**Description:** Update the paperless Invoice information for the specified contractId


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract for which the paperless Info is defined | Yes | string |
| body | body |  | Yes | [paperlessInvoiceInfoRequest](#paperlessinvoiceinforequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Paperless Invoice was successfully updated | [successBody](#successbody) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `invoiceId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***POST***
**Summary:** Create Paperless Invoice Info by contractId

**Description:** Create the paperless Invoice information when there is none, for the specified contractId


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract for which the paperless Info is defined | Yes | string |
| body | body |  | Yes | [paperlessInvoiceInfoRequest](#paperlessinvoiceinforequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | Paperless Invoice subcription was scuessfully created | [successBody](#successbody) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `invoiceId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***DELETE***
**Summary:** Delete Paperless Invoice Info by contractId

**Description:** Remove the paperless Invoice information for the specified contractId


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract for which the paperless Info is defined | Yes | string |
| body | body |  | Yes | [paperlessInvoiceInfoRequest](#paperlessinvoiceinforequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Paperless Invoice subscription succesfully removed | [successBody](#successbody) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `invoiceId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /billing/contracts/{contractId}/{idType}/{id}/paperlessInvoiceInfo
---
##### ***GET***
**Summary:** Get Paperless Invoice Info by contractId and idType and Id

**Description:** If referenced contract and its subaccount provided in the id, is using paperless Invoice, this method will return email and other details.
Guatemala uses subscriptions as idType and uses a subscriptionNumber as the id.
El Salvador uses billingaccounts as idType and uses the billingAccountId as the id. 
Colombia does not use this method, only uses the contractId.


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |
| idType | path | Possible values sor far are subscriptions for Guatemala and billingaccounts for El Salvador. | Yes | string |
| id | path | Unique identifier for the Subscription or main account in the billing system. In Guatemala it may be the phone number, MSISDN or line; known as subscriptionNumber. El Salvador the billing system Id is used, known as billingAccountId. | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested Invoice was found | [paperlessInvoiceInfo](#paperlessinvoiceinfo) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | The specified `contractId` is not subscribed to Paperless Invoice | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***PUT***
**Summary:** Update Paperless Invoice Info by contractId and idType and Id

**Description:** Update the paperless Invoice information for the specified contractId and subscriptionNumber


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract for which the paperless Info is defined | Yes | string |
| idType | path | Possible values sor far are subscriptions for Guatemala and billingaccounts for El Salvador. | Yes | string |
| id | path | Unique identifier for the Subscription or main account in the billing system. In Guatemala it may be the phone number, MSISDN or line; known as subscriptionNumber. El Salvador the billing system Id is used, known as billingAccountId. | Yes | string |
| body | body |  | Yes | [paperlessInvoiceInfoRequest](#paperlessinvoiceinforequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Paperless Invoice was successfully updated | [successBody](#successbody) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `invoiceId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***POST***
**Summary:** Create Paperless Invoice Info by contractId and idType and Id

**Description:** Create the paperless Invoice information when there is none, for the specified contractId


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract for which the paperless Info is defined | Yes | string |
| idType | path | Possible values sor far are subscriptions for Guatemala and billingaccounts for El Salvador. | Yes | string |
| id | path | Unique identifier for the Subscription or main account in the billing system. In Guatemala it may be the phone number, MSISDN or line; known as subscriptionNumber. El Salvador the billing system Id is used, known as billingAccountId. | Yes | string |
| body | body |  | Yes | [paperlessInvoiceInfoRequest](#paperlessinvoiceinforequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | Paperless Invoice subcription was scuessfully created | [successBody](#successbody) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `invoiceId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***DELETE***
**Summary:** Delete Paperless Invoice Info by contractId and idType and Id

**Description:** Remove the paperless Invoice information for the specified contractId


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract for which the paperless Info is defined | Yes | string |
| idType | path | Possible values sor far are subscriptions for Guatemala and billingaccounts for El Salvador. | Yes | string |
| id | path | Unique identifier for the Subscription or main account in the billing system. In Guatemala it may be the phone number, MSISDN or line; known as subscriptionNumber. El Salvador the billing system Id is used, known as billingAccountId. | Yes | string |
| body | body |  | Yes | [paperlessInvoiceInfoRequest](#paperlessinvoiceinforequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Paperless Invoice subscription succesfully removed | [successBody](#successbody) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `invoiceId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /billing/doc-type/{docTypeId}/customers/{customerId}/invoices/
---
##### ***GET***
**Summary:** Get Invoices by customerId

**Description:** Returns a list up to the 5 most recent invoices associated to this customerId 
for only the first contract associated with this customer. 
If this customerId has more than one contract, a query by contractId must be used to obtain them.


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| docTypeId | path |  | Yes | string |
| customerId | path | Unique identifier for the Customer, may be NationalId or Tax Payer Number | Yes | string |
| limit | query | number of invoices to return | No | integer |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Invoices associated with provided customerId were found | [InvoiceList](#invoicelist) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `customerId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /billing/doc-type/{docTypeId}/customers/{customerId}/invoices/{invoiceId}
---
##### ***GET***
**Summary:** Get Invoice by customerId and invoiceId

**Description:** Returns the invoice details that matches the corresponding invoiceId and is associated with provided customerId

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| docTypeId | path |  | Yes | string |
| customerId | path | Unique identifier for the Customer, may be NationalId or Tax Payer Number | Yes | string |
| invoiceId | path | Unique identifier for the Invoice | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested Invoice was found | [Invoice](#invoice) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `invoiceId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /billing/doc-type/{docTypeId}/customers/{customerId}/contracts/
---
##### ***GET***
**Summary:** Get Contracts by customerId

**Description:** Returns a list of all contracts associated to this customerId, 
including a contractId that can be used to query invoices, and the address associated with it.
Contracts are not grouped by Address.


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| docTypeId | path |  | Yes | string |
| customerId | path | Unique identifier for the Customer | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Contracts associated with provided customerId were found | [ContractList](#contractlist) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `customerId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /billing/doc-type/{docTypeId}/customers/{customerId}
---
##### ***GET***
**Summary:** Get Customer by customerId

**Description:** Return information about the Customer that matches the provided docTypeId and customerId


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| docTypeId | path |  | Yes | string |
| customerId | path | Unique identifier for the Customer | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Customer contact Info for the provided customerId were found | [CustomerExtendedInfo](#customerextendedinfo) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `customerId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /billing/contracts/{contractId}/customers
---
##### ***GET***
**Summary:** Get Customer by contractId

**Description:** Return information about the Customer that matches the provided contractId


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Customer contact Info for the provided customerId were found | [CustomerExtendedInfo](#customerextendedinfo) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `customerId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /billing/contracts/{contractId}/invoices/{invoiceId}/checkOut
---
##### ***GET***
**Summary:** Get ChekOut by contractId and invoiceId

**Description:** Return CheckOut Information and payment information for the latest attempt made for the contractId and invoiceId provided.
PaymentApproved = true only when transaction successfully completed


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |
| invoiceId | path | Unique identifier for the Invoice | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | CheckOut information for invoiceId provided was found | [CheckOutInfo](#checkoutinfo) |
| 202 | CheckOut information for invoiceId provided found but still in process | [errorBody](#errorbody) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | CheckOut information about  specified `invoiceId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***POST***
**Summary:** Create CheckOut for contractId and invoiceId

**Description:** Create a new CheckOut instance and retrieve information about how to complete the process and track its temporary status until approved or rejected   


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |
| invoiceId | path | Unique identifier for the Invoice | Yes | string |
| body | body |  | Yes | [CheckOutInfo](#checkoutinfo) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | CheckOut was scuessfully created | [CheckOutReference](#checkoutreference) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `invoiceId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /billing/contracts/{contractId}/invoices/{invoiceId}/checkOut/{paymentToken}
---
##### ***GET***
**Summary:** Get ChekOut by contractId and invoiceId and paymentToken

**Description:** Return CheckOut Information and payment information for the paymentToken provided.
PaymentApproved = true only when transaction successfully completed


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |
| invoiceId | path | Unique identifier for the Invoice | Yes | string |
| paymentToken | path | Unique identifier for the payment attempt at Checkout | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | CheckOut information for paymentToken provided was found | [CheckOutInfo](#checkoutinfo) |
| 202 | CheckOut information for paymentToken provided found but still in process | [errorBody](#errorbody) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | CheckOut information about  specified `paymentToken` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /billing/contracts/{contractId}/invoices/spool/billingDates/
---
##### ***GET***
**Summary:** Get Available Spool Billing Dates by contractId

**Description:** Return the billing dates that have available invoices on the spool for the specified contract. The billingDate of an invoice is the Creation Date, also known as the billing period

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested Invoice was found | [BillingDateList](#billingdatelist) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `invoiceId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /billing/contracts/{contractId}/invoices/spool/billingDates/{billingDate}/url
---
##### ***GET***
**Summary:** Get Spool URL by contractId and billingDate

**Description:** Return the URL where the spool can be downloaded for the specified contractId and billingDate. The billingDate of an invoice is the Creation Date, also known as the billing period

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |
| billingDate | path | invoice  Creation Date or billing period formatted as initial date | Yes | date |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested Invoice was found | [URLaddress](#urladdress) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `invoiceId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /billing/contracts/{contractId}/invoices/spool/{invoiceId}/url
---
##### ***GET***
**Summary:** Get Spool URL by contractId and invoiceId

**Description:** Return the encoded PDF for the specified contractId and invoiceId

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |
| invoiceId | path | Unique identifier for the Invoice | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested Invoice was found | [URLaddress](#urladdress) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `invoiceId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /billing/contracts/{contractId}/invoices/spool/{invoiceId}/pdf
---
##### ***GET***
**Summary:** Get Invoice PDF by contractId and invoiceId

**Description:** Return the encoded PDF for the specified contractId and invoiceId

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |
| invoiceId | path | Unique identifier for the Invoice | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested PDF was found for provided invoiceId | file |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `invoiceId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /billing/billingaccounts/{billingAccountId}/invoices/spool/{invoiceId}/pdf
---
##### ***GET***
**Summary:** Get Invoice PDF by billingAccountId and invoiceId

**Description:** Return the encoded PDF for the specified billingAccountId and invoiceId

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| billingAccountId | path | Unique identifier in the billing system. This can speed up searches compared to the contract. | Yes | string |
| invoiceId | path | Unique identifier for the Invoice | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested PDF was found for provided invoiceId | file |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `invoiceId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /billing/contracts/{contractId}/balance
---
##### ***GET***
**Summary:** Get Balance by contractId

**Description:** Get the total outstanding balance from the provided contractId.
This amount could be zero, a positive number if the customer owes money or negative if the customer has a credit.
If the customer has more than one invoice pending, this amount will reflect the sum of the outstanding amount from those invoices.
Example of balances are total debt, sum of all outstanding invoices, credit loss, the total credit loss for the billing account, 
over due, the sum of all outstanding invoices that as passed the over due date.        


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested Invoice was found | [BillingBalance](#billingbalance) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `invoiceId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /billing/contracts/{contractId}/measuringElement/{measuringElement}/localcalls/
---
##### ***GET***
**Summary:** Get LocalCalls by contractId and measuringElement

**Description:** Return detail about phone calls that were made by the phone provided in the measuringElement parameter during the period between dateFrom and dateTo, both inclusive.
This specific method for Colombia only returns the local phone calls.


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |
| measuringElement | path | Unique identifier for which the usage is matched, usually the phone number | Yes | string |
| fromDate | query | Results must have a date equal or later than the fromDate | Yes | date |
| toDate | query | Results must have a date earlier or equal than the toDate | Yes | date |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested Invoice was found | [CallDetailList](#calldetaillist) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `measureingElement` has no data | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /billing/contracts/{contractId}/measuringElement/{measuringElement}/calls/
---
##### ***GET***
**Summary:** Get Calls by contractId and measuringElement

**Description:** Return detail about phone calls that were made by the phone provided in the measuringElement parameter during the period between dateFrom and dateTo, both inclusive.


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |
| measuringElement | path | Unique identifier for which the usage is matched, usually the phone number | Yes | string |
| fromDate | query | Results must have a date equal or later than the fromDate | Yes | date |
| toDate | query | Results must have a date earlier or equal than the toDate | Yes | date |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested Invoice was found | [CallDetailList](#calldetaillist) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `measureingElement` has no data | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /billing/contracts/{contractId}/financing
---
##### ***GET***
**Summary:** Get Financing Details by contractId

**Description:** Get financing details like minimum amount and availability for the specified contract

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested Financing info was found | [FinancingInfo](#financinginfo) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | The specified `contractId` is not subscribed to Paperless Invoice | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /portfolio/contracts/{contractId}/products/
---
##### ***GET***
**Summary:** Get Products by contractId

**Description:** Returns a list of products associated with the provided contractId


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |
| limit | query | number of products to return | No | integer |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Products associated with provieded contractId were found | [ProductList](#productlist) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `contractId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /portfolio/contracts/{contractId}/products/{productId}
---
##### ***GET***
**Summary:** Get Product by contractId and productId

**Description:** Returns the product details that matches the corresponding productId and is associated with provided contractId

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple products into one invoice | Yes | string |
| productId | path | Unique identifier for the Product | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested Product was found | [Product](#product) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `invoiceId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***POST***
**Summary:** Add Offering by contractId and productId

**Description:** Add the specified offeringId (in body) to the provided ContractId and ProductId


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple products into one invoice | Yes | string |
| productId | path | Unique identifier for the Product. One contract may have more than one of the same Product | Yes | string |
| body | body |  | Yes | [OfferingRequest](#offeringrequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | Requested Product was found | [successBody](#successbody) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `invoiceId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***DELETE***
**Summary:** Delete Offering by contractId and productId

**Description:** Remove the specified offeringId to the provided ContractId and ProductId


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple products into one invoice | Yes | string |
| productId | path | Unique identifier for the Product. One contract may have more than one of the same Product | Yes | string |
| body | body |  | Yes | [OfferingRequest](#offeringrequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | Requested Product was found | [successBody](#successbody) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `invoiceId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /portfolio/contracts/{contractId}/products/{productId}/subscriptions/{subscriptionNumber}
---
##### ***GET***
**Summary:** Get Product by contractId and productId and subscriptionNumber

**Description:** Returns the product details that matches the corresponding subscriptionNumber and is associated with provided contractId.
Since one contract may have more than one subscription of the same product, productId is not unique within the same contract,
but subscriptionNumber is indeed unique within the same contract.


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple products into one invoice | Yes | string |
| productId | path | Unique identifier for the Product. One contract may have more than one of the same Product | Yes | string |
| subscriptionNumber | path | Unique identifier for the Subscription. This number is unique whithin the Contract | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested Product was found | [Product](#product) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `invoiceId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /portfolio/doc-type/{docTypeId}/customers/{customerId}/
---
##### ***GET***
**Summary:** Get Products by customerId

**Description:** Returns a list of products associated with the provided docTypeId and customerId


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| docTypeId | path |  | Yes | string |
| customerId | path | Unique identifier for the Customer, may be NationalId or Tax Payer Number | Yes | string |
| limit | query | number of products to return | No | integer |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Products associated with provieded contractId were found | [ProductList](#productlist) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `contractId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /tokenization/doc-type/{docTypeId}/customers/{customerId}/cardtokens/
---
##### ***GET***
**Summary:** Get cardTokens by customerId

**Description:** Retrieve cardToken and information about the tokenized card for the specified docTypeId and customerId

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| docTypeId | path |  | Yes | string |
| customerId | path | Unique identifier for the Customer, may be NationalId or Tax Payer Number | Yes | string |
| limit | query | number of tokens to return. | No | integer |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested Token Information was found | [TokenInfoList](#tokeninfolist) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `invoiceId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***POST***
**Summary:** Create Card Token for customerId

**Description:** Create a cardToken representing the provided credit card information for the specified docTypeId and customerId

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| docTypeId | path |  | Yes | string |
| customerId | path | Unique identifier for the Customer, may be NationalId or Tax Payer Number | Yes | string |
| body | body |  | Yes | [CreateCardTokenizationRequest](#createcardtokenizationrequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | Recurring Billing was successfully created | [TokenInfo](#tokeninfo) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `contractId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***DELETE***
**Summary:** Delete cardToken by customerId

**Description:** Delete the Token associated with the provided docTypeId and customerId

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| docTypeId | path |  | Yes | string |
| customerId | path | Unique identifier for the Customer, may be NationalId or Tax Payer Number | Yes | string |
| body | body |  | Yes | [cardTokenizationRequest](#cardtokenizationrequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Recurring Billing was successfully deleted | [successBody](#successbody) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `contractId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /portfolio/contracts/{contractId}/products/{productId}/availableoffers
---
##### ***GET***
**Summary:** Get Available Offers by contractId and productId

**Description:** Retrieve a list of offers available to the specified productId (Internet, TV, etc.) and contractId

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple products into one invoice | Yes | string |
| productId | path | Unique identifier for the Product | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested Product was found | [CommercialOfferingList](#commercialofferinglist) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `invoiceId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /cases/contracts/{contractId}/servicerequests/
---
##### ***GET***
**Summary:** Get Service Requests by contractId

**Description:** Returns a list of open service requests and their list of actions for the specified contract


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple products into one invoice | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Invoices associated with provided customerId were found | [ServiceRequestList](#servicerequestlist) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `customerId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /cases/doc-type/{docTypeId}/customers/{customerId}/servicerequests/
---
##### ***GET***
**Summary:** Get Service Requests by customerId

**Description:** Returns a list of open service requests and their list of actions


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| docTypeId | path |  | Yes | string |
| customerId | path | Unique identifier for the Customer, may be NationalId or Tax Payer Number | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Invoices associated with provided customerId were found | [ServiceRequestList](#servicerequestlist) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `customerId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /cases/doc-type/{docTypeId}/customers/{customerId}/scheduledvisits/
---
##### ***GET***
**Summary:** Get Scheduled Visits by customerId

**Description:** Returns a list of scheduled visits from technicians for installations 
and repairs of damages.


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| docTypeId | path |  | Yes | string |
| customerId | path | Unique identifier for the Customer, may be NationalId or Tax Payer Number | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Invoices associated with provided customerId were found | [ScheduledVisitInfo](#scheduledvisitinfo) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `customerId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /customer/contracts/{contractId}/contactinformation
---
##### ***GET***
**Summary:** Get ContactInformation by contractId

**Description:** Return information the contact that matches the provided contractId


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Customer contact Info for the provided customerId were found | [CustomerDetailInfo](#customerdetailinfo) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `customerId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /customer/contracts/{contractId}/contactinformation/phones/
---
##### ***GET***
**Summary:** Get Phones by ContactInformation by contractId

**Description:** Return list of phones from the contact that matches the provided contractId


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Customer contact Info for the provided customerId were found | [CustomerPhoneList](#customerphonelist) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `customerId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***POST***
**Summary:** Add Phone to ContactInformation by contractId

**Description:** Add phone to the contact that matches the provided contractId


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Customer contact Info for the provided customerId were found | [CustomerPhone](#customerphone) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `customerId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***DELETE***
**Summary:** Remove Phone to ContactInformation by contractId

**Description:** Remove phone information the contact that matches the provided contractId


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Customer contact Info for the provided customerId were found | [CustomerPhone](#customerphone) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `customerId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***PUT***
**Summary:** Update Phone to ContactInformation by contractId

**Description:** Update phone information the contact that matches the provided contractId


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Customer contact Info for the provided customerId were found | [CustomerPhoneUpdate](#customerphoneupdate) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `customerId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /customer/contracts/{contractId}/contactinformation/emails/
---
##### ***GET***
**Summary:** Get Emails from ContactInformation by contractId

**Description:** Return list of emails from the contact that matches the provided contractId


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Customer contact Info for the provided customerId were found | [CustomerEmailList](#customeremaillist) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `customerId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***POST***
**Summary:** Add Email to ContactInformation by contractId

**Description:** Add email to the contact that matches the provided contractId


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Customer contact Info for the provided customerId were found | [CustomerEmail](#customeremail) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `customerId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***DELETE***
**Summary:** Remove Email to ContactInformation by contractId

**Description:** Remove email information the contact that matches the provided contractId


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Customer contact Info for the provided customerId were found | [CustomerEmail](#customeremail) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `customerId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***PUT***
**Summary:** Update Email to ContactInformation by contractId

**Description:** Update email information the contact that matches the provided contractId


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Customer contact Info for the provided customerId were found | [CustomerEmailUpdate](#customeremailupdate) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `customerId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### Models
---

### Invoice  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| invoiceId | string | Unique Identifier for the Invoice | Yes |
| contractId | string | Unique Identifier for the Contract associated with this invoice | No |
| invoiceType | string | type of invoice that is generated to the client. Ex.charges, partial payments. | No |
| billingId | number | Unique Id of the billing system where this contract exists | No |
| billingName | string | Name of the billing system where this contract exists, not as consistent as billingId. | No |
| streetAddress | string | The main street address for identifying the contract | No |
| invoiceAmount | number | Total amount of the invoiced, adjusted or not. It's never Zero. | No |
| dueAmount | number | Amount that must be payed by dueDate. Zero if already payed. | No |
| minPaymentAmount | number | Minimum amount that can be payed by dueDate, only available to customers with extended credit. | No |
| taxAmount | number | tax amount, already included into the invoiceAmount | No |
| currencyId | string | This is the ISO Id of the currency | No |
| period | string | Named period for this invoice | No |
| creationDate | date | Date when the Invoice was generated | No |
| dueDate | date | Date when the Invoice must be payed without incurring in late fees | No |
| extendedDueDate | date | Date when the Invoice must be payed including generated late fees | No |
| hasAdjustments | boolean | True if the invoice has received adjustements so avoid showing the outdated PDF file. | No |
| hasPayment | boolean | True if the invoice has been already been payed in full | No |
| hasRecurringBilling | boolean | True if there is a recurring paymnet method associated to this contract | No |
| hasPaperlessInvoice | boolean | True if the customer is subscribed to receive only a digital invoice | No |
| VIP | boolean | True if customer is VIP or Plus | No |
| billingAccountId | number | The contractId identifier in the local billing system, in case they are different. | No |

### paymentInfo  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| paymentId | string | Reference to the payment in our internal systems | No |
| paymentDate | date | Date in which the Invoice was payed | No |
| paymentAmount | number | Amount of the payed amount, if ommited it assumed the payed amount was the Invoice amount to which this payment refers to. | No |
| paymentMethod | string | For Colombia the possible values are POL or PSE or FACTURANET BANCOLOMBIA | No |
| ExternalReference | string | A reference that provides trazability with payment provider | No |
| bankName | string | The bank institution associated witht he payment | No |
| cardBrand | string | Franchise or Brand of the registered card | No |

### paperlessInvoiceInfo  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| email | string | EMail where the digital Invoice is going to be sent | Yes |
| alternateEmail | string | optional secondary email for sending the digital Invoice | No |
| phoneNumber | string | Phone number associated with the digital invoice | No |
| billingId | number | Name or Id of the billing system where this contract exists | No |
| customerId | string | Unique identifier for the Customer, may be NationalId or Tax Payer Number | No |
| documentType | string | Defines if customerId es a National Id, Tax Payer Number, Passport, etc. | No |
| subcriptionStatusId | integer | 1 if the customer is subscribed to receive only a digital invoice, other number may represent cancelled, invalid address, etc. | No |
| subcriptionStatusMessage | string | A description of the status like Active | No |

### paperlessInvoiceInfoRequest  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| email | string | EMail where the digital Invoice is going to be sent | Yes |
| alternateEmail | string | optional secondary email for sending the digital Invoice | No |
| phoneNumber | string | Phone number associated with the digital invoice | No |
| billingId | number | Name or Id of the billing system where this contract exists | No |
| customerId | string | Unique identifier for the Customer, may be NationalId or Tax Payer Number | No |
| documentType | string | Defines if customerId es a National Id, Tax Payer Number, Passport, etc. | No |
| registeringAppName | string | Name of the App consuming the services, for auditing processes. Possible values may be MiTigoWeb or CanalesAlternos | No |
| customerIpAddress | string | IP Address of the customer, reported to the App server, for auditing processes | No |
| unsubscribeReasonId | number | And Id for the reson the customer decided to unsubscribe. Only needed on the DELETE | No |
| updateReason | string | A text reason the customer decided to unsubscribe or update the email. Added for SV for the first time. | No |
| affectRelatedContracts | boolean | When true, related contracts like child accounts or other accounts for the same customer, are also updated | No |

### RecurringBillingInfo  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| contractId | string | Unique Identifier for the Contract | No |
| billingId | string | Name or Id of the billing system where this contract exists | No |
| billingName | string | Name of the billing system where this contract exists, not as consistent as billingId. | No |
| cardInfo | string | Last 4 digits of credit card or account. Or full masked number if possibe (first 6 digits, 6 "X" characters and last 4 digits) | No |
| cardBrand | string | Franchise or Brand of the registered card | No |
| cardExpirationDate | string | Expiration date, month and year or full date, of the registered card | No |
| cardIssuingBank | string | Name of the issuing bank | No |
| paymentMethod | string | For Colombia the possible values are Debit = 1 or Credit = 2. This value is use to define some business logic at the front end.
For the Regional Payment Gateway this value must be different to that of "Card on file" that is already processed by a local bank institution.
 | No |
| registrationDate | date | Date when the payment was registered in ISO 8601 format | No |
| phoneNumber | string | Phone number associated with this payment registration | No |
| customerIpAddress | string | IP Address from client that submitted the registration, if it was online. | No |

### RecurringBillingInfoRequest  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| recurringBillingInfo | [RecurringBillingInfo](#recurringbillinginfo) |  | No |
| customerInfo | [CustomerInfo](#customerinfo) |  | No |
| transactionId | string | Unique Identifier for the Transaction | No |
| cardToken | string | Token obtained from the Payment Gateway | No |

### cardTokenizationRequest  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| cardToken | string | Token obtained from the Payment Gateway | No |
| customerId | string | Customer unique identifier, usually national identification number or company tax payer number | No |
| documentType | string | Defines if customerId es a National Id, Tax Payer Number, Passport, etc. | No |
| transactionId | string | Unique Identifier for the Transaction | No |
| customerIpAddress | string | IP Address of the customer, reported to the App server, for auditing processes | No |

### CreateCardTokenizationRequest  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| customerInfo | [CustomerInfo](#customerinfo) |  | No |
| address | [Address](#address) |  | No |
| cardDetails | [CardDetails](#carddetails) |  | No |
| transactionId | string | Unique Identifier for the Transaction | No |
| customerIpAddress | string | IP Address of the customer, reported to the App server, for auditing processes | No |

### CardDetails  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| cardNumber | string |  | No |
| cardExpirationDate | string |  | No |
| cardVerificationValue | string |  | No |
| cardBrand | string |  | No |
| cardPrintedName | string |  | No |

### InvoiceList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| InvoiceList | array |  |  |

### Contract  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| contractId | string | Unique Identifier for the Contract | Yes |
| billingId | string | Name or Id of the billing system where this contract exists | No |
| streetAddress | string | the main street address associated with the contract | No |

### ContractList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| ContractList | array |  |  |

### Address  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| streetAddress | string | the main street address | Yes |
| streetAddressLine2 | string | optional additional information about address like suite or floor number | No |
| stateId | string | Unique Identifier for State, Province or Department of the address. Numeric or two letter depending on each database. | No |
| stateName | string | Name of the State, Province or Department of the address | No |
| districtId | integer | Unique Identifier for County, Municipality, Town, District, Sector or Neighborhood | No |
| districtName | string | Name of the County, Municipality, Town, District, Sector or Neighborhood | No |
| cityId | integer | Unique Identifier for City associated with the address | No |
| cityName | string | Name of the City associated with the address | No |
| countryId | string | Unique Identifier for Name of the country using ISO Alpha-2 | No |
| countryName | string | Name of the country | No |
| zoneId | integer | Identifier for the internal zone | No |
| stratumId | integer | Identifier for social stratum | No |

### CustomerInfo  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| customerId | string | Customer unique identifier, usually national identification number or company tax payer number | Yes |
| documentType | string | Defines if customerId es a National Id, Tax Payer Number, Passport, etc. | No |
| name | string | First Name, Comapny Name or Full Name of the Customer | No |
| lastName | string | Last Name of the Custoemr | No |
| email | string | Email of the customer | No |
| phoneNumber | string | Preferred contact phone number for the customer | No |
| checksum | string | Some countries may have an additional digit for validating integrity of the customerId. | No |

### CustomerDetailInfo  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| name | string | First Name, Comapny Name or Full Name of the Customer | No |
| lastName | string | Last Name of the Customer | No |
| Address | [Address](#address) |  | No |
| checksum | string | Some countries may have an additional digit for validating integrity of the customerId. | No |
| customerEmailList | [CustomerEmailList](#customeremaillist) |  | No |
| customerPhoneList | [CustomerPhoneList](#customerphonelist) |  | No |
| customerIdentificationList | [ [CustomerIdentification](#customeridentification) ] |  | No |

### CustomerEmailList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| CustomerEmailList | array |  |  |

### CustomerPhoneList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| CustomerPhoneList | array |  |  |

### CustomerIdentification  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| documentType | string | Defines if customerId is a National Id, Tax Payer Number, Passport, etc. | No |
| customerId | string | Customer unique identifier, usually national identification number or company tax payer number | No |

### CustomerEmail  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| email | string | Emails of customer. | No |
| validated | boolean | True if the email was validated. False is not validated yet. | No |

### CustomerPhone  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| phoneType | string | Defines if the phone is a home phone, work phone,mobile, etc. | No |
| phone | string | Customer telephone | No |
| validated | boolean | True if the phone number was validated. False is not validated yet. | No |

### CustomerPhoneUpdate  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| oldPhone | string | Customer telephone | No |
| newPhoneType | string | Defines if the phone is a home phone, work phone,mobile, etc. | No |
| newPhone | string | Customer telephone | No |

### CustomerEmailUpdate  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| oldEmail | string | Customer email | No |
| newEmail | string | Customer email | No |

### CustomerCharacteristics  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| segmentId | string | Internal identifier for customer segmentation | No |
| segmentName | string | Friendly name for the customer segmentation | No |
| VIP | boolean | Important customers have access to video call support and other services | No |

### CheckOutInfo  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| checkOutId | string | Non-Encrypted Unique identifier returned by the Payment Gateway | No |
| invoiceId | string | Reference to the payment in our internal systems, usually the invoiceId | Yes |
| paymentDate | date | Date of the invoice that is being payer, may help to prevent frauds or errors | No |
| paymentAmount | number | Amount of the payed amount, if ommited it assumed the payed amount was the Invoice amount to which this payment refers to. | Yes |
| paymentDescription | string | Reference to the payment in our internal systems, usually the invoiceId | No |
| returnUrl | string | URL of the application payment result page | No |
| cancelUrl | string | URL redirect if customer cancels payment | No |
| paymentMethods | [ string ] | Forms of payment allowed for this process | No |
| paymentApproved | boolean | True if approved, false if not approved yet. | No |
| paymentStatus | integer | Some payment gateways may give more details on the temporary status during payment, like pending, in process. And also final status like cancelled, rejected or approved.
 | No |
| customerInfo | [CustomerInfo](#customerinfo) |  | Yes |

### CheckOutReference  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| paymentToken | string | Encrypted unique identifier for the payment attempt. Is tied to an invoiceId and amount | Yes |
| checkOutId | string | Non-Encrypted Unique identifier returned by the Payment Gateway | No |
| redirectUrl | string | Url where the user needs to be redirected, including the paymentToken to be presented | No |

### Product_Old_Please_Deleteme  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| productId | number | The Id of the product, its unique only within the contract scope | Yes |
| productName | string | The common name of the product like Internet or TV | Yes |
| subscriptionNumber | string | Unique identifier for the subscription | No |
| measuringElement | string | Unique identifier for the subscription used for metering, like the phone number | No |
| offeringId | string | An Id that identifies the offering in the backend platform | Yes |
| offeringName | string | The common name of the offering or plan, like 5GB or Premium | Yes |
| offeringLegacyId | string | Alternate Id for the offering or plan | No |
| offeringLegacyName | string | Alternate name of the product plan | No |
| serviceAddress | string | The address where the user receive the service, may be different to the one where the bill is received | No |
| active | boolean | Indicates if the product is currently active for the the contract, can be used to draw colors | No |
| status | string | A descriptive name of the satus of this service to provide better feedback about why the service is inactive, like for example Suspedido por falta de Pago | No |
| fromDate | date | Date when the customer first received this service | No |
| DeviceList | [ [DeviceList](#devicelist) ] | Products associated with provieded contractId were found | No |

### Product  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| productId | number | The Id of the product, its unique only within the contract scope | Yes |
| productName | string | The common name of the product like Internet or TV | Yes |
| serviceAddress | string | The address where the user receive the service, may be different to the one where the bill is received | No |
| offeringList | [ [Offering](#offering) ] | List of Offerings, Plans and Services contracted by the Customer | No |

### ProductList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| ProductList | array |  |  |

### Offering  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| subscriptionNumber | string | Unique identifier for the subscription | Yes |
| measuringElement | string | Unique identifier for the subscription used for metering, like the phone number | No |
| offeringId | string | An Id that identifies the offering in the backend platform | Yes |
| offeringName | string | The common name of the offering or plan, like 5GB or Premium | Yes |
| offeringLegacyId | string | Alternate Id for the offering or plan | No |
| offeringLegacyName | string | Alternate name of the product plan | No |
| active | boolean | Indicates if the product is currently active for the the contract, can be used to draw colors | No |
| status | string | A descriptive name of the satus of this service to provide better feedback about why the service is inactive, like for example Suspedido por falta de Pago | No |
| registrationDate | date | Added for Guatemala. Date when the service was registered, created or purchased. | No |
| fromDate | date | Date when the customer stopped or will stop receiving the service. For prepaid addons, date when the service expires. | No |
| toDate | date | Date when the customer stopped or will stop receiving the service. For prepaid addons, date when the service expires. | No |
| offeringType | string | The type of offering, could be Prepaid, Postpaid, etc. | No |
| mediaType | string | The type of connection, could be Copper, Coaxial, Cable Modem, HFC, Satellite | No |
| currencyId | string | This is the ISO Id of the currency | No |
| priceAmount | number | regular price for the bundled item | No |
| bundledItemList | [ [BundledItem](#bundleditem) ] | List of additional offerings or plans. Currently not used by any country. | No |
| deviceList | [ [Device](#device) ] | List of devices associated with the subscription | No |
| contract | [Contract](#contract) |  | No |

### OfferingList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| OfferingList | array |  |  |

### BundledItem  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| bundledItemId | number | Internal numeric identifier for the bundled item | Yes |
| bundledItemName | string | Name of the bundled item | Yes |
| bundledItemLegacyName | string | Alternate name of the bundled item | No |
| currencyId | string | This is the ISO Id of the currency | No |
| priceAmount | number | regular price for the bundled item | No |
| fromDate | date | Date when the customer first received the bundled item | No |
| toDate | date | Date when the customer last received the bundled item | No |
| bundledItemType | string | Type of the bundled item | No |

### Device  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| deviceId | number | Internal numeric identifier for the device | Yes |
| serialNumber | string | Serial number unique to the model and manufacturer, usually visible  on the device | Yes |
| modelId | number | Numeric identifier for the model | No |
| modelName | string | Name of the model of the device | No |
| manufacturer | string | Name of the manufacturer | No |
| type | string | Type of Media or Device | No |
| active | boolean | Indicates if the device is currently active for the the contract, can be used to draw colors | No |
| status | string | A descriptive name of the satus of this device to provide better feedback about why the service is inactive, like for example Sin Se�al | No |
| extendedUniqueIdentifier | string | An identifier whose limited uses include a 48-bit or 64-bit identifier used to address hardware interfaces within existing IEEE 802 or IEEE 802-like networking applications (MAC address) | No |

### DeviceList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| DeviceList | array |  |  |

### CustomerExtendedInfo  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| customerInfo | [CustomerInfo](#customerinfo) |  | No |
| customerCharacteristics | [CustomerCharacteristics](#customercharacteristics) |  | No |

### docTypeEnum  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| docTypeEnum | string |  |  |

### BillingDateList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| BillingDateList | array |  |  |

### URLaddress  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| URL | string | And URL address like htttp://www.tigo.com | Yes |

### TokenInfo  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| cardToken | string | Token obtained from the Payment Gateway | Yes |
| cardInfo | string | Last 4 digits of credit card or account | No |
| cardBrand | string | Franchise or Brand of the registered card | No |
| cardPrintedName | string |  | No |

### TokenInfoList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| TokenInfoList | array |  |  |

### BillingBalance  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| dueAmount | number | Amount that must be payed by dueDate. | Yes |
| minPaymentAmount | number | Minimum Amount that the user must pay before dueDate. | No |
| dueDate | date | Date when the dueAmount must be payed without incurring in late fees | No |
| lastUpdateDate | date | Date when the balance last changed, could be the date of the most recent invoice. | No |
| period | string | Named period for this pending balance. | No |
| dueInvoicesCount | number | Number of invoices with pending amounts. | No |
| hasRecurringBilling | boolean | True if there is a recurring paymnet method associated to this contract | No |

### CallDetail  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| origin | string | Originating number, usually the same measuring element. | No |
| destination | string | Called number, the one that received the call | Yes |
| destinationCityName | string | Name of the City where the destination number resides | No |
| destionationStateName | string | Name of the State or Province where the call was recevied | No |
| dateTimeStart | string (dateTime) | Date and time when the call started | No |
| dateTimeEnd | string (dateTime) | Date and time when the call ended | No |
| duration | float | Duation in minutes of the call | Yes |
| destinationType | string | A tag that helps differiantiate between national calls, international calls and mobile phone calls | No |
| operatorName | string | When known, gives information about the mobile network operator that received the call | No |
| callOffering | string | Name or reference of the plan or offering that was used to bill the call | No |

### CallDetailList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| CallDetailList | array |  |  |

### ServiceRequest  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| serviceId | string | IDServicioDano | No |
| creationDate | string (dateTime) | FechaIngreso | No |
| productName | string | NombreProducto | No |
| serviceRequestId | string | NumeroSR | Yes |
| status | string | Estado | No |
| requestType | string | SubTipo | No |
| subStatus | string | SubEstado | No |
| externalId | string | NumeroCUN | No |
| asignedGroup | string | Grupo | No |
| ServiceActionList | [ [ServiceAction](#serviceaction) ] | <ListOfAction/> | No |

### ServiceRequestList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| ServiceRequestList | array |  |  |

### ServiceAction  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| serviceActionId | string | Id of the Service Action | No |
| status | string | Estado | No |
| type | string | Tipo of Schedule, Recuperaci�n or Agendamiento | No |
| startDateTime | string (dateTime) | FechaInicial + ' ' + HoraInicial | No |
| endDateTime | string (dateTime) | FechaFinal + ' ' HoraFinal | No |
| scheduleType | string | TipoFranja | No |
| technicianName | string | Complete Name of Technician Visiting | No |
| technicianDocumentId | string | Cedula or Identification Number of Technician | No |
| technicianPictureURL | string | URL of Technician Picture Image | No |
| technicianContractorCompany | string | Name of the Contractor Company the Technician belongs to | No |
| SimplifiedOfferingList | [ [SimplifiedOffering](#simplifiedoffering) ] | List of Offerings in their simplified Version | No |

### ScheduledVisit  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| contractId | string | Unique identifier for the contract that may combine multiple services into one invoice | No |
| serviceAddressId | string | Unique Identifier of the Address where the service is going to be provided | No |
| serviceAddress | string | Address where the service is going to be provided | No |
| serviceCityName | string | Name of the City where the address belongs to | No |
| serviceStateName | string | Name of the State, Province or Department where the address belongs to | No |
| neighborhood | string | Name of the neighborhood, area or zonification reference | No |
| serviceActionList | [ [ServiceAction](#serviceaction) ] | List of Actions to be Performed at the address | No |

### ScheduledVisitInfo  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| customerId | string | Id of the Customer receiving the service, could be the CC, NIT or Passport number | No |
| msisdn | string | Tigo Mobile Phone Number of the customer. Colombia used both msisdn and Phone Number. | No |
| customerName | string | Name of the Customer receiving the service | No |
| customerPhone | string | Phone number of the Customer receiving the service | No |
| scheduledVisitList | [ [ScheduledVisit](#scheduledvisit) ] |  | No |

### SimplifiedOffering  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| offeringId | string | An Id that identifies the offering in the backend platform | Yes |
| offeringName | string | The common name of the offering or plan, like 5GB or Premium | Yes |
| offeringType | string | Type of transaction, new installation, repairing, recover equipment | No |
| subscriptionNumber | string | Unique identifier for the subscription. Needed only if the customer already is subscribed | No |
| measuringElement | string | Unique identifier for the subscription used for metering, like the phone number | No |
| productId | number | The Id of the product that this offering belongs to | No |
| productName | string | The common name of the product this offering belongs to, like Internet or TV | No |
| details | string | Details about the offering | No |

### FinancingInfo  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| isAvailable | boolean | True if Financing is availbe for the specified contract, or false if the customer can't finance the owed amount. | Yes |
| minPaymentAmount | number | Minimum amount that can be payed by dueDate, only available to customers with extended credit. | No |

### CommercialOfferingList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| CommercialOfferingList | array |  |  |

### CommercialOffering  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| offeringId | string | An Id that identifies the offering in the backend platform | Yes |
| offeringName | string | The common name of the offering or plan, like 5GB or Premium | Yes |
| includedAssets | string | Short summary of included assets for display to user | No |
| offeringDescription | string | Text explaining the offering and its coditions. | No |
| productId | string | The Id of the product that this offering belongs to | No |
| productName | string | The common name of the product this offering belongs to, like Internet or TV | No |
| amount | number | regular price for the offer | No |
| currencyId | string | This is the ISO Id of the currency | No |
| promotionAmount | number | special price for this offer | No |
| promotionDescription | string | Optional text explaining conditions regulating the discounted price, like limited period of time. If they are not included in the Description. | No |
| promotionCode | string | Code that may be required when requesting the upsell/upgrade | No |
| promotionStatus | string | Code that may help presenting the promotion to the customer | No |
| mediaType | string | The type of connection, could be Copper, Coaxial, Cable Modem, HFC, Satellite | No |
| details | string | Additional Details about the offering. Use this field for to map capabilities like ' "HD_Capable": "S" '
 | No |

### OfferingRequest  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| offeringId | string | An Id that identifies the offering in the backend platform | Yes |
| promotionCode | string | Code that may be required when requesting the upsell/upgrade | No |

### successBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| response | string | Generic response from platform. May be ommited. | No |
| message | string | Success Message from platform. May be ommited. | No |

### errorBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| code | integer |  | Yes |
| message | string |  | Yes |