tigo_b2b_bo_selfcare_crm_v2
===========================
API related to CRM for Bolivia B2B exposes a collection of contracts with the amount of lines and products included in the contract.


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
|read|customer contracts|

### /customer/{idType}/{id}/services
---
##### ***GET***
**Summary:** Get Customer Contracts by the Customer Identification

**Description:** This resource returns a collection of contracts with the number of lines and / or products included in the contract taking as initial parameter the Customer Identification.


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| idType | path | Customer Id Type | Yes | integer |
| id | path | Client's Document Number | Yes | integer |
| Authorization | header | Access Token provided by the Token Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [contracts](#contracts) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### Models
---

### contracts  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | integer | Contract number | No |
| countMsisdn | integer | Number of lines per contract | No |

### errorBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error | object |  | No |