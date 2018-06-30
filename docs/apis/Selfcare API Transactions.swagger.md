Selfcare API Transactions
=========================
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

### /customers/{idType}/{id}/products
---
##### ***GET***
**Summary:** Find the Customer Products by the Customer Code

**Description:** This resource returns a Inventory of Services (Products) of the Customer by the Client Code

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| idType | path | The Id Type that we want to use, in this case the Client Code of the Subscriber | Yes | integer |
| id | path | Client Code Number of the Subscriber | Yes | integer |
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

### /customers/{idType}/{id}/credits
---
##### ***GET***
**Summary:** Find the Customer Credit Limits by the Customer Code

**Description:** This resource returns data about the Credit Limits (activation dates, accumulated credits and limits) related to the Subscriber by his ClientCode, it accepts the MSISDN as filter.


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| idType | path | The Id Type that we want to use, in this case the Client Code of the Subscriber | Yes | integer |
| id | path | Client Code Number of the Subscriber | Yes | integer |
| msisdn | query | Msisdn of the Subscriber | Yes | integer |
| limit | query | Number of products to be returned | No | integer |
| Authorization | header | Access Token provided by the Token Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [CreditLimitResponse](#creditlimitresponse) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

##### ***PUT***
**Summary:** Set the Customer Credit Limits by the Customer Code

**Description:** This feature allows you set manually the Credit Limits using the Subscriber ClientCode and his MSISDN.


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| idType | path | The Id Type that we want to use, in this case the Client Code of the Subscriber | Yes | integer |
| id | path | Client Code Number of the Subscriber | Yes | integer |
| updateCreditLimits | body | TODO Add description | Yes | [UpdateCreditLimits](#updatecreditlimits) |
| Authorization | header | Access Token provided by the Token Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful transaction |  |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### Models
---

### CreditLimitResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| cumulativeCredit | string |  | No |
| definedCreditLimit | string |  | No |
| lastIncrement | object |  | No |

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

### UpdateCreditLimits  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| changeType | string |  | Yes |
| msisdn | string |  | Yes |
| Deadline | string |  | Yes |
| newManualLimit | string |  | Yes |

### errorBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error | object |  | No |