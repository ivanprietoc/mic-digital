Mobile Self Care API
====================
This is the standard API for Self Care functions related to Mobile Phones and all other Mobile Network services for Tigo. 
We use swagger-2.0 specification

This document is used mainly for new API design of new use cases. Traditional use cases have not been ported here yet.
This is the reason we used v2


**Version:** 1.0.0

**Terms of service:**  
http://swagger.io/terms/

**Contact information:**  
Andres Cavallin  
http://www.millicom.com  
andres.cavallin@millicom.com  

**License:** [MIT](http://github.com/gruntjs/grunt/blob/master/LICENSE-MIT)

### /billing/subscribers/{MSISDN}/status
---
##### ***GET***
**Summary:** Get Status of Subscriber by MSISDN

**Description:** Returns the status of a subscriber


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| MSISDN | path | International Identifiable mobile phone number | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Status was successfully retrived | [Status](#status) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `MSISDN` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***PUT***
**Summary:** Update Status of Subscriber by MSISDN

**Description:** Update the status of a subscriber due to stolen SIM card, stolen phone or any other incident that requires the user to block the service.


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| MSISDN | path | International Identifiable mobile phone number | Yes | string |
| body | body |  | Yes | [StatusChangeRequest](#statuschangerequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Status was successfully updated | [Status](#status) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `MSISDN` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /billing/subscribers/{msisdn}/usage/data/hourlybyapp
---
##### ***GET***
**Summary:** Get Data Usage By MSISDN Per Hour and App

**Description:** Obtain a list of consumed services per hour.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | Unique identifier for the customer | Yes | string |
| startDate | query | (optional, ISO8601 datetime) Start date for query period, if not specified it should default to 24 hours ago, from current system datetime. | No | string |
| endDate | query | (optional, ISO8601 datetime) End Date for query period, if not specified, it should default to current system datetime. | No | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successfull | [getUsagePerHourResponse](#getusageperhourresponse) |
| 400 | Invalid Parameters | [error](#error) |
| 404 | Not found | [error](#error) |
| 500 | Server Error | [error](#error) |
| default | unexpected error | [error](#error) |

### /billing/subscribers/{msisdn}/usage/data/percentagebyapp
---
##### ***GET***
**Summary:** Get Data Usage Percentage By MSISDN Per App

**Description:** Obtain a list of consumed services percentage.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | Unique identifier for the customer | Yes | string |
| startDate | query | (optional, ISO8601 datetime) Start date for query period, if not specified it should default to 24 hours ago, from current system datetime. | No | string |
| endDate | query | (optional, ISO8601 datetime) End Date for query period, if not specified, it should default to current system datetime. | No | string |
| resolution | query | DAY means 1 record per hour per App/protocol and HOUR means 1 record per day per App/protocol (default if not specified). | No | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successfull | [getUsagePercentageResponse](#getusagepercentageresponse) |
| 400 | Invalid Parameters | [error](#error) |
| 404 | Not found | [error](#error) |
| 500 | Server Error | [error](#error) |
| default | unexpected error | [error](#error) |

### /plans/subscribers/{MSISDN}/favorites/
---
##### ***GET***
**Summary:** Get Favorite Numbers by MSISDN

**Description:** Retrieve a list of favorite numbers associated with the specified MSISDN

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| MSISDN | path | International Identifiable mobile phone number | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested Favorites Information was found | [FavoriteNumberList](#favoritenumberlist) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `Favorites Number List` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***POST***
**Summary:** Add Favorite Number by MSISDN

**Description:** If slots are still available, the specified phone number will be added to the list of favorite numbers of the provided MSISDN

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| MSISDN | path | International Identifiable mobile phone number | Yes | string |
| body | body |  | Yes | [FavoriteNumber](#favoritenumber) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | Favorite Number was successfully added | [successBody](#successbody) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `contractId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***DELETE***
**Summary:** Delete Favorite Numbers by MSISDN

**Description:** If found in the favorite number list of the specified MSISDN, the specified phone number will be deleted

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| MSISDN | path | International Identifiable mobile phone number | Yes | string |
| body | body |  | Yes | [FavoriteNumber](#favoritenumber) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Recurring Billing was successfully deleted | [successBody](#successbody) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `contractId` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /plans/subscribers/{MSISDN}/availableoffers/
---
##### ***GET***
**Summary:** Get Available Offers by MSISDN

**Description:** Retrieve a list of offers available to the specified MSISDN

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| MSISDN | path | International Identifiable mobile phone number | Yes | string |
| channelId | query | Channel used to present the offer. Default will be Self Care Web and App | No | integer |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested Offer Information was found | [OfferList](#offerlist) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `Offers List` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /plans/subscribers/{MSISDN}/acquiredoffers/{offerId}
---
##### ***POST***
**Summary:** Purchase Offer by MSISDN and OfferId

**Description:** The Subscriber specified by MSISDN will purchase the Offer specified by OfferId

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| MSISDN | path | International Identifiable mobile phone number | Yes | string |
| offerId | path | The Offer Unique Identifier obtained from Get Available Offers by MSISDN | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | Offer was successfully acquired | [successBody](#successbody) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `Offer Id` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***DELETE***
**Summary:** Delete Offer by MSISDN and OfferId

**Description:** The subscriber specified by MSISDN will remove the Offer specified by OfferId previously purchased

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| MSISDN | path | International Identifiable mobile phone number | Yes | string |
| offerId | path | The Offer Unique Identifier obtained from Get Available Offers by MSISDN | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | Offer was successfully acquired | [successBody](#successbody) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `Offer Id` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /plans/subscribers/{MSISDN}/phonelease/
---
##### ***GET***
**Summary:** Get Phone Lease Details by MSISDN

**Description:** Retrieve details of leased phone

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| MSISDN | path | International Identifiable mobile phone number | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested phone lease Information was found | [PhoneLeaseInfo](#phoneleaseinfo) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `phonelease` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /plans/subscribers/{MSISDN}/current
---
##### ***GET***
**Summary:** Get Current Plan Details by MSISDN

**Description:** Retrieve Current Plan Details for the provided Customer

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| MSISDN | path | International Identifiable mobile phone number | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested Current Plan Information was found | [Plan](#plan) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `Favorites Number List` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***PUT***
**Summary:** Update Current Plan by MSISDN

**Description:** Update the current plan for the MSISDN to the PlanId provided

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| MSISDN | path | International Identifiable mobile phone number | Yes | string |
| body | body |  | Yes | [PlanUpgrate](#planupgrate) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Offer was successfully acquired | [successBody](#successbody) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `request plan upgrate` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /plans/subscribers/{MSISDN}/availableplans/
---
##### ***GET***
**Summary:** Get Available Plans by MSISDN

**Description:** Obtain a Catalog of available plans by MSISDN that the client can select. Plans can be filtered by planType.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| MSISDN | path | International Identifiable mobile phone number | Yes | string |
| planType | query | Apply a filter to returned plans, for example Upgrades, Downgrades, Retention, Additional. If ommited, all plans in the Catalog are returned. | No | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested Upgrade Information was found | [PlanList](#planlist) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `Available Plans` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /plans/subscribers/{MSISDN}/upgrades/
---
##### ***GET***
**Summary:** Get Available Plans Upgrades by MSISDN

**Description:** Retrieve Available Plans that the customer can upgrade to the specified MSISDN.
This is specific use case of the "Get Available Plans by MSISDN" method.


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| MSISDN | path | International Identifiable mobile phone number | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested Upgrade Information was found | [PlanList](#planlist) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `Available Plans` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /plans/subscribers/{MSISDN}/upgraderequest
---
##### ***GET***
**Summary:** Get Upgrade Request Status by MSISDN

**Description:** Get information if the customer has initiated an upgrade or not for the provided Customer

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| MSISDN | path | International Identifiable mobile phone number | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested status of plan update Information was found | [successBody](#successbody) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `status of plan update` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

##### ***POST***
**Summary:** Create Upgrade Request by MSISDN

**Description:** Register a request from the MSISDN to receive a plan upgrade

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| MSISDN | path | International Identifiable mobile phone number | Yes | string |
| body | body |  | Yes | [PlanUpgrate](#planupgrate) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Offer was successfully acquired | [successBody](#successbody) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `request plan upgrate` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /plans/subscribers/{MSISDN}/subscriptionrequests/
---
##### ***POST***
**Summary:** Create Subscription Requests by MSISDN

**Description:** Register one or more requests made by the specified MSISDN to accquire Additional Subscriptions

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| MSISDN | path | International Identifiable mobile phone number | Yes | string |
| body | body |  | Yes | [PlanAdditional](#planadditional) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Offer was successfully acquired | [successBody](#successbody) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `request plan upgrate` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### Models
---

### Status  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| code | string | Status Code. May be alphanumeric | Yes |
| description | string | Human readable status if needed. | No |
| assetType | string | Asset which status is being returned | Yes |

### StatusChangeRequest  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| code | string | Status Code. May be alphanumeric | Yes |
| assetType | string | Asset which status is being updated | Yes |
| updateReason | string | Reson of status being updated | No |
| customerId | string | Customer unique identifier, usually national identification number or company tax payer number | No |
| documentType | string | Defines if customerId es a National Id, Tax Payer Number, Passport, etc. | No |
| name | string | First Name, Comapny Name or Full Name of the Customer | No |
| lastName | string | Last Name of the Custoemr | No |

### FavoriteNumberList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| FavoriteNumberList | array |  |  |

### FavoriteNumber  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| PhoneNumber | string | Phone Number that is considered a Favorite Number | Yes |
| ExpirationDate | date | Optional value if this number have an expiration date | No |
| Label | string | Optional value if this number has a description or user defined label | No |
| PlanCode | string | Optional plan code or number to which this PhoneNumber is being added | No |

### OfferList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| OfferList | array |  |  |

### Offer  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| OfferId | string | Unique Id of the offering, needed to complete the order. | Yes |
| OfferName | string | Short name for the offer | Yes |
| Description | string | Explanation to the user. | No |
| Validity | string | The quantitative number or period for which the offer is valid. | No |
| ValidityUnit | string | The period unit. Could be Hour, Day, Week, Month, Megabytes, Gigabytes, Slots | No |
| CategoryName | string | The name of main category of this offer | No |
| SubCategoryName | string | The name of the secondary category of this offer | No |
| Rank | number | This value is used to present the offers in a sorted order. | No |
| amount | double |  | No |
| currencyId | string | This is the ISO Id of the currency | No |
| AcquisitionMethodList | [AcquisitionMethod](#acquisitionmethod) |  | No |

### AcquisitionMethod  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| AcquisitionMethodId | number | Unique Id of the Acquisition Method | Yes |
| AcquisitionMethodName | string | Short name for the Acquisition Method. Could be Next Invoice or Prepaid | Yes |

### PlanList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| PlanList | array |  |  |

### Plan  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| planId | string | Unique Id of the plan | Yes |
| planName | string | Short name for the plan | Yes |
| monthlyAmount | number | Monthly base amount that customer pays for this plan | Yes |
| planDataInMB | number | Monthly megabytes included in this plan. 
This value is also included in the ProdutOffering array but must be reflected in this value so megabytes can be compared,
charted and better communicated to the customer.
 | No |
| currencyId | string | This is the ISO Id of the currency | No |
| status | string | Status of this plan, may help build the UX | No |
| CategoryName | string | The name of main category of this plan | No |
| Rank | number | This value is used to present the offers in a sorted order. | No |
| productOfferingList | [ [ProductOffering](#productoffering) ] | An array of offering details grouped by category | No |

### NameValuePair  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| name | string | This is the name of the of data | No |
| value | string | this is the value | No |

### ProductOffering  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| offeringCategory | string | This is the category that defines the type of offering | No |
| offeringId | string | This is the id of that type of offering | No |
| offeringDetailList | [ [NameValuePair](#namevaluepair) ] | An array of Name and Value pair for additional services | No |

### PhoneLeaseInfo  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| clauseId | string | Identifier that legacy uses for that permanency clause | No |
| lastBillingDate | date | Last billing of the contract with equipment | Yes |
| nextRenewalDate | date | Next renewal of the contract with equipment | Yes |
| typeClauseId | string | Type of permanency clause | No |
| imei | string | International Mobile Station Equipment Identity | No |
| gama | string | Equipment gama | No |
| brand | string | Equipment brand | No |
| model | string | Equipment model | No |
| insurance | string | Confirmation if the equipment is or is not insured | No |
| status | string | Status of the comodato | No |

### PlanUpgrate  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| name | string | Full Name of the Customer | No |
| email | string | Email of the Customer | No |
| planId | string | Unique Id of the NEW plan | Yes |
| planName | string | Short name for the NEW plan | No |
| monthlyAmount | number | Monthly base amount that customer pays for the NEW plan | No |
| currencyId | string | This is the ISO Id of the currency | No |
| categoryName | string | The name of main category of the NEW plan | No |
| fromPlan | string | Source or Id of the OLD plan | No |

### PlanAdditional  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| fromPlan | string | Source of the plan | No |
| planId | string | Unique Id of the plan | Yes |
| planName | string | Short name for the plan | Yes |
| categoryName | string | The name of main category of this plan | Yes |
| name | string | Full Name of the Customer | Yes |
| email | string | Email of the Customer | No |
| AdditionalSubscriptionsList | [ [AdditionalSubscriptions](#additionalsubscriptions) ] |  | No |

### AdditionalSubscriptions  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| currencyId | string | This is the ISO Id of the currency | No |
| email | string | Email of the Customer | No |
| planId | string | Unique Id of the plan | Yes |
| planName | string | Short name for the plan | Yes |
| categoryName | string | The name of main category of this plan | No |
| monthlyAmount | number | Monthly base amount that customer pays for this plan | No |

### getUsagePerHourResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| code | string |  | No |
| description | string |  | No |
| totalVolumeBytes | number |  | No |
| lastUpdatedAt | string |  | No |
| trafficDetails | [usagePerHourList](#usageperhourlist) |  | No |

### getUsagePercentageResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| code | string |  | No |
| description | string |  | No |
| lastUpdatedAt | string |  | No |
| trafficDetails | [usagePercentageList](#usagepercentagelist) |  | No |

### usagePerHourList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| usagePerHourList | array |  |  |

### usagePercentageList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| usagePercentageList | array |  |  |

### usagePerHourDetail  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| date | string |  | No |
| hour | string |  | No |
| appName | string |  | No |
| trafficVolumeBytes | number |  | No |

### usagePercentageDetail  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| date | string |  | No |
| percentage | string |  | No |
| appName | string |  | No |
| trafficVolumeBytes | number |  | No |

### error  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| statusCode | integer |  | No |
| code | string |  | No |
| message | string |  | No |
| developerMessage | string |  | No |

### successBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| response | string | Generic response from platform. May be ommited. | No |
| message | string | Success Message from platform. May be ommited. | No |

### errorBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| code | integer |  | Yes |
| message | string |  | Yes |