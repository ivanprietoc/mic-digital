Tigo Mobile PY Up-Selling Information API
=========================================
Provides status information of a Tigo Mobile Customer about its Mobile services, Balances and Data Quota

**Version:** 1.0

**Contact information:**  
Jorge Levera  
jorge.levera@millicom.com  

### Security
---
**api_key**  

|apiKey|*API Key*|
|---|---|
|Name|Bearer|
|In|header|

### /subscribers/{msisdn}/quota
---
##### ***GET***
**Description:** returns Tigo Subscriber's current Data Plan or Data Package information.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | Tigo subscriber MSISDN | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Ok | [mobileInternetQuota](#mobileinternetquota) |
| 400 | Bad Request | [BadRequestErrorResponse](#badrequesterrorresponse) |
| 401 | Unauthorized | [UnauthorizedErrorResponse](#unauthorizederrorresponse) |
| 403 | Forbidden | [ForbiddenErrorResponse](#forbiddenerrorresponse) |
| 504 | Gateway Timeout | [TimeoutErrorResponse](#timeouterrorresponse) |

**Security**

| Security Schema | Scopes |
| --- | --- |
| api_key | |

### Models
---

### quota  

Tigo subscriber quota information

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| availableQuota | string |  | Yes |
| effectiveDate | string |  | Yes |
| expirationDate | string |  | Yes |
| description | string |  | Yes |

### mobileInternetQuota  

Tigo Subscriber's current Data Plan or Data Package information

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| accountType | string | Type of Account | Yes |
| clientType | string | Type of Customer. A more verbose description of accountType | Yes |
| totalAvailableQuota | string |  | Yes |
| additionalResults | string |  | Yes |
| accumulatedQuotas | [ [quota](#quota) ] | (Array of JSON objects, optional) Not Always present information about Subscriber's quotas | Yes |
| queuedPacks | [ [queuedPack](#queuedpack) ] | (Array of JSON objects, optional) Not Always present information about Subscriber's queued Data Packages which are purchased but not yet beign consumed. Maybe more than one | Yes |
| currentPasses | [ [currentPass](#currentpass) ] | A list of currentPasses | Yes |

### currentPass  

(Not Always present) information about Subscriber's current Pass that can be purchased on top of Data Plans and Data packages and modify the normal behavior of the Offer.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| description | string | Name of the Data package | Yes |
| quota | string | how many Mbytes or Gbytes are granted by this Data Package (not to confuse with availableQuota). | Yes |
| dpiCode | string | Identifier of Plan in the DPI/PCRF system | Yes |
| dpiQuotaName | string | Identifier of Quota name in DPI/PCRF system. | Yes |
| expirationDate | string | (ISO date) Local date-time When the Data pack is going to expire | Yes |
| availableQuota | string | Amount of Mbytes or Gbytes left in the Data Pack. This will be expired at expirationDate | Yes |
| purchaseDate | string | Local date-time when the Data pack was purchased | Yes |
| duration | integer | Validity of the Data Pack or Data pass in seconds | Yes |
| mundo2 | boolean | (string) true or false if this Data Pack is elegible to "Mundo2" subscribers | Yes |
| priority | integer | Consumption priority used to determine in which order Data packs are consumed | Yes |

### queuedPack  

(Not Always present) information about Subscriber's queued Data Packages which are purchased but not yet being consumed. Maybe more than one.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| description | string | Name of the Data package | Yes |
| quota | string | how many Mbytes or Gbytes are granted by this Data Package (not to confuse with availableQuota). | Yes |
| dpiCode | string | Identifier of Plan in the DPI/PCRF system | Yes |
| dpiQuotaName | string | Identifier of Quota name in DPI/PCRF system. | Yes |
| availableQuota | string | Amount of Mbytes or Gbytes left in the Data Pack. This will be expired at expirationDate | Yes |
| purchaseDate | string | Local date-time when the Data pack was purchased | Yes |
| duration | integer | Validity of the Data Pack or Data pass in seconds | Yes |
| mundo2 | boolean | (string) true or false if this Data Pack is elegible to "Mundo2" subscribers | Yes |
| priority | integer | Consumption priority used to determine in which order Data packs are consumed | Yes |

### UnauthorizedErrorResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error | object |  | Yes |

### ForbiddenErrorResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error | object |  | Yes |

### TimeoutErrorResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error | object |  | Yes |

### BadRequestErrorResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error | object |  | Yes |