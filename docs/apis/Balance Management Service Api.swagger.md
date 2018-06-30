Balance Management Service Api
==============================
This is the standard API for Balance Management for Tigo. 
We use swagger-2.0 specification


**Version:** 1.0.0

**Terms of service:**  
http://swagger.io/terms/

**Contact information:**  
Jose Colman  
https://edge.com.py/  
jose.colman@edge.com.py  

**License:** [MIT](http://github.com/gruntjs/grunt/blob/master/LICENSE-MIT)

### /{creditMsisdn}/transfer
---
##### ***POST***
**Summary:** Transfer credit balance from a debtMsisdn to a creditMsisdn

**Description:** Transfer credit balance from a debtMsisdn to a creditMsisdn

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| creditMsisdn | path | Unique identifier for the customer | Yes | string |
| body | body | body | Yes | [request](#request) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successfull Transfer | [success](#success) |
| 400 | Invalid Parameters | [error](#error) |
| 404 | Not found | [error](#error) |
| 500 | Server Error | [error](#error) |
| default | unexpected error | [error](#error) |

### /{creditMsisdn}/topup
---
##### ***POST***
**Summary:** Buy credit for the creditMsisdn balance

**Description:** Buy credit for the creditMsisdn balance

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| creditMsisdn | path | Unique identifier for the customer | Yes | string |
| body | body | body | Yes | [request](#request) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successfull Transfer | [success](#success) |
| 400 | Invalid Parameters | [error](#error) |
| 404 | Not found | [error](#error) |
| 500 | Server Error | [error](#error) |
| default | unexpected error | [error](#error) |

### Models
---

### success  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| estado | string |  | No |

### error  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| statusCode | integer |  | No |
| message | string |  | No |
| developerMessage | string |  | No |

### request  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| debtAccount | string |  | No |
| amount | string |  | No |
| action | string |  | No |