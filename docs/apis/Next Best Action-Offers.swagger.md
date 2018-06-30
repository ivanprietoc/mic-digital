Next Best Action-Offers
=======================
This the especific description for the API for a centralized Next Best Offer and Next Best Action, this documentation is in swagger-2.0 specification. 

The objective of this API is to deliver the information of the following actions or offers that are proposed for a user from commercial or retention offers.

This solution is to be used in all countries, each country will be indentified in the path. This solution It covers the requirement to request information about the offers that a user has calculated according to their behavior.
The information that will be used for these use cases is obtained directly from the calculation of a supplier (<a href="https://www.exacaster.com/">Exacaster</a>) that will deliver through an API service. This model is intended to be the data model that we want to show to users. 

In the cases of the countries where exacaster has not been implemented, a static database will be used that the country must feed daily and a service with the same design proposed here should be presented.

In the case that (<a href="https://www.exacaster.com/">Exacaster</a>) don't have the implemented the project is going to use a static database that the country must feed daily and a service with the same design proposed here should be presented.

The API Proxy will group all the fulfillment methods a country offers, and will be named <b>v1_tigo_{businessunit}_{country}</b>

So the base for each proxy wiil be: 

<b>`/v1/tigo/{businessunit}/{country}`</b>

And then the path will include the business unit and product type:

Suggested Examples:
* `/v1/tigo/mobile/gt/catalog/`
* `/v1/tigo/home/sv/catalog/`
* `/v1/tigo/mobile/co/customer/`

The methods are designed for each business unit mobile and home, in this proposal are defined call by subscribers (MSISDN) for mobile and account id for home. in the case that the business unit is not especified.


**Version:** 1.0

**Contact information:**  
Armando Umerez  
http://www.millicom.com  
armando.umerez@millicom.com  

**License:** [MIT](https://github.com/apiaryio/polls-api/blob/master/LICENSE)

### /catalog/subscribers/{MSISDN}/recomendedplans/
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

### /catalog/subscribers/{MSISDN}/currentplan
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

### /customer/subscribers/{MSISDN}/insights
---
##### ***GET***
**Summary:** Get Insights Customer by id

**Description:** Retrieve the insight calculated about Customer

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| MSISDN | path | International Identifiable mobile phone number | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested Current Plan Information was found | [Insights](#insights) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `Favorites Number List` was not found | [errorBody](#errorbody) |
| default | unexpected error | [errorBody](#errorbody) |

### /customer/contracts/{contractId}/contactinformation
---
##### ***GET***
**Summary:** Get ContactInformation by contractId

**Description:** Return information the contact that matches the provided contractId


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contractId | path | Unique identifier for the contract that may combine multiple services into one invoice | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Customer contact Info for the provided customerId were found | [CustomerDetailInfo](#customerdetailinfo) |
| 403 | Forbidden. Check `error.message` for details | [errorBody](#errorbody) |
| 404 | the specified `customerId` was not found | [errorBody](#errorbody) |
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

### Models
---

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
| rank | number | This value is used to present the offers in a sorted order. | No |
| productOfferingList | [ [ProductOffering](#productoffering) ] | An array of offering details grouped by category | No |

### Insights  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| churnRiskCategory | string | This is the risk of churn of user categorized | Yes |
| churnRiskValue | number | This is the risk of churn of user in the exact | Yes |
| monthsAsCustomer | number | The time in month that user have Tigo service | Yes |
| dataAverageConsumptionInMB | number | The data average usage in MB of the determined period | No |
| amountAverageConsumption | number | The amount in money that the user spent in the period | No |
| lifeCycleSegment | string | This data is the | Yes |
| contractEndDate | string | The expiration date of the contractin in ISO 8601 format | Yes |
| dataUsage | string | Is the state calculated in exacaster, this is an Enum | Yes |
| recomendedAction | string | The category of the recomended action in this moment only can be Retention, Mantenimiento and Upsell | No |
| resourceConsumptionList | [resourceConsumptionList](#resourceconsumptionlist) |  | No |

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

### resourceConsumptionList  

An array of the resources consumption in the period of months

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| resourceConsumptionList | array | An array of the resources consumption in the period of months |  |

### resourceConsumption  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| period | string | The month of the period of billing system | No |
| dataInPlan | number | The total of MegaBytes in the actual plan | Yes |
| dataUsed | number | The total of MegaBytes the user use in these period | Yes |
| dataAdded | number | The total of MegaBytes is data in the actual plan plus the topups in the month | Yes |
| amountInPlan | number | The price of the plan that user use in the period | Yes |
| amountUsed | number | The amount in money that the user spent in the period | Yes |
| amountAdded | number | The total of the balance purchased in the period sumatory of the plan price and topups | Yes |

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

### Address  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| streetAddress | string | the main street address | Yes |
| streetAddressLine2 | string | optional additional information about address like suite or floor number | No |
| stateId | string | Unique Identifier for State, Province or Department of the address. Numeric or two letter depending on each database. | No |
| stateName | string | Name of the State, Province or Department of the address | No |
| districtId | integer | Unique Identifier for County, Municipality, Town, District, Sector or Neighborhood | No |
| districtName | string | Name of the County, Municipality, Town, District, Sector or Neighborhood | No |
| cityId | integer | Unique Identifier for City associated with the address | No |
| cityName | string | Name of the City associated with the address | No |
| countryId | string | Unique Identifier for Name of the country using ISO Alpha-2 | No |
| countryName | string | Name of the country | No |
| zoneId | integer | Identifier for the internal zone | No |
| stratumId | integer | Identifier for social stratum | No |

### CustomerInfo  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| customerId | string | Customer unique identifier, usually national identification number or company tax payer number | Yes |
| documentType | string | Defines if customerId es a National Id, Tax Payer Number, Passport, etc. | No |
| name | string | First Name, Comapny Name or Full Name of the Customer | No |
| lastName | string | Last Name of the Custoemr | No |
| email | string | Email of the customer | No |
| phoneNumber | string | Preferred contact phone number for the customer | No |
| checksum | string | Some countries may have an additional digit for validating integrity of the customerId. | No |

### CustomerDetailInfo  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| name | string | First Name, Comapny Name or Full Name of the Customer | No |
| lastName | string | Last Name of the Customer | No |
| Address | [Address](#address) |  | No |
| checksum | string | Some countries may have an additional digit for validating integrity of the customerId. | No |
| customerEmailList | [CustomerEmailList](#customeremaillist) |  | No |
| customerPhoneList | [CustomerPhoneList](#customerphonelist) |  | No |
| customerIdentificationList | [ [CustomerIdentification](#customeridentification) ] |  | No |

### CustomerEmailList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| CustomerEmailList | array |  |  |

### CustomerPhoneList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| CustomerPhoneList | array |  |  |

### CustomerIdentification  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| documentType | string | Defines if customerId is a National Id, Tax Payer Number, Passport, etc. | No |
| customerId | string | Customer unique identifier, usually national identification number or company tax payer number | No |

### CustomerEmail  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| email | string | Emails of customer. | No |
| validated | boolean | True if the email was validated. False is not validated yet. | No |

### CustomerPhone  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| phoneType | string | Defines if the phone is a home phone, work phone,mobile, etc. | No |
| phone | string | Customer telephone | No |
| validated | boolean | True if the phone number was validated. False is not validated yet. | No |

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

### errorBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| code | integer |  | Yes |
| message | string |  | Yes |

### successBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| response | string | Generic response from platform. May be ommited. | No |
| message | string | Success Message from platform. May be ommited. | No |