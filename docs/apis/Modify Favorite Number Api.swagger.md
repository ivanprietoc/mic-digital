Modify Favorite Number Api
==========================
This is the standard API for Self Care functions to modify favorite number for Tigo. 
We use swagger-2.0 specification


**Version:** 1.0.0

**Terms of service:**  
http://swagger.io/terms/

**Contact information:**  
Jose Colman  
https://edge.com.py/  
jose.colman@edge.com.py  

**License:** [MIT](http://github.com/gruntjs/grunt/blob/master/LICENSE-MIT)

### /{msisdn}/favoritePlans/{favoritePlan}/favoriteNumbers
---
##### ***PUT***
**Summary:** Modify a favorite number

**Description:** Modify a favorite number

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | Unique identifier for the customer | Yes | string |
| favoritePlan | path | Unique identifier for the favorite plan | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successfull Favorite Number Modification | [success](#success) |
| 400 | Invalid Parameters | [proxyError](#proxyerror) |
| default | unexpected error | [error](#error) |

### Models
---

### success  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| result | string |  | No |
| resultCode | string |  | No |

### error  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| errorType | string |  | No |
| code | integer |  | No |
| description | string |  | No |
| reason | string |  | No |

### proxyError  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| statusCode | integer |  | No |
| message | string |  | No |
| developerMessage | string |  | No |