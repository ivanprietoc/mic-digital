Internet Usage Data
===================
This is the standard API for Internet Usage Data for Tigo. 
We use swagger-2.0 specification


**Version:** 1.0.0

**Terms of service:**  
http://swagger.io/terms/

**Contact information:**  
Jose Colman  
https://edge.com.py/  
jose.colman@edge.com.py  

**License:** [MIT](http://github.com/gruntjs/grunt/blob/master/LICENSE-MIT)

### /subscribers/{msisdn}/usage/data/hourlybyapp
---
##### ***GET***
**Summary:** Obtain a list of consumed services per hour.

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

### /subscribers/{msisdn}/usage/data/percentagebyapp
---
##### ***GET***
**Summary:** Obtain a list of consumed services percentage.

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

### Models
---

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