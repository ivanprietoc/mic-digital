tigo_mobile_bo_crm_v1
=====================
This is an api that is responsible for prepaid postpaid service activations and migration from prepaid to postpaid service to BO CRM


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

### /lines/{msisdn}/postpaid/activation
---
##### ***POST***
**Summary:** Performs the activation of the postpaid service taking as initial parameters the customer data.

**Description:** Taking as initial parameters the data of the client performs the activation of the postpaid service.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | Is the msisdn number. | Yes | integer |
| postpaid | body | Parameters necessary to perform the activation of the postpaid service and migration from the prepaid service to postpaid | Yes | [postpaid](#postpaid) |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [activationList](#activationlist) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /lines/{msisdn}/prepaid/activation
---
##### ***POST***
**Summary:** Performs the activation of the prepaid service taking as initial parameters the customer data.

**Description:** Taking as initial parameters the data of the client performs the activation of the prepaid service.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | Is the msisdn number. | Yes | integer |
| prepaid | body | Parameters necessary to perform the activation of the prepaid service | Yes | [prepaid](#prepaid) |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [activationList](#activationlist) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /lines/{msisdn}/prepaid/migration
---
##### ***POST***
**Summary:** Performs the migration of the prepaid service to postpaid taking as initial parameters the customer data.

**Description:** Taking as initial parameters the data of the client performs the migration of the prepaid service to postpaid.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | Is the msisdn number. | Yes | integer |
| postpaid | body | Parameters necessary to perform the activation of the postpaid service and migration from the prepaid service to postpaid | Yes | [postpaid](#postpaid) |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [migrationList](#migrationlist) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### Models
---

### postpaid  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| vendorId | integer |  | No |
| vendorRegister | integer |  | No |
| eh | integer |  | No |
| operationId | string |  | No |
| documentType | integer |  | No |
| documentNumber | integer |  | No |
| name | string |  | No |
| surname | string |  | No |
| civilStatus | string |  | No |
| birthDate | date |  | No |
| gender | string |  | No |
| saleType | integer |  | No |
| applyPortability | integer |  | No |
| planId | integer |  | No |
| branchOffice | integer |  | No |
| nationality | string |  | No |
| location | integer |  | No |
| iccid | integer |  | No |
| supportInside | string |  | No |
| amountIncome | integer |  | No |
| backupDate | date |  | No |

### prepaid  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| vendorId | integer |  | No |
| vendorRegister | integer |  | No |
| eh | integer |  | No |
| operationId | string |  | No |
| documentType | integer |  | No |
| documentNumber | integer |  | No |
| name | string |  | No |
| surname | string |  | No |
| civilStatus | string |  | No |
| birthDate | date |  | No |
| gender | string |  | No |
| saleType | integer |  | No |
| applyPortability | integer |  | No |
| planId | integer |  | No |
| branchOffice | integer |  | No |
| nationality | string |  | No |
| location | integer |  | No |
| iccid | integer |  | No |

### activationList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| correlationID | integer |  | No |
| message | string |  | No |

### migrationList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| correlationID | integer |  | No |
| message | string |  | No |
| referenceId | string |  | No |

### errorBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error | object |  | No |