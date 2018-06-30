Selfcare API CRM
================
This is the Standard API related to Selfcare Transactions in Version 2


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
|read|allows reading products|

### /customers/{customerCode}/products
---
##### ***GET***
**Summary:** Find the Customer Products by the Customer Code

**Description:** This resource returns a Inventory of Services (Products) of the Customer by the Client Code

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| customerCode | path | Client Code of the Subscriber | Yes | integer |
| offset | query | Initial number for pagination | No | integer |
| limit | query | Number of products to be returned | No | integer |
| Authorization | header | Access Token provided by the Token Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [ProductsList](#productslist) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### Models
---

### ProductsList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| customerCode | integer |  | Yes |
| contract | integer |  | No |
| msisdn | string |  | No |
| customerName | string |  | No |
| address | string |  | No |
| planCode | integer |  | No |
| planDescription | string |  | No |
| planValue | integer |  | No |

### errorBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error | object |  | No |