tigo_home_sv_billing_v1
=======================
This is a standard Api for SV Home Billing


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
|read|bill detail|

### /bills/{billingId}/accounts/{accountId}
---
##### ***GET***
**Summary:** Get the Billing Payment Details by the Billing Id and the Account Id

**Description:** Returns the detail of the Payment of an Invoice taking as parameters the Invoice Number and the Account ID to which it belongs.


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| billingId | path | Billing Id (aka Invoice Number) | Yes | integer |
| accountId | path | The Account Id to which the Invoice belongs | Yes | integer |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response. | [details](#details) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource. | [errorBody](#errorbody) |

### Models
---

### details  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| bankName | string | Payment channel | No |
| paymentAmount | number | Amount of the invoice | No |
| paymentDate | string | Payment date of the invoice | No |
| paymentMethod | number | Payment method | No |

### errorBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error | object |  | No |