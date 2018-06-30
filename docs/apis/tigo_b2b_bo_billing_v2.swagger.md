tigo_b2b_bo_billing_v2
======================
This is the Standard API related to Billing in Version 2 for BOtermsOfService: http://swagger.io/terms/


**Version:** 1.0.0

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
|read|Allows read bills collection|

### /customers/{idType}/{id}/bills
---
##### ***GET***
**Summary:** Find the Customers Bills Collection by the Client Number

**Description:** This resource returns Bills Collection optionally can be filtered by the Contract Number

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | The Identifier number related to the Type (the Local Client Number in this case) | Yes | number |
| idType | path | Identification Type (related to the Local Client Number) | Yes | string |
| pageInit | query | Initial number for pagination | No | integer |
| quantity | query | Number of bills to be returned | No | integer |
| contractNumber | query | Contract Number Identification | Yes | integer |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [billsCollection](#billscollection) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### Models
---

### billsCollection  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| contractNo | string | Contract number | No |
| billingAddress | [ [address](#address) ] | Addresses related to the contract | No |
| dueDate | string | Account expiration date | No |
| invoiceCollection | [ [invoice](#invoice) ] | Invoices related to the contract | No |

### address  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| street | string | Customer address | No |
| neighborhood | string | Neighborhood where the customer lives | No |
| city | string | City ??where the consumer lives | No |
| state | string | State where the consumer resides | No |
| country | string | Country of residence of the consumer | No |
| zipCode | string | Customer zipCode | No |

### invoice  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| invoiceContractNo | string | Invoice contract number | No |
| invoiceNumber | string | Invoice number | No |
| billPeriod | string | Billing period | No |
| invoiceAmount | integer | Total invoice value | No |
| invoiceStatus | boolean | Invoice Status | No |

### errorBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error | object |  | No |