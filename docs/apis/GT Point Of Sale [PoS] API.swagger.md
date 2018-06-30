GT Point Of Sale [PoS] API
==========================
Basic PoS activities

**Version:** 1.0.0

### /login
---
##### ***POST***
**Description:** Validate point of sale credentials

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| Authorization | header | API access token | Yes | string |
| body | body |  | Yes | [RequestLogin](#requestlogin) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Ok | [ResponseLogin](#responselogin) |
| 401 | Unauthorized | [UnauthorizedResponse](#unauthorizedresponse) |
| 403 | Forbidden | [ForbiddenResponse](#forbiddenresponse) |
| 404 | Forbidden | [NotFoundResponse](#notfoundresponse) |

### /credentials
---
##### ***PUT***
**Description:** Change point of sale password

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| Authorization | header | API access token | Yes | string |
| body | body |  | Yes | [CredentialsRequest](#credentialsrequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Ok | object |
| 401 | Unauthorized | [UnauthorizedResponse](#unauthorizedresponse) |
| 403 | Forbidden | [ForbiddenResponse](#forbiddenresponse) |
| 404 | Forbidden | [NotFoundResponse](#notfoundresponse) |

### /retailers/{retailerMsisdn}/balance
---
##### ***POST***
**Description:** Get PoS available balance

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| Authorization | header | API access token | Yes | string |
| retailerMsisdn | path | Point of sale MSISDN | Yes | string |
| body | body |  | Yes | [RequestGetBalance](#requestgetbalance) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [ResponseGetBalance](#responsegetbalance) |
| 403 | Forbidden | [ForbiddenResponse](#forbiddenresponse) |

### /topups
---
##### ***GET***
**Description:** Get available air time top up amounts

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| Authorization | header | API access token | Yes | string |
| subscriberMsisdn | query | Tigo subscriber MSISDN | No | string |
| retailerMsisdn | query | Point of sale MSISDN | No | string |
| posId | query | Point of sale ID in DMS platform | No | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Ok | [TopUpResponse](#topupresponse) |
| 403 | Forbidden | [ForbiddenResponse](#forbiddenresponse) |

##### ***POST***
**Description:** Sell airtime top up to Tigo subscriber

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| Authorization | header | API access token | Yes | string |
| body | body |  | Yes | [TopUpRequest](#topuprequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Ok | [TopUpResponsePost](#topupresponsepost) |
| 403 | Forbidden | [ForbiddenResponse](#forbiddenresponse) |

### /retailers/{retailerMsisdn}/subscribers/{clientMsisdn}/products
---
##### ***GET***
**Description:** Get available products for sale

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| Authorization | header | API access token | Yes | string |
| clientMsisdn | path | Tigo susbcribers MSISDN | Yes | string |
| retailerMsisdn | path | Point of sale MSISDN | Yes | string |
| posId | query | Point of sale ID in DMS platform | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Ok | [ResponseProducts](#responseproducts) |
| 403 | Forbidden | [ForbiddenResponse](#forbiddenresponse) |

### /retailers/{retailerMsisdn}/subscribers/{clientMsisdn}/products/{productId}
---
##### ***POST***
**Description:** Sell a product to a Tigo subscriber

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| Authorization | header | API access token | Yes | string |
| clientMsisdn | path | Tigo subscriber MSISDN | Yes | string |
| retailerMsisdn | path | Point of sale MSISDN | Yes | string |
| productId | path | Product id returned by GET /products | Yes | string |
| body | body | Sell product request body | Yes | [RequestAcquireProduct](#requestacquireproduct) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK |  |
| 403 | Forbbiden | [ForbiddenResponse](#forbiddenresponse) |

### Models
---

### ResponseProducts  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| products | [  ] |  | No |

### RequestAcquireProduct  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| pin | string | Retailer pin | No |
| amount | string | Product price. Mapped to price returned by GET /products | No |
| referenceNumber | string | Unique reference id for traceability | No |

### ResponseLogin  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| status | string |  | No |
| msisdn | string |  | No |
| role | string |  | No |
| distributor | string |  | No |
| seller | string |  | No |

### TopUpResponsePost  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| status | string |  | No |
| transactionId | string |  | No |

### TopUpRequest  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| retailerMsisdn | string | Point of sale MSISDN | No |
| clientMsisdn | string | Tigo subscriber MSISDN | No |
| retailerPin | string | Point of sale Pin | No |
| amount | number | Air time top up amount | No |
| currency | string | Quetzal | No |
| referenceNumber | string | Transaction reference Id | No |

### TopUpResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| amounts | [  ] |  | No |

### RequestLogin  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| username | string |  | No |
| password | string |  | No |

### NotFoundResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| statusCode | number |  | No |
| code | string |  | No |
| message | string |  | No |
| developerMessage | string |  | No |

### ForbiddenResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| statusCode | number |  | No |
| code | string |  | No |
| message | string |  | No |
| developerMessage | string |  | No |

### UnauthorizedResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| statusCode | number |  | No |
| code | string |  | No |
| message | string |  | No |
| developerMessage | string |  | No |

### CredentialsRequest  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| username | string |  | No |
| oldPassword | string |  | No |
| newPassword | string |  | No |

### ResponseGetBalance  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| balances | [  ] |  | No |

### RequestGetBalance  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| pin | string |  | No |