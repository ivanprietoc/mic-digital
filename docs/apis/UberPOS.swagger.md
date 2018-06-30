UberPOS
=======
UberPOS API Methods

**Version:** 0.1.alpha

### /uberpos/v1/{country}/agents
---
##### ***POST***
**Summary:** create new agent

**Description:** add a new Uber POS agent to the backend. verify the `canOperate`  flag on the response to check if the agent is immediately  authorized and ready to start operating or not.


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| country | path | country | Yes | string |
| body | body |  | No | [addUberPOSAgentRequestBody](#adduberposagentrequestbody) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Ok, the agent was successfully added. | [addUberPOSAgentResponseBody](#adduberposagentresponsebody) |
| 403 | Forbidden. Usually because of an invalid request.  Check `error.message` for details  | [errorBody](#errorbody) |
| 404 | the specified `msisdn` does not exist in the country | [errorBody](#errorbody) |

### /agents/{msisdn}
---
##### ***GET***
**Summary:** get agent

**Description:** return information about an existing UberPOS. If the msisdn argument is inexistent or does not belong to an UberPOS, the method will return 404 (NOT FOUND)
            


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | the msisdn of the agent, including the country prefix.  | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Ok. | [getUberPOSAgentResponseBody](#getuberposagentresponsebody) |
| 403 | Forbidden. Usually because of an invalid request.  Check `error.message` for details  | [errorBody](#errorbody) |
| 404 | the specified `msisdn` does not exist or is not an UberPOS Agent  | [errorBody](#errorbody) |

##### ***PUT***
**Summary:** activate agent

**Description:** this call executes (if any) any procedures on the backend to activate an agent that was previously created using the  method `create new agent`
if any prerequisite is not met, the method will return a 403 (FORBIDDEN) response and the body will contain an explanation of what is required to proceed with the activation. Additionally to the standard error body, the `failedConditions` object will contain one or more messages from the country with instructions on how to proceed.


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | the msisdn of the agent | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 204 | Ok. |  |
| 403 | Forbidden. Usually because of an invalid request.  Check `error.message` for details  | [errorBodyActivateUberPOSAgent](#errorbodyactivateuberposagent) |
| 404 | the specified `msisdn` does not exist in the country. | [errorBody](#errorbody) |

### /agents/{msisdn}/wallets
---
##### ***GET***
**Summary:** get agent wallets

**Description:** return information about the current agent wallets


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | the msisdn of the agent, including the country prefix.  | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Ok. | [getAgentWalletsResponseBody](#getagentwalletsresponsebody) |
| 403 | Forbidden. Usually because of an invalid request.  Check `error.message` for details  | [errorBody](#errorbody) |
| 404 | the specified `msisdn` does not exist or is not an UberPOS Agent  | [errorBody](#errorbody) |

### /agentWallets
---
##### ***GET***
**Summary:** query multiple agent wallets

**Description:** return information about the current agents wallets. more than one agent can be queried at the same time


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| body | body |  | No | [queryAgentsWalletsGroupRequestBody](#queryagentswalletsgrouprequestbody) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Ok. | [queryAgentsWalletsGroupResponseBody](#queryagentswalletsgroupresponsebody) |
| 403 | Forbidden. Usually because of an invalid request.  Check `error.message` for details  | [errorBody](#errorbody) |
| 404 | the specified `msisdn` does not exist or is not an UberPOS Agent  | [errorBody](#errorbody) |

### /agents/{msisdn}/transactions
---
##### ***POST***
**Summary:** transfer money

**Description:** transfer money from the UberPOS Agent Wallet to the purchaser user


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | the msisdn of the agent | Yes | string |
| body | body |  | No | [transferMoneyRequestBody](#transfermoneyrequestbody) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Ok, the agent was successfully added.  | [transferMoneyResponseBody](#transfermoneyresponsebody) |
| 403 | Forbidden. Usually because of an invalid request.  Check `error.message` for details  | [errorBody](#errorbody) |
| 404 | the specified `msisdn` does not exist in the country  | [errorBody](#errorbody) |

##### ***GET***
**Summary:** query previous agent transactions

**Description:** query a list of transactions made by the agent in a date range


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | msisdn number of the agent  | Yes | string |
| startDate | query | start date for querying the transactions. ISO-8601 date only  | Yes | string |
| endDate | query | end date for querying the transactions. ISO-8601 date only  | Yes | string |
| limit | query | maximum number of transactions to return. 0 means no limit if not specified, it defaults to 10  | No | number (int32) |
| transactionType | query | desired type of transaction for que query  | No | string |
| targetMsisdn | query | destination of the transfer transaction. irrelevant for topup transactions. includes international code  | No | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Ok.  | [queryTransactionsResponseBody](#querytransactionsresponsebody) |
| 403 | Forbidden. Usually because of an invalid request.  Check `error.message` for details  | [errorBody](#errorbody) |
| 404 | means either the specified `msisdn` does not exist in the country no transactions are available on the provided range  | [errorBody](#errorbody) |

### Models
---

### errorBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error | object |  | Yes |

### conditionsObject  

specify one or more conditions that were not met thus the  403 response is sent to the invoker


| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| conditionCode | string | unique internal code for the failed condition. this CAN be used by the UI layer to map the message to something more adequate for presentation.
 | No |
| conditionMessage | string | developer oriented message indicating the failed condition and causes.
 | No |
| message | string | backend UI friendly message to show to end consumer. CAN be replaced with the invoker by creating a map internally with the `conditionCode` as the attribute
 | No |

### errorBodyActivateUberPOSAgent  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error | object |  | Yes |

### addUberPOSAgentResponseBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| msisdn | string | msisdn of the new agent | No |
| canOperate | boolean | indicates if the agent can or not operate  after being created
 | No |
| userLevel | number | level assigned to the new agent upon creation. this level establishes limits and attributions according to country rules.
 | No |

### addUberPOSAgentRequestBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| msisdn | string | msisdn of the new agent | Yes |
| documentId | string | document id of the new agent | Yes |
| documentIdType | string | type of  document id. each country provides the enumerated values
 | Yes |
| name | string | name of the agent | Yes |
| lastName | string | last name of the agent | Yes |
| dob | date | date of birth of the agent. ISO-8601 date | Yes |
| email | string | email address of the new agent | Yes |

### getUberPOSAgentResponseBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| msisdn | string | msisdn of the agent | Yes |
| documentId | string | document id of the agent | Yes |
| documentIdType | string | type of  document id. each country provides the enumerated values
 | Yes |
| name | string | name of the agent | Yes |
| lastName | string | last name of the agent | Yes |
| dob | date | date of birth of the agent. ISO-8601 date | Yes |
| email | string | email address of the new agent | Yes |
| canOperate | boolean | indicates if the agent can or not operate  after being created
 | Yes |
| userLevel | number | level assigned to the new agent upon creation. this level establishes limits and attributions according to country rules.
 | Yes |

### locationObject  

defines the location of the agent

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| longitude | double | longitude | Yes |
| latitude | double | latitude | Yes |

### transferMoneyRequestBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| targetMsisdn | string | msisdn of the purchaser | Yes |
| targetCarrier | string | target carrier for the transaction. | Yes |
| sourceCarrier | string | carrier of the UberPOS Agent. | Yes |
| amount | float | amount to be transferred | Yes |
| currency | string | currency of the transferred amount. ISO-4217 | Yes |
| transactionId | string | invoker unique transaction id for correlation purposes
 | Yes |
| agentLocation | [locationObject](#locationobject) |  | No |
| requestMethod | string | method used for requesting the transaction  (another app, buyer directly, etc.)        
 | No |

### transferMoneyResponseBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| transactionId | string | Tigo unique transaction id for correlation purposes
 | Yes |
| paidCommissionPercentage | double | percentage of comission paid
 | Yes |
| paidCommissionAmount | double | amount of commision paid
 | Yes |
| currency | string | currency of the paid commission. ISO-4217 | Yes |

### transactionObject  

definition of a transaction made by the agent


| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| internalTransactionId | string | Tigo unique transation id for correlation purposes
 | Yes |
| externalTransactionId | string | invoker unique transaction id for correlation purposes
 | Yes |
| transactionType | string | type of transaction
 | Yes |
| currency | string | currency of the transaction. ISO-4217 | Yes |
| amount | float | amount of the transaction | Yes |
| paidCommissionPercentage | double | percentage of comission paid
 | Yes |
| paidCommissionAmount | double | amount of commision paid
 | Yes |
| transactionTimestamp | string (datetime) | datetime of the transaction. ISO-8601
 | Yes |
| targetNumber | string | destination of | No |

### queryTransactionsResponseBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| queryTransactionsResponseBody | array |  |  |

### agentWalletInstance  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| walletId | string | id of the wallet | Yes |
| balance | double | balance on the wallet | Yes |
| currency | string | currency of the wallet. `ISO-4217` | Yes |

### agentWalletCollection  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| msisdn | string | msisdn of the wallet owner | No |
| wallets | [ [agentWalletInstance](#agentwalletinstance) ] |  | No |

### getAgentWalletsResponseBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| getAgentWalletsResponseBody |  |  |  |

### msisdnInstancePart  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| msisdn | string | msisdn of the agent | Yes |

### queryAgentsWalletsGroupRequestBody  

array of `msisdn` (including international prefix) of the agents
to query their wallets


| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| queryAgentsWalletsGroupRequestBody | array | array of `msisdn` (including international prefix) of the agents
to query their wallets
 |  |

### queryAgentsWalletsGroupResponseBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| queryAgentsWalletsGroupResponseBody | array |  |  |