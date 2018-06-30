tigo_b2b_gt_selfcare_crm_v2
===========================
This is a standard Api for GT B2B Selfcare CRM

**Version:** 2.0.0

**Terms of service:**  
http://swagger.io/terms/

**Contact information:**  
Andrea Forneron  
https://edge.com.py  
andrea.forneron@edge.com.py  

**License:** [MIT](http://github.com/gruntjs/grunt/blob/master/LICENSE-MIT)

### Security
---
**application**  

|oauth2|*OAuth 2.0*|
|---|---|
|Token URL|https://test.api.tigo.com/oauth/client_credential/accesstoken?grant_type=client_credentials|
|Flow|application|
|**Scopes**||
|read|Customer Selfcare CRM|

### /customers/calls/details
---
##### ***POST***
**Summary:** Find the detail of the calls taking the msisdn as the initial parameter

**Description:** Returns the detail of the calls made from the msisdn

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| callsDetails | body | List of necessary parameters to obtain the detail of the calls  | Yes | [callsList](#callslist) |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [details](#details) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### Models
---

### callsList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| msisdn | integer | List of msisdn | No |
| startDate | string | Initial date of the query | No |
| endDate | string | Final date of the query | No |
| email | string | Mail where the information will be sent | No |
| user | string | User data | No |

### details  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| message | string | Backend response message | No |

### errorBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error | object |  | No |