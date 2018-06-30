tigo_crm_co_digitalDocuments_v2
===============================
This is an API that allows you to obtain the url of the digital document (Contract) for massive clients as well as for corporate clients.


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

### /customers/{idType}/{id}/documents
---
##### ***GET***
**Summary:** Returns the url of the digital document for massive and corporate clients.

**Description:** Taking as initial parameter the client id returns the url of the digital document for massive and corporate clients.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| idType | path | Type of document. | Yes | string |
| id | path | Is the document number. | Yes | integer |
| movil | query | Msisdn to consult. | Yes | integer |
| segment | query | Segment to consult can be one of the CORPORATE / MASIVE values. | No | string |
| document | query | Corresponds to the id of the document found in computer. | No | string |
| additional | query | Additional parameters. | No | string |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [documents](#documents) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### Models
---

### documents  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| url | string | Url of the digital document (Contract) found on the Computec platform in pdf format. | No |

### errorBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error | object |  | No |