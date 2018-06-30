Insurance API
=============
This is the standard API for Self Care functions related to insurance services for Tigo. 
We use swagger-2.0 specification


**Version:** 1.0.0

**Terms of service:**  
http://swagger.io/terms/

**Contact information:**  
Jose Colman  
https://edge.com.py/  
jose.colman@edge.com.py  

**License:** [MIT](http://github.com/gruntjs/grunt/blob/master/LICENSE-MIT)

### /insurances/{msisdn}
---
##### ***GET***
**Summary:** Get a list of insurances acquired

**Description:** Get a detailed list of insurances acquired by the user based on his msisdn

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | Unique identifier for the customer | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested Insurance list was found | [insuranceList](#insurancelist) |
| 400 | Invalid Parameters | [proxyError](#proxyerror) |
| default | unexpected error | [error](#error) |

### Models
---

### insuranceList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| insuranceList | array |  |  |

### insurance  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| model | string |  | No |
| insuranceType | string |  | No |
| allowedClaims | string |  | No |
| incurredClaims | number |  | No |
| insurancePremium | string |  | No |

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