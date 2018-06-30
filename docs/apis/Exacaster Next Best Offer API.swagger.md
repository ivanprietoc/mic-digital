Exacaster Next Best Offer API
=============================
Exacaster Next Best Offer API

**Version:** 1.0.0

**Contact information:**  
support@exacaster.com  

**License:** [Exacaster](http://www.exacaster.com)

### Security
---
**APIKeyHeader**  

|apiKey|*API Key*|
|---|---|
|In|header|
|Name|X-API-Key|

### /subscription/{subscriptionId}
---
##### ***GET***
**Summary:** Returns a list of Next Best Offers for specified Subscription

**Description:** Returns list of Next Best Offers for specified Subscription

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| subscriptionId | path | Subscription ID (MSISDN) to get NBO for | Yes | string |
| channel | query | Requesting channel | No | string |
| maxPerSubscription | query | Maximum campaigns per subscription | No | integer |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | successful operation | [Response](#response) |
| 400 | Invalid Subscription ID supplied |  |
| 401 | API key missing or invalid |  |
| 404 | msisdn not found or has no offers |  |

### Models
---

### Response  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| interaction_id | string | Interaction ID assigned by Exacaster NBO for tracking | No |
| subscription_id | string | Subscription ID (MSISDN) | No |
| campaigns | [ [Campaign](#campaign) ] |  | No |

### Campaign  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| campaign_id | integer | Campaign ID | No |
| instance_id | integer | Campaign Instance ID. Instance is created for every campaign run attempt | No |
| campaign_priority | integer | Campaign relative priority (1 - highest) | No |
| campaign_tag | string | Campaign tag for reference | No |
| channel_info_valid_from | dateTime | Date and time NBO is valid from | No |
| channel_info_valid_to | dateTime | Date and time NBO is valid to | No |
| channel_agent_info | [ChannelAgentInfo](#channelagentinfo) |  | No |

### CustomerProfile  

Exacaster Customer Profile Metrics and Variables

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| msisdn | string |  | No |
| rate_plan_name | string |  | No |
| rate_plan_VozID | string |  | No |
| rate_plan_DataID | string |  | No |
| rate_plan_price_usd | number |  | No |
| original_rate_plan_data_resources_mb | integer |  | No |
| available_data_resources_mb | integer |  | No |
| rate_plan_name_month_1 | string |  | No |
| rate_plan_VozID_month_1 | string |  | No |
| rate_plan_DataID_month_1 | string |  | No |
| rate_plan_price_usd_month_1 | number |  | No |
| invoice_amount_charged_usd_month_1 | number |  | No |
| original_rate_plan_data_resources_mb_month_1 | integer |  | No |
| available_data_resources_mb_month_1 | integer |  | No |
| data_resources_consumed_mb_month_1 | integer |  | No |
| recharges_amount_usd_month_1 | number |  | No |
| rate_plan_name_month_2 | string |  | No |
| rate_plan_VozID_month_2 | string |  | No |
| rate_plan_DataID_month_2 | string |  | No |
| rate_plan_price_usd_month_2 | number |  | No |
| invoice_amount_charged_usd_month_2 | number |  | No |
| original_rate_plan_data_resources_mb_month_2 | integer |  | No |
| available_data_resources_mb_month_2 | integer |  | No |
| data_resources_consumed_mb_month_2 | integer |  | No |
| recharges_amount_usd_month_2 | number |  | No |
| rate_plan_name_month_3 | string |  | No |
| rate_plan_VozID_month_3 | string |  | No |
| rate_plan_DataID_month_3 | string |  | No |
| rate_plan_price_usd_month_3 | number |  | No |
| invoice_amount_charged_usd_month_3 | number |  | No |
| original_rate_plan_data_resources_mb_month_3 | integer |  | No |
| available_data_resources_mb_month_3 | integer |  | No |
| data_resources_consumed_mb_month_3 | integer |  | No |
| recharges_amount_usd_month_3 | number |  | No |
| avg_monthly_mb_used_90d | integer |  | No |
| avg_recharges_amount_usd_90d | number |  | No |
| lifetime_months | integer |  | No |
| lifecycle_segment | string |  | No |
| churn_risk_segment | string |  | No |
| churn_risk | number |  | No |
| contract_expiration_date | date |  | No |
| data_consumption_segment | string |  | No |
| recommended_action | string |  | No |

### Scenario  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| scenario_type | string | type of scenario. MAIN = suggested by engine, ALTERNATIVE = the rest. | No |
| scenario_priority | integer |  | No |
| scenario_action | string |  | No |
| scenario_offers | [ [NextBestOffer](#nextbestoffer) ] |  | No |

### NextBestOffer  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| offer_priority | integer |  | No |
| recommended_offers_VozID | string |  | No |
| recommended_offers_DataID | string |  | No |
| recommended_offers_name | string |  | No |
| recommend_contract | integer |  | No |
| recommend_subsidy | integer |  | No |

### ChannelAgentInfo  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| customer_profile | [CustomerProfile](#customerprofile) |  | No |
| scenarios | [ [Scenario](#scenario) ] |  | No |