Music Freedom SV API
====================
This is the standard API for Music Freedom related functions, get customer status, subscribe and unsubscribe to the Music Freedom service. 
We use swagger-2.0 specification


**Version:** 1.0.0

**Terms of service:**  
http://swagger.io/terms/

**Contact information:**  
Jose Colman  
https://edge.com.py/  
jose.colman@edge.com.py  

**License:** [MIT](http://github.com/gruntjs/grunt/blob/master/LICENSE-MIT)

### /subscribers/{msisdn}/status/
---
##### ***GET***
**Summary:** Get subscriber status by msisdn

**Description:** Returns a list of provider plans.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | Subscriber MSISDN | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Provider plans associated with provided MSISDN were found | [providerPlans](#providerplans) |
| 400 | Bad Request | [error](#error) |
| 404 | the plans for the specified `MSISDN` was not found | [error](#error) |
| default | unexpected error | [error](#error) |

### /subscribers/{msisdn}
---
##### ***POST***
**Summary:** Subscribe a customer to a provider plan

**Description:** Subscribe a customer to a provider plan

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | Subscriber MSISDN | Yes | string |
| body | body | body | Yes | [SubscribeRequest](#subscriberequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | Subscription was successful | [SubscribeResponse](#subscriberesponse) |
| 400 | Bad Request | [error](#error) |
| 403 | Forbidden. Check `error.message` for details | [error](#error) |
| 404 | Not found | [error](#error) |
| default | unexpected error | [error](#error) |

##### ***DELETE***
**Summary:** Unsubscribe a customer from a provider plan

**Description:** Unsubscribe a customer from a provider plan

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | Subscriber MSISDN | Yes | string |
| body | body | body | Yes | [UnsubscribeRequest](#unsubscriberequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | Subscription was successful | [UnsubscribeResponse](#unsubscriberesponse) |
| 400 | Bad Request | [error](#error) |
| 403 | Forbidden. Check `error.message` for details | [error](#error) |
| 404 | Not found | [error](#error) |
| default | unexpected error | [error](#error) |

### Models
---

### providerPlans  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| providerPlans | array |  |  |

### plan  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| status | string |  | No |
| id | string |  | No |
| description | string |  | No |
| startDate | string |  | No |
| endDate | string |  | No |
| responseCode | string |  | No |
| responseMessage | string |  | No |

### error  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| errorType | string |  | No |
| code | integer |  | No |
| description | string |  | No |
| reason | string |  | No |

### SubscribeRequest  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| providerPlan | string |  | Yes |
| startDate | string |  | No |
| externalTransactionId | string |  | No |

### SubscribeResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| responseCode | string |  | No |
| responseMessage | string |  | No |
| transactionId | string |  | No |

### UnsubscribeRequest  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| providerPlan | string |  | Yes |
| startDate | string |  | No |
| externalTransactionId | string |  | No |

### UnsubscribeResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| responseCode | string |  | No |
| responseMessage | string |  | No |
| transactionId | string |  | No |