Mobile Money API - Accounts
===========================
Millicom version of GSMA Harmonized Mobile Money API for handling Accounts.<br>
The Accounts APIs are used to view properties associated with an account resource. Types of account include mobile wallets, financial institution accounts and utility accounts (e.g. for electricity).
Two methods are provided for identifying an account � *the multiple identifiers method* and *the MSISDN identifier method.

**Multiple Identifiers Method :** There is no single industry-accepted method of uniquely identifying an account. There are numerous methods of identifying an account and the list of permitted identifiers can be found in the Account Identifiers section. Every Account API identifies the target account through the URI. As there can be multiple identifiers required to identify the target account, the URI uses a �$� delimiter to separate each identifier. 
The format can be expressed as:

`/accounts/{accountIdentifier1}@{value1}${accountIdentifier2}@{value2}${accountIdentifier3}@{value3}`

Possible accountIdentifiers are:
- MSISDN
- Users ID number depending on the country this could be:
      `DUI` for El Salvador
      `DPI` for Guatemala
      `TDI` for Honduras
      `CI` for Paraguay and Bolivia
- MFS Platform unique user ID

**MSISDN Identifier Method :** In the scenario where MSISDN is the only identifier needed to uniquely identify an account, an alternate short URI is available:
`/accounts/msisdn/{value}`

See [https://mmapi.gsma.com/accounts/]


**Version:** 1.0.0

**Terms of service:**  
https://mmapi.gsma.com/

**Contact information:**  
Andres Cavallin  
https://mmapi.gsma.com/  
andres.cavallin@millicom.com  

**License:** [MIT](http://github.com/gruntjs/grunt/blob/master/LICENSE-MIT)

### Security
---
**applicationLevel_auth**  

|apiKey|*API Key*|
|---|---|
|Description|This API Key is a secret known only to the API Client and the API Gateway server. Never store in an App. API Key secret is used instead of oauth2 grant type "client credentials" to avoid conflict with user level security which uses oauthv2 (Open ID Connect) |
|Name|api_key|
|In|header|

**userLevel_auth**  

|oauth2|*OAuth 2.0*|
|---|---|
|Description|Any party in possession of a bearer token (a "bearer") can use it to get access to the associated resources (without demonstrating possession of a cryptographic key). To prevent misuse, bearer tokens need to be protected from disclosure in storage and in transport. This token is going to be passed to the Mobile Money Backend who supports it.  If not supported, this token can be used to retrieve proper credentials to be presented to the backend (MFS ID) |
|Flow|accessCode|
|Authorization URL|https://mic-test.apigee.net/oauth/v2/authorize?response_type=code{&redirect_uri,client_id,scope,state,nonce,prompt,display,login_hint}|
|Token URL|https://myapp.tigo.com/tigoid/callback|
|**Scopes**||
|openid|Used to identify this API is compliant with the OpenID Connect 1.0 specification|
|profile|May be useful for self registering the user. Includs name, birthday, photo on Tigo ID, not the KWY|
|email|Email address of the user used to register on Tigo ID, not the KYC|
|phone|The MSISDN. Also the account identifier on the Mobile Money Platform|
|write:transactions|Create or update transactions that affect the balance|
|read:transactions|Query existing transactions that affected the wallet|
|write:accounts|Modify information about the account like name or PIN|
|read:accounts|Read information about the account like balance or address|
|read:companioncard|Elevated privileges to see the full Companion Card Info. Must expire in a short period.|
|write:companioncard|Elevated privileges to associate a Companion card to the account. Requires two factor authentication.|
|merchantpayment|Grant permission to a third party merchant to charge (debit) the account. One time use.|

**legacyUserLevel_auth**  

|basic|*Basic*|
|---|---|
|Description|If basic credentials are present, token based authentication is ommited.  Use only as a fallback method when there is no support for Open ID Connect at the Mobile Money Platform nor MFS ID deployment. Best practice is for PIN to be encrypted and salted at the source using a pre-shared key and symmetric algorithm obtained during provisioning of the API Client. The API Client (App Server) can then pass this decrypted credentials to the API Gateway. |

### /accounts/{accountId}
---
##### ***POST***
**Summary:** Create Account

**Description:** Create a new account linked to the ACCOUNT identifier and with the provided KYC information. If the account already exists, this call will fail.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| Date | header | Header parameter to indicate the date and time that the message was originated | Yes | string (datetime) |
| accountId | path | Path variable to uniquely identify an account | Yes | string |
| kyc | body |  | Yes | [kyc](#kyc) |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 |  |
| 400 |  |
| 401 |  |
| 404 |  |
| 500 |  |
| 503 |  |

##### ***GET***
**Summary:** View Account KYC

**Description:** View KYC information linked to the provided ACCOUNT identifier.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| Date | header | Header parameter to indicate the date and time that the message was originated | Yes | string (datetime) |
| accountId | path | Path variable to uniquely identify an account | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 |  |
| 400 |  |
| 401 |  |
| 404 |  |
| 500 |  |
| 503 |  |

##### ***PUT***
**Summary:** Update Account KYC

**Description:** Update KYC information for an existing account linked to the provided ACCOUNT identifier. If the account does not exists, this call will fail.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| Date | header | Header parameter to indicate the date and time that the message was originated | Yes | string (datetime) |
| accountId | path | Path variable to uniquely identify an account | Yes | string |
| kyc | body |  | Yes | [kyc](#kyc) |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 |  |
| 400 |  |
| 401 |  |
| 404 |  |
| 500 |  |
| 503 |  |

### /accounts/{accountId}/kyc/accountname
---
##### ***GET***
**Summary:** View Account Name

**Description:** This endpoint returns the name of an account (via ACCOUNT identifier)

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| Date | header | Header parameter to indicate the date and time that the message was originated | Yes | string (datetime) |
| accountId | path | Path variable to uniquely identify an account | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 |  |
| 400 |  |
| 401 |  |
| 404 |  |
| 500 |  |
| 503 |  |

### /accounts/{accountId}/status
---
##### ***GET***
**Summary:** View Account Status

**Description:** This endpoint returns the current status of an account (via ACCOUNT identifier)

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| Date | header | Header parameter to indicate the date and time that the message was originated | Yes | string (datetime) |
| accountId | path | Path variable to uniquely identify an account | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 |  |
| 400 |  |
| 401 |  |
| 404 |  |
| 500 |  |
| 503 |  |

### /accounts/{accountId}/balance
---
##### ***GET***
**Summary:** View Account Balance

**Description:** This endpoint returns the balance of an account (via ACCOUNT identifier)

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| Date | header | Header parameter to indicate the date and time that the message was originated | Yes | string (datetime) |
| accountId | path | Path variable to uniquely identify an account | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 |  |
| 400 |  |
| 401 |  |
| 404 |  |
| 500 |  |
| 503 |  |

### /accounts/{accountId}/transactions
---
##### ***GET***
**Summary:** View Account Specific Transactions

**Description:** This endpoint returns transactions linked to a specific account (via ACCOUNT identifier). Filters include date and transaction type. Supports pagination.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| Date | header | Header parameter to indicate the date and time that the message was originated | Yes | string (datetime) |
| accountId | path | Path variable to uniquely identify an account | Yes | string |
| limit | query | Supports pagination. If this is not supplied, then the server will apply a limit of 50 records returned for each request. | No | integer |
| offset | query | Supports pagination. This value will indicate the cursor position from where to retrieve the set of records. For example, a limit of 50 and offset of 10 will return records 10 to 60. | No | integer |
| fromDateTime | query | Indicates the minimum date for which records should be returned | No | string (datetime) |
| toDateTime | query | Indicates the maximum date for which records should be returned | No | string (datetime) |
| type | query | Filter so only transactions that has matching type are returned. If ommited all types are included. | No | [ [transactionTypeEnum](#transactiontypeenum) ] |
| status | query | Filter so only transactions that has matching status, as stored by the API provider,  are returned. If ommited all status are included. Possible values as defined by requestStateStatusEnum: pending, completed and failed. | No | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 |  |
| 400 |  |
| 401 |  |
| 404 |  |
| 500 |  |
| 503 |  |

### Models
---

### baseTransaction  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| amount | double | Principle Transaction Amount. | Yes |
| currency | [currenciesEnum](#currenciesenum) | Currency of the principal transaction amount. | Yes |
| type | [transactionTypeEnum](#transactiontypeenum) | The harmonised Transaction Type | Yes |
| subType | string | A non-harmonised sub-classification of the type of transaction. Values are not fixed and usage will vary according to Provider. | No |
| descriptionText | string | Free format text description of the transaction provided by the client. This can be provided as a reference for the receiver on the SMS and on the account statement. | No |
| requestDate | dateTime | The creation date and time of the transaction as supplied by the client. | Yes |
| oneTimeCode | string | A one-time code that can be supplied in the request or can be generated in the response depending upon the use case. | No |
| geoCode | string | Indicates the geographic location from where the transaction was initiated. | No |
| debitParty | [ [accountIdentifierBase](#accountidentifierbase) ] | A collection of key/value pairs that enable the debit party to be identified. Keys include MSISDN and Wallet Identifier. | Yes |
| creditParty | [ [accountIdentifierBase](#accountidentifierbase) ] | A series of key/value pairs that enable the credit party to be identified. Keys include MSISDN and Wallet Identifier. | Yes |
| senderKyc | [kyc](#kyc) | A collection of properties detailing the KYC of the transaction Sender, typically used for International Transfers. | No |
| recipientKyc | [kyc](#kyc) | A collection of properties detailed the KYC of the transaction Recipient, typically used for International Transfers. | No |
| originalTransactionReference | string | For reversals and refunds, this property indicates the transaction which is the subject of the reversal. | No |
| servicingIdentity | string | The property is used to identify the servicing identity for ?present? transactions, e.g. till, POS ID, assistant ID | No |
| metadata | [ [metadata](#metadata) ] | A collection of key/value pairs. These can be used to populate additional transaction properties. | No |

### requestTransaction  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| requestTransaction |  |  |  |

### responseTransaction  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| responseTransaction |  |  |  |

### internationalTransfer  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| originCountry | [countriesEnum](#countriesenum) | The originating country of the transaction, i.e. the country where the transaction commenced. | Yes |
| quotationReference | string | Reference for the quotation that was provider to the sender. | No |
| quoteId | string | The specific quote associated with the quotation. | No |
| receivingCountry | [countriesEnum](#countriesenum) | Destination Country of international remittance. | No |
| remittancePurpose | string | Property providing a description of the reason for the international remittance. | No |
| relationshipSender | string | Indicates the relationship (if any) between the sender and the receiver. | No |
| deliveryMethod | [deliveryMethodEnum](#deliverymethodenum) | The recipient delivery method as chosen by the sender. | No |

### internationalTransferResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| internationalTransferResponse |  |  |  |

### baseReversal  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| amount | double | Principle Transaction Amount. | No |
| currency | [currenciesEnum](#currenciesenum) | Currency of the principal transaction amount. | No |
| type | [transactionTypeEnum](#transactiontypeenum) | The harmonised Transaction Type | Yes |
| subType | string | A non-harmonised sub-classification of the type of transaction. Values are not fixed and usage will vary according to Provider. | No |
| descriptionText | string | Free format text description of the transaction provided by the client. This can be provided as a reference for the receiver on the SMS and on the account statement. | No |
| requestDate | dateTime | The creation date and time of the transaction as supplied by the client. | Yes |
| geoCode | string | Indicates the geographic location from where the transaction was initiated. | No |
| debitParty | [ [accountIdentifierBase](#accountidentifierbase) ] | A collection of key/value pairs that enable the debit party to be identified. Keys include MSISDN and Wallet Identifier. | No |
| creditParty | [ [accountIdentifierBase](#accountidentifierbase) ] | A series of key/value pairs that enable the credit party to be identified. Keys include MSISDN and Wallet Identifier. | No |
| servicingIdentity | string | The property is used to identify the servicing identity for ?present? transactions, e.g. till, POS ID, assistant ID | No |
| metadata | [ [metadata](#metadata) ] | A collection of key/value pairs. These can be used to populate additional transaction properties. | No |

### requestReversal  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| requestReversal |  |  |  |

### responseReversal  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| responseReversal |  |  |  |

### accountStatus  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| status | [accountStatusEnum](#accountstatusenum) | Indicates a simplified representation of the account state. This will be shown as ?Available? or ?Unavailable?. A state of ?Unavailable? means that the account is in a state that does not allow posting of transactions. Unregistered indicates that although not available a transaction created with the account identifier(s) will result an unregistered voucher creation. | Yes |
| subStatus | string | Property can be used to return a provider-specific status for the account. | No |

### accountBalance  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| currentBalance | double | Current outstanding balance on the account. | No |
| availableBalance | double | Indicates the balance that is able to be debited for an account. This balance is only provided on some API provider systems. | No |
| reservedBalance | double | Indicates the portion of the balance that is reserved, i.e. intended to be debited. This balance is only provided on some API provider systems. | No |
| unclearedBalance | double | Indicates the sum of uncleared funds in an account, i.e. those that are awaiting a credit confirmation. | No |
| currency | [currenciesEnum](#currenciesenum) | Currency for all returned balances. | No |
| status | [accountStatusEnum](#accountstatusenum) | Indicates a simplified representation of the account state. This will be shown as ?Available? or ?Unavailable?. A state of ?Unavailable? means that the account is in a state that does not allow posting of transactions. Unregistered indicates that although not available a transaction created with the account identifier(s) will result an unregistered voucher creation. | No |

### accountName  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| name | [name](#name) | A collection of properties detailing the name of the Primary Account Holder. | No |
| status | [accountStatusEnum](#accountstatusenum) | Indicates a simplified representation of the account state. This will be shown as ?Available? or ?Unavailable?. A state of ?Unavailable? means that the account is in a state that does not allow posting of transactions. Unregistered indicates that although not available a transaction created with the account identifier(s) will result an unregistered voucher creation. | Yes |

### statementEntry  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| amount | double | Requested transaction amount. | Yes |
| currency | [currenciesEnum](#currenciesenum) | Currency of the requested transaction amount. | Yes |
| displayType | string | The transaction type that is to be used for presentation to the account holder as determined by the API provider. This is not necessarily the actual transaction type. | No |
| transactionStatus | string | Indicates the status of the transaction as represented by the API provider. | Yes |
| descriptionText | string | Free format text description of the transaction provided by the client. This can be provided as a reference for the receiver on the SMS and on the account statement. | No |
| requestDate | string (datetime) | The creation date and time of the transaction as supplied by the client. | No |
| creationDate | string (datetime) | Date and time when the transaction was created by the API Provider. | No |
| modificationDate | string (datetime) | Date and time when the transaction modified by the API Provider. | No |
| transactionReference | string | Unique reference for the transaction. This is returned in the response by API provider. Note that for GET and PATCH requests, the Transaction Reference for the subject can be provided in the URI. | Yes |
| transactionReceipt | string | Transaction receipt number as notified to the parties. This may differ from the Transaction Reference. | No |
| debitParty | [ [accountIdentifierBase](#accountidentifierbase) ] | A collection of key/value pairs that enable the debit party to be identified. Keys include MSISDN and Wallet Identifier. | Yes |
| creditParty | [ [accountIdentifierBase](#accountidentifierbase) ] | A series of key/value pairs that enable the credit party to be identified. Keys include MSISDN and Wallet Identifier. | Yes |

### bill  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| currency | [currenciesEnum](#currenciesenum) | Currency of the bill to be paid. | No |
| amountDue | double | Amount outstanding on the bill to be paid. | No |
| dueDate | date | Date on which the Bill is due to be paid. | No |
| billReference | string | Reference number for the Bill that this payer can use when he/she wishes to pay. | No |
| minimumAmountDue | double | The minimum amount that is outstanding on the bill to be paid. | No |

### baseDebitMandate  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| currency | [currenciesEnum](#currenciesenum) | Currency of the principal transaction amount. | No |
| amountLimit | double | The maximum amount that can be taken by the Payee on a payment request. | No |
| startDate | date | Date on which the first payment is to be taken. | Yes |
| endDate | date | Date on which the final payment is to be taken. | No |
| numberOfPayments | number (int32) | Indicates the number of consecutive payments that are to be taken. | No |
| frequencyType | [frequencyTypeEnum](#frequencytypeenum) | Indicates the frequency for which payments will be taken from the payers account. | No |
| mandateStatus | [mandateStatusEnum](#mandatestatusenum) | Indicates the status of the Mandate as held in the API Provider system. | No |
| requestDate | string (datetime) | The request date and time of the transaction as supplied by the client. | Yes |

### requestDebitMandate  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| requestDebitMandate |  |  |  |

### responseDebitMandate  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| responseDebitMandate |  |  |  |

### link  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| status | [linkStatusEnum](#linkstatusenum) | Indicates the status of the Link. | Yes |
| mode | [linkModeEnum](#linkmodeenum) | Indicates the mode of operation support for the Link. If not populated, then default value it ?Both?. | No |

### responseLink  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| responseLink |  |  |  |

### baseQuotation  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| requestDate | string (datetime) | The creation date and time of the transaction as supplied by the client. | Yes |
| debitParty | [ [accountIdentifierBase](#accountidentifierbase) ] | A collection of key/value pairs that enable the debit party to be identified. Keys include MSISDN and Wallet Identifier. | Yes |
| creditParty | [ [accountIdentifierBase](#accountidentifierbase) ] | A series of key/value pairs that enable the credit party to be identified. Keys include MSISDN and Wallet Identifier. | Yes |
| senderKyc | [kyc](#kyc) | A collection of properties detailing the KYC of the transaction Sender, typically used for International Transfers. | No |
| recipientKyc | [kyc](#kyc) | A collection of properties detailed the KYC of the transaction Recipient, typically used for International Transfers. | No |
| requestAmount | double | Requested quotation amount. | Yes |
| requestCurrency | [currenciesEnum](#currenciesenum) | Currency of the requested quotation amount. | Yes |
| chosenDeliveryMethod | [deliveryMethodEnum](#deliverymethodenum) | The delivery method chosen by the sending end user as the specific delivery method to be used in the quotes received. | No |
| quotes | [ [quote](#quote) ] | A collection of quotes. A quote can be received from a single receiving payment service provider or from multiple providers. | No |
| senderBlockingReason | string | The reason for blocking the quotation, based on AML checks on the sender. | No |
| recipientBlockingReason | string | The reason for blocking the quotation, based on AML checks on the recipient. | No |
| metadata | [ [metadata](#metadata) ] | A collection of key/value pairs. These can be used to populate additional quotation properties. | No |

### requestQuotation  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| requestQuotation |  |  |  |

### responseQuotation  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| responseQuotation |  |  |  |

### requestState  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| serverCorrelationId | string | A unique identifier issued by the provider to enable the client to identify the RequestState resource on subsequent polling requests. | Yes |
| status | [requestStateStatusEnum](#requeststatestatusenum) | Indicates the status of the request. | Yes |
| pendingReason | string | A textual description that can be provided to describe the reason for a pending status. | No |
| notificationMethod | [notificationMethodEnum](#notificationmethodenum) | Indicates whether a callback will be issued or whether the client will need to poll. | Yes |
| objectReference | string | Provides a reference to the subject resource, e.g. transaction reference. | No |
| expiryTime | string (datetime) | Indicate the time by which the provider will fail the request if completion criteria have not been met. For an example, a debit party failing to authorise within the allowed time period. | No |
| pollLimit | number (int32) | Indicates the number of poll attempts for the given requeststate resource that will be allowed by the provider. | No |
| error | [error](#error) |  | No |

### kyc  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| nationality | [countriesEnum](#countriesenum) | Nationality of the KYC subject. | No |
| dateOfBirth | date | Birth date of the KYC subject. | Yes |
| occupation | string | Occupation of the KYC subject. | No |
| employerName | string | Employer Name of the KYC subject. | No |
| contactPhone | string | Contact phone number (mobile or landline) of the KYC subject. | No |
| gender | [genderEnum](#genderenum) | Gender of the KYC Object. | No |
| idDocument | [ [idDocument](#iddocument) ] | An array of properties containing the forms of identification that are associated with the subject. | Yes |
| postalAddress | [address](#address) | A collection of properties that details the postal address of the KYC subject. | Yes |
| subjectName | [name](#name) | Refers to the name properties for the KYC subject. | Yes |
| emailAddress | string | Email address of the KYC subject. | No |
| birthCountry | [countriesEnum](#countriesenum) | The country of birth of the KYC subject. | No |

### name  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| title | string | The given title of the KYC subject, e.g. Mr, Mrs, Dr. | No |
| firstName | string | First name (also referred to as given name) of the KYC subject. | No |
| middleName | string | Middle Name of the KYC subject. | No |
| lastName | string | Surname (also referred to as last or family name) of the KYC subject. | No |
| fullName | string | The full name of the KYC subject. | No |
| nativeName | string | The full name expressed as in the native language. | No |

### idDocument  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| idType | [idTypeEnum](#idtypeenum) | Indicates the type of identification for the KYC subject, e.g. passport, driving licence etc. | Yes |
| idNumber | string | Reference pertaining to the type of identification for the KYC subject. | No |
| issueDate | date | Date of issue for the identification document. | No |
| expiryDate | date | Date of expiry for the identification document. | No |
| issuer | string | Indicates the organisation/government entity that issued the ID document. | No |
| issuerPlace | string | Place of issue for the identification type. | No |
| issuerCountry | [countriesEnum](#countriesenum) | Country where the identification type was issued. | No |
| otherIdDescription | string | Where an ID Type of ?OtherID? is specified, a description of the type of identification can be provided in this property. | No |

### address  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| addressLine1 | string | First line of the address. | No |
| addressLine2 | string | Second line of the address. | No |
| addressLine3 | string | Third line of the address. | No |
| city | string | City/Town | No |
| stateProvince | string | State or Province | No |
| postalCode | string | Postal Code | No |
| country | [countriesEnum](#countriesenum) | Country | Yes |

### quote  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| quoteId | string | The unique ID for this quote. | Yes |
| quoteExpiryTime | string (datetime) | The timestamp when the quote will expire. | No |
| receivingServiceProvider | string | The name of the RSP, i.e. the provider that the quote is associated with. | No |
| sendingAmount | double | Requested quotation amount as supplied by the sender. | Yes |
| sendingCurrency | [currenciesEnum](#currenciesenum) | Currency of the requested quotation amount. | Yes |
| receivingAmount | double | The total amount as it will be received by the receiving end user. | Yes |
| receivingCurrency | [currenciesEnum](#currenciesenum) | The currency of the quote. | Yes |
| fxRate | double | The conversion rate applicable between the sending and the receiving currency for the requested transaction. | Yes |
| deliveryMethod | [deliveryMethodEnum](#deliverymethodenum) | The delivery method that is applicable to the quotation. | No |

### metadata  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| key | string | Identifies the type of additional property. | Yes |
| value | string | Identifies the value of the additional property. | Yes |

### error  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| errorCategory | [errorCategoryEnum](#errorcategoryenum) | The category grouping for the error. | Yes |
| errorCode | [errorCodeEnum](#errorcodeenum) | The harmonised error code identifying the reason for error. | Yes |
| errorDescription | string | A textual Description of the error. | No |
| errorDateTime | string (datetime) | The timestamp indicating when the error occurred. | No |
| errorParameters | [ [metadata](#metadata) ] | Diagnostic information in the form of key/value pairs relating to the error. | No |

### heartbeat  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| serviceStatus | [serviceStatusEnum](#servicestatusenum) | Provides the status of the requested service. | Yes |
| delay | number (int64) | The anticipated processing delay in milliseconds. | No |

### response  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| link | string | Provides a URL to the resource associated with the given correlation ID. | Yes |

### patch  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| op | [patchOpEnum](#patchopenum) |  | Yes |
| path | string |  | Yes |
| value | string |  | Yes |

### accountIdentifierBase  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| key | string | Provides the account identifier type. | Yes |
| value | string | Provides the account identifier type value. | Yes |

### accountCategory  

Can be used to identify the sources of funds category where there are multiple accounts (wallets) held against an account holder.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| accountCategory |  | Can be used to identify the sources of funds category where there are multiple accounts (wallets) held against an account holder. |  |

### bankAccountNo  

Financial institution account number that is typically known by the account holder.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| bankAccountNo |  | Financial institution account number that is typically known by the account holder. |  |

### accountRank  

Is used to identify the rank of the source of funds ranks where there are multiple accounts (wallets) held against an account holder.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| accountRank |  | Is used to identify the rank of the source of funds ranks where there are multiple accounts (wallets) held against an account holder. |  |

### identityAlias  

An alias for the identity, e.g. short code for an agent till or company name/number for a bill payment.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| identityAlias |  | An alias for the identity, e.g. short code for an agent till or company name/number for a bill payment. |  |

### iban  

Internationally agreed system of identifying bank accounts across national borders to facilitate the communication and processing of cross border transactions. Can contain up to 34 alphanumeric characters.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| iban |  | Internationally agreed system of identifying bank accounts across national borders to facilitate the communication and processing of cross border transactions. Can contain up to 34 alphanumeric characters. |  |

### accountId  

Identifier for the account holder.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| accountId |  | Identifier for the account holder. |  |

### msisdn  

Mobile Number of the account holder. Should conform to ITU E.123.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| msisdn |  | Mobile Number of the account holder. Should conform to ITU E.123. |  |

### payRef  

Payment reference, i.e. utility bill number.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| payRef |  | Payment reference, i.e. utility bill number. |  |

### swiftbic  

A bank identifier code (BIC) is a unique identifier for a specific financial institution. A BIC is composed of a 4-character bank code, a 2-character country code, a 2-character location code and an optional 3-character branch code. BICs are used by financial institutions for letters of credit, payments and securities transactions and other business messages between banks. Please refer to ISO 9362 for further information.

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| swiftbic |  | A bank identifier code (BIC) is a unique identifier for a specific financial institution. A BIC is composed of a 4-character bank code, a 2-character country code, a 2-character location code and an optional 3-character branch code. BICs are used by financial institutions for letters of credit, payments and securities transactions and other business messages between banks. Please refer to ISO 9362 for further information. |  |

### transactionTypeEnum  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| transactionTypeEnum | string |  |  |

### countriesEnum  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| countriesEnum | string |  |  |

### currenciesEnum  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| currenciesEnum | string |  |  |

### genderEnum  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| genderEnum | string |  |  |

### idTypeEnum  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| idTypeEnum | string |  |  |

### deliveryMethodEnum  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| deliveryMethodEnum | string |  |  |

### frequencyTypeEnum  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| frequencyTypeEnum | string |  |  |

### accountStatusEnum  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| accountStatusEnum | string |  |  |

### mandateStatusEnum  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| mandateStatusEnum | string |  |  |

### linkStatusEnum  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| linkStatusEnum | string |  |  |

### linkModeEnum  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| linkModeEnum | string |  |  |

### quotationStatusEnum  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| quotationStatusEnum | string |  |  |

### patchOpEnum  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| patchOpEnum | string |  |  |

### requestStateStatusEnum  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| requestStateStatusEnum | string |  |  |

### notificationMethodEnum  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| notificationMethodEnum | string |  |  |

### serviceStatusEnum  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| serviceStatusEnum | string |  |  |

### errorCategoryEnum  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| errorCategoryEnum | string |  |  |

### errorCodeEnum  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| errorCodeEnum | string |  |  |