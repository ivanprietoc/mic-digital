tigo_b2b_co_selfcare_transactions_v2
====================================
This is an api in charge of managing the operations of activating / deactivating basic services and checking the 
status of services to a msisdn for CO Transactions.


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
|read|Customer B2B Transactions|

### /customers/services
---
##### ***POST***
**Summary:** Enables the habilitation or disabling of services to a msisdn.

**Description:** Taking as initial parameter the msisdn of the client allows to perform the habilitation or disablement of services to a msisdn.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| servicesParameters | body | Parameters needed to enable or disable a service | Yes | [servicesParameters](#servicesparameters) |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [servicesAvailable](#servicesavailable) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /customers/{msisdn}/services
---
##### ***GET***
**Summary:** Returns the status of services enabled for a msisdn.

**Description:** Taking as initial parameter the msisdn returns the status of enabled services.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | Is the customer msisdn. | Yes | integer |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [services](#services) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### Models
---

### servicesParameters  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| msisdn | integer |  | No |
| operation | string |  | No |
| serviceId | integer |  | No |

### servicesAvailable  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| code | integer |  | No |
| message | string |  | No |

### services  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| code | integer |  | No |
| description | string |  | No |
| name | string |  | No |
| currency | string |  | No |
| serviceCost | integer |  | No |
| status | string |  | No |

### errorBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error | object |  | No |