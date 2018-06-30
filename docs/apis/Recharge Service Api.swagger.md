Recharge Service Api
====================
This is the standard API for the Recharge Service for Tigo. 
We use swagger-2.0 specification


**Version:** 1.0.0

**Terms of service:**  
http://swagger.io/terms/

**Contact information:**  
Jose Colman  
https://edge.com.py/  
jose.colman@edge.com.py  

**License:** [MIT](http://github.com/gruntjs/grunt/blob/master/LICENSE-MIT)

### /{msisdn}
---
##### ***PUT***
**Summary:** Recharge given msisdn account

**Description:** Recharge given msisdn account

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | Unique identifier for the customer | Yes | string |
| body | body | body | Yes | [rechargeRequest](#rechargerequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successfull Recharge | [success](#success) |
| 400 | Invalid Parameters | [proxyError](#proxyerror) |
| 404 | Not found | [error](#error) |
| default | unexpected error | [error](#error) |

### Models
---

### success  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| code | string |  | No |
| msisdn | string |  | No |
| bonusBalance | [bonusBalance](#bonusbalance) |  | No |
| bonusCredit | [bonusCredit](#bonuscredit) |  | No |
| realBalance | [realBalance](#realbalance) |  | No |
| realCredit | [realCredit](#realcredit) |  | No |

### error  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| code | string |  | No |
| description | string |  | No |
| severity | string |  | No |

### proxyError  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| statusCode | integer |  | No |
| message | string |  | No |
| developerMessage | string |  | No |

### rechargeRequest  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| information | string |  | No |
| transactionId | string |  | No |
| transactionType | string |  | No |
| bonusCredit | [bonusCredit](#bonuscredit) |  | No |
| realCredit | [realCredit](#realcredit) |  | No |

### bonusBalance  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| amount | string |  | No |
| currencyId | string |  | No |
| currencyName | string |  | No |

### bonusCredit  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| amount | string |  | No |
| currencyId | string |  | No |
| currencyName | string |  | No |

### realBalance  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| amount | string |  | No |
| currencyId | string |  | No |
| currencyName | string |  | No |

### realCredit  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| amount | string |  | No |
| currencyId | string |  | No |
| currencyName | string |  | No |