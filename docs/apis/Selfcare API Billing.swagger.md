Selfcare API Billing
====================
This is the Standard API related to Billing in Version 2


**Version:** 1.0.0

**Terms of service:**  
http://swagger.io/terms/

**Contact information:**  
Carlos Carvallo  
https://edge.com.py  
carlos.carvallo@edge.com.py  

**License:** [MIT](http://github.com/gruntjs/grunt/blob/master/LICENSE-MIT)

### Security
---
**application**  

|oauth2|*OAuth 2.0*|
|---|---|
|Token URL|https://test.api.tigo.com/oauth/client_credential/accesstoken?grant_type=client_credentials|
|Flow|application|
|**Scopes**||
|read|allows read bills collection|

### /customers/{idType}/{id}/bills
---
##### ***GET***
**Summary:** Find the Customers Bills Collection by the Client Code

**Description:** This resource returns a Bills Collection

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | The Identifier itself related to the Type (the Local Client Code in this case) | Yes | number |
| idType | path | Identification Type (related to the Local Client Code) | Yes | string |
| pageInit | query | Initial number for pagination | No | integer |
| quantity | query | Number of bills to be returned | No | integer |
| start | query | Start date | No | integer |
| end | query | End date | No | integer |
| contractNumber | query | Contract Number Identification | No | integer |
| status | query | TODO Add description | No | string |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [BillCollection](#billcollection) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /customers/{idType}/{id}/bills/groups/{groupId}
---
##### ***GET***
**Summary:** Find the Customers Bills Collection by the Client Code

**Description:** This resource returns a Bills Collection

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | The Identifier itself related to the Type (the Local Client Code in this case) | Yes | number |
| idType | path | Identification Type (related to the Local Client Code) | Yes | string |
| groupId | path | TODO Add description | Yes | string |
| pageInit | query | Initial number for pagination | No | integer |
| quantity | query | Number of bills to be returned | No | integer |
| start | query | Start date | No | integer |
| end | query | End date | No | integer |
| contractNumber | query | Contract Number Identification | No | integer |
| status | query | TODO Add description | No | string |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [BillCollection](#billcollection) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /customers/{msisdn}/profile
---
##### ***GET***
**Summary:** Get Client Profile

**Description:** Return a Client Profile based on his MSISDN


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | MSISDN of the Client | Yes | number |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Succesful response | [Profile](#profile) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unathorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /customers/{idType}/{id}/bills/groups
---
##### ***POST***
**Summary:** Create a Billing Group based on the Code of the Client

**Description:** Create a Billing Group based on the Code of the Client


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | The Identifier itself related to the Type (the Local Client Code in this case) | Yes | number |
| idType | path | Identification Type (related to the Local Client Code) | Yes | string |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Succesful response | [BillingGroupRequest](#billinggrouprequest) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unathorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

##### ***PUT***
**Summary:** Update a Billing Group based on the Code of the Client

**Description:** Update a Billing Group based on the Code of the Client


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | The Identifier itself related to the Type (the Local Client Code in this case) | Yes | number |
| idType | path | Identification Type (related to the Local Client Code) | Yes | string |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Succesful response | [BillingGroupRequest](#billinggrouprequest) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unathorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

##### ***DELETE***
**Summary:** Delete a Billing Group based on the Code of the Client

**Description:** Delete a Billing Group based on the Code of the Client


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | The Identifier itself related to the Type (the Local Client Code in this case) | Yes | number |
| idType | path | Identification Type (related to the Local Client Code) | Yes | string |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Succesful response | [BillingGroupRequest](#billinggrouprequest) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unathorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### Models
---

### Profile  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| ContractProfileType | object |  | No |

### BillCollection  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| invoice | [ object ] |  | No |

### BillingGroupRequest  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| address | string |  | No |
| groupId | string |  | No |

### errorBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error | object |  | No |