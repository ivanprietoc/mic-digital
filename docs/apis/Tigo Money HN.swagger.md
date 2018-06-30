Tigo Money HN
=============
Subscriber operations

**Version:** 1.0.0

**Contact information:**  
Miguel Godoy  
miguel.godoy@edge.com.py  

### /subscribers/{msisdn}/know-your-customer
---
##### ***GET***
**Description:** KYC (Know Your Customer) subscriber registration complementary API. Will allow us to validate a set of parameters for a susbcriber before proceeding to register.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | Client MSISDN | Yes | string |
| id_number | query | Id Number | Yes | integer |
| birthdate | query | Date of birth YYYY-MM-DD | Yes | date |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | ok |  |
| 400 | bad request | [ErrorResponse](#errorresponse) |
| 404 | not found | [ErrorResponse](#errorresponse) |

### /subscribers/login
---
##### ***POST***
**Description:** API to authenticate subscribers

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| subscriber | body | Tigo Money PIN | Yes |  |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Ok |  |
| 400 | Bad Request | [ErrorResponse](#errorresponse) |
| 403 | Forbidden | [ErrorResponse](#errorresponse) |
| 404 | Not Found | [ErrorResponse](#errorresponse) |

### /subscribers/{msisdn}/pins
---
##### ***GET***
**Description:** API to get Tigo Money subscriber pin status

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | Subscriber MSISDN | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Ok |  |
| 400 | Bad Request | [ErrorResponse](#errorresponse) |
| 404 | Not Found | [ErrorResponse](#errorresponse) |

##### ***PUT***
**Description:** API to change Tigo Money subscriber pin

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | Subscriber MSISDN | Yes | string |
| pin_data | body | Tigo Money subscriber pin information | Yes |  |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | ok |  |
| 400 | bad request | [ErrorResponse](#errorresponse) |
| 404 | not found | [ErrorResponse](#errorresponse) |

### /subscribers/{msisdn}/send-money
---
##### ***POST***
**Description:** API to send Tigo Money

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | Subscriber MSISDN | Yes | string |
| Send money | body | transaction data | No |  |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | Created | [SuccessTransactionResponse](#successtransactionresponse) |
| 400 | Bad Request | [ErrorResponse](#errorresponse) |
| 403 | Forbidden | [ErrorResponse](#errorresponse) |
| 404 | Not Found | [ErrorResponse](#errorresponse) |

### /subscribers/{msisdn}/transactions
---
##### ***POST***
**Description:** API to get a list of transactions made by a Tigo Money subscriber

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | Subscriber MSISDN | Yes | string |
| transactions | body | transaction data | No |  |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | ok |  |
| 400 | bad request | [ErrorResponse](#errorresponse) |
| 404 | not found | [ErrorResponse](#errorresponse) |

### /topups
---
##### ***GET***
**Description:** API to get the list of air time top up amounts

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| channel_code | query | channel code | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Ok |  |
| 400 | Bad Request | [ErrorResponse](#errorresponse) |
| 404 | Not Found | [ErrorResponse](#errorresponse) |

### /subscribers/{msisdn}/topups
---
##### ***POST***
**Description:** API to reload airtime to a prepaid account.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | Subscriber MSISDN | Yes | string |
| Top Up | body | transaction data | No |  |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | created | [SuccessTransactionResponse](#successtransactionresponse) |
| 400 | bad request | [ErrorResponse](#errorresponse) |
| 404 | not found | [ErrorResponse](#errorresponse) |

### /agents
---
##### ***GET***
**Description:** API to obtain nearest Tigo Money agents.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| lat | query | subscriber latitude | Yes | float |
| long | query | subscriber longitude | Yes | float |
| limit | query | max results to return | No | integer |
| type | query | type of agent | No | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Ok |  |
| 400 | Bad Request | [ErrorResponse](#errorresponse) |
| 404 | Not Found | [ErrorResponse](#errorresponse) |

### /billers
---
##### ***GET***
**Description:** API to obtain available billers integrated with Tigo Money.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| category_code | query | Biller category Id (default 0) | Yes | integer |
| channel_code | query |  | No | integer |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Ok |  |
| 400 | Bad Request | [ErrorResponse](#errorresponse) |
| 404 | Not Found | [ErrorResponse](#errorresponse) |

### /subscribers/{msisdn}/billers/{biller_id}/bills
---
##### ***POST***
**Description:** API to obtain bill/s for a specific company given a reference number

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | Subscriber MSISDN | Yes | string |
| biller_id | path | Biller number | Yes | string |
| data | body |  | No |  |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Ok |  |
| 400 | Bad Request | [ErrorResponse](#errorresponse) |
| 404 | Not Found | [ErrorResponse](#errorresponse) |

### /subscribers/{msisdn}/billers/{biller_id}/bills/{bill_id}
---
##### ***POST***
**Description:** API to pay a bill

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | Subscriber MSISDN | Yes | string |
| biller_id | path | Company Id | Yes | string |
| bill_id | path | Biller Id | Yes | string |
| bill | body | Bill payment data | Yes |  |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | Created |  |
| 400 | Bad Request | [ErrorResponse](#errorresponse) |
| 404 | Not Found | [ErrorResponse](#errorresponse) |

### /subscribers/{msisdn}/fees
---
##### ***GET***
**Description:** Get fees

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | The internacional cellphone number | Yes | string |
| transaction_type | query | transaction type | Yes | string |
| amount | query | fees amount | Yes | float |
| currency | query | type of currency | Yes | string |
| target | query | target's msisdn | No | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Ok |  |
| 400 | Bad Request | [ErrorResponse](#errorresponse) |
| 404 | Not Found | [ErrorResponse](#errorresponse) |

### /subscribers/{msisdn}/fees/{biller_name}
---
##### ***POST***
**Description:** Get fees

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | The internacional cellphone number | Yes | string |
| biller_name | path | set biller name | Yes | string |
| transaction | body | transaction body | Yes |  |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | Created |  |
| 400 | Bad Request | [ErrorResponse](#errorresponse) |
| 404 | Not Found | [ErrorResponse](#errorresponse) |

### /subscribers/{msisdn}/balances
---
##### ***POST***
**Description:** Get balance

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | The internacional cellphone number | Yes | string |
| transaction | body | transaction body | Yes |  |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Ok |  |
| 400 | Bad Request | [ErrorResponse](#errorresponse) |
| 404 | Not Found | [ErrorResponse](#errorresponse) |

### Models
---

### Subscriber  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id_number | integer |  | Yes |
| birthdate | date | date of birthday YYYY-MM-DD | Yes |
| pin | string |  | Yes |
| pin_confirm | string |  | Yes |

### SubscriberDetails  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | Yes |
| firstname | string |  | Yes |
| lastname | string |  | Yes |
| primary_id_type | string |  | Yes |
| birth_date | date | date of birthday YYYY-MM-DD | Yes |
| address | string |  | Yes |
| msisdn | string |  | Yes |
| primary_id_number | string |  | Yes |
| email_address | string |  | No |
| language | integer |  | Yes |
| status | string |  | Yes |
| user_type | string |  | Yes |
| created_at | string (datetime) | date was created YYYY-MM-DD HH:MM:YY | Yes |
| category | string |  | Yes |

### StatusResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| status_code | string |  | Yes |
| status_message | string |  | Yes |

### TransactionDetail  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| type_transaction | string |  | Yes |
| description | string |  | Yes |
| detail | string |  | Yes |
| amount | float |  | Yes |
| currency | string | type of currency | No |
| charge | integer |  | Yes |
| reference | string |  | Yes |
| processed_at | date | date processed YYYY-MM-DD | Yes |
| entry_type | string |  | Yes |

### SubscriberResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id_number | integer |  | Yes |
| firstname | string |  | Yes |
| lastname | string |  | Yes |
| birthdate | date | date of birthdate YYYY-MM-DD | Yes |

### ErrorResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error | object |  | Yes |

### SuccessTransactionResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| transaction_id | string |  | Yes |

### AgentDetail  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| latitude | float |  | No |
| longitude | float |  | No |
| type | string |  | No |
| business_unit | string |  | No |
| name_pos | string |  | No |
| contact_pos | string |  | No |
| contact_number | string |  | No |
| description | string |  | No |
| status | string |  | No |
| neighborhood | string |  | No |
| pos_code | string |  | No |
| distance | string (float) |  | No |
| business_hours | string |  | No |
| balance_amount | integer |  | No |
| currency_amount | string |  | No |

### ReferenceNumber  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| number | string |  | Yes |
| max_length | number |  | Yes |
| min_length | number |  | Yes |
| type | string |  | Yes |

### Bill  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | No |
| code | string |  | No |
| shortname | string |  | No |
| fullname | string |  | No |
| category_code | integer |  | No |
| category_name | string |  | No |
| partial_payment | boolean |  | No |
| view_bill | boolean |  | No |
| reference_numbers | [ [ReferenceNumber](#referencenumber) ] |  | No |

### BillPayment  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| subscriber | object |  | Yes |
| bill | object |  | Yes |

### Fee  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| type | string |  | No |
| fee | float |  | No |
| units | string |  | No |
| description | string |  | No |
| conditions | string |  | No |
| additional_results | string |  | No |

### Balance  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| transaction_id | string |  | Yes |
| wallet | object |  | Yes |