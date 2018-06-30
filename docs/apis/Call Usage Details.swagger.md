Call Usage Details
==================
This is the standard API for Call Usage Details for Tigo. 
We use swagger-2.0 specification


**Version:** 1.0.0

**Terms of service:**  
http://swagger.io/terms/

**Contact information:**  
Jose Colman  
https://edge.com.py/  
jose.colman@edge.com.py  

**License:** [MIT](http://github.com/gruntjs/grunt/blob/master/LICENSE-MIT)

### /subscribers/{msisdn}/usage/voice
---
##### ***GET***
**Summary:** Obtain a detailed list of voice call usage.

**Description:** Obtain a detailed list of voice call usage.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | Unique identifier for the customer | Yes | string |
| startDate | query | (optional, ISO8601 datetime) Start date for query period. | No | string |
| endDate | query | (optional, ISO8601 datetime) End Date for query period. | No | string |
| limit | query |  | No | number |
| offset | query |  | No | number |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successfull | [voiceDetailList](#voicedetaillist) |
| 400 | Invalid Parameters | [error](#error) |
| 404 | Not found | [error](#error) |
| 500 | Server Error | [error](#error) |
| default | unexpected error | [error](#error) |

### Models
---

### voiceDetailList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| voiceDetailList | array |  |  |

### voiceDetail  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| targetNumber | string |  | No |
| targetCompany | string |  | No |
| originNumber | string |  | No |
| eventType | string |  | No |
| DateTime | string |  | No |
| eventDuration | number |  | No |
| cost | number |  | No |

### error  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| statusCode | integer |  | No |
| code | string |  | No |
| message | string |  | No |
| developerMessage | string |  | No |