tigo_b2b_hn_billing_v2
======================
Api that is in charge of making the downloads of the invoices in pdf format.


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
|read|customer bills|

### /customers/{msisdn}/invoices
---
##### ***POST***
**Summary:** Allows you to download invoices in pdf format

**Description:** This resource allows you to download the billing summary in pdf format

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | Customer Msisdn | Yes | string |
| invoiceNumber | query | Invoice Number Identification | Yes | string |
| invoiceDate | query | Date of issue of the invoice | Yes | string |
| type | query | Type of invoice to be returned | Yes | string |
| typeResult | query | Format of the invoice to be returned | Yes | string |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [invoice](#invoice) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### Models
---

### invoice  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| status | string | Result of the execution of ws | No |
| message | string | Shows the message that accompanies the status of the service query | No |
| invoice | string | Result of the invoice returned in B64 format | No |

### errorBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error | object |  | No |