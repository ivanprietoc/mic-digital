tigo_sv_selfcare_crm_v1
=======================
This is a standard Api for SV B2B Selfcare 


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
|read|Customer CRM|

### /customers/calls/details
---
##### ***POST***
**Summary:** Find the detail of the calls taking the msisdn as the initial parameter.

**Description:** Returns the detail of the calls made from the msisdn.

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
| msisdn | integer | Msisdn of the customers | No |
| startDate | dateTime | Initial date of the query | No |
| endDate | dateTime | Final date of the query | No |
| limit | integer | Amount of values to show | No |
| offset | integer | Initial value of result to show | No |

### details  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| calledNumber | integer |  | No |
| callingNumber | integer |  | No |
| chargedAmount | integer |  | No |
| duration | integer |  | No |
| endDate | dateTime |  | No |
| roaming | string |  | No |
| serviceType | string |  | No |
| startDate | dateTime |  | No |

### errorBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error | object |  | No |