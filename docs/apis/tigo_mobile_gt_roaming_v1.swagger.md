tigo_mobile_gt_roaming_v1
=========================
API related to mobile for GT, which is responsible for removing a profile and a subscription using the imsi as the initial parameter.


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
|read|customer imsi|

### /imsis/profile
---
##### ***DELETE***
**Summary:** Removes a profile taking the imsi as the initial parameter

**Description:** Taking the imsi as initial parameter a profile is removed

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| transactions | body | Parameter needed to eliminate the user's profile | Yes | [transactions](#transactions) |
| Authorization | header | Access Token provided by the Token Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [imsiList](#imsilist) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /imsis/subscription
---
##### ***DELETE***
**Summary:** Removes a subscription taking the imsi as the initial parameter

**Description:** Taking the imsi as initial parameter a subscription is removed

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| subscriberGroup | body | Parameter needed to eliminate the user's subscription | Yes | [subscriberGroup](#subscribergroup) |
| Authorization | header | Access Token provided by the Token Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [imsiList](#imsilist) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### Models
---

### transactions  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | integer |  | No |
| imsi | integer |  | No |

### subscriberGroup  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | integer |  | No |
| imsi | integer |  | No |
| packageCode | string |  | No |
| transactionId | integer |  | No |

### imsiList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| message | string |  | No |
| transactionId | integer |  | No |

### errorBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error | object |  | No |