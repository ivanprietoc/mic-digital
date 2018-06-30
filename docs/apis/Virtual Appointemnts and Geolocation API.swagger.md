Virtual Appointemnts and Geolocation API
========================================
This is the standard API for Self Care functions related virtual appointments and stores geolocation services for Tigo. 
We use swagger-2.0 specification


**Version:** 1.0.0

**Terms of service:**  
http://swagger.io/terms/

**Contact information:**  
Jose Colman  
https://edge.com.py/  
jose.colman@edge.com.py  

**License:** [MIT](http://github.com/gruntjs/grunt/blob/master/LICENSE-MIT)

### /appointments/{queueType}
---
##### ***GET***
**Summary:** Get Appointments by queueType

**Description:** Returns a list of appointment types.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| queueType | path | Allowed values CALENDAR and FIFO | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Appointments associated with provided queueType were found | [AppointmentList](#appointmentlist) |
| 400 | Invalid Parameters | [proxyError](#proxyerror) |
| default | unexpected error | [error](#error) |

### /stores/{idAppointmentType}
---
##### ***GET***
**Summary:** Get a list of stores by AppointmentType

**Description:** Returns a list of stores with their basic information that matches the corresponding AppointmentType

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| idAppointmentType | path | Id of the Appointment Type. | Yes | string |
| nameStore | query | The name of the Store that needs to be fetched. | No | string |
| addressStore | query | The address of the Store that needs to be fetched. | No | string |
| city | query | The schedules of the Store that needs to be fetched. | No | string |
| state | query | The state of the Store that needs to be fetched. | No | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested Store list was found | [storeList](#storelist) |
| 400 | Invalid Parameters | [proxyError](#proxyerror) |
| default | unexpected error | [error](#error) |

### /stores/{idAppointmentType}/nearest
---
##### ***GET***
**Summary:** Get a list of stores by AppointmentType and geolocation

**Description:** Returns a list of stores with their basic information based on the location of the user that matches the corresponding AppointmentType

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| idAppointmentType | path | Id of the Appointment Type. | Yes | string |
| currentLatitude | query | The current latitude coordinate of the customer. | Yes | string |
| currentLongitude | query | The current longitude coordinate of the customer. | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Requested Store list was found | [storeList](#storelist) |
| 400 | Invalid Parameters | [proxyError](#proxyerror) |
| default | unexpected error | [error](#error) |

### /appointments/{msisdn}
---
##### ***POST***
**Summary:** Create a new customer appointment

**Description:** Create a new customer appointment

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | MSISDN of the customer. | Yes | string |
| body | body | body | Yes | [CreateCustomerAppointmentRequest](#createcustomerappointmentrequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | Appointment successfully created | [Appointment](#appointment) |
| 400 | Invalid Parameters | [proxyError](#proxyerror) |
| 404 | the specified `msisdn` was not found | [error](#error) |
| default | unexpected error | [error](#error) |

### Models
---

### AppointmentList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| AppointmentList | array |  |  |

### AppointmentType  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| idAppointmentType | string | Unique Identifier for the AppointmentType | No |
| name | string | Name of the AppointmentType | No |
| description | string | Description of the AppointmentType | No |

### storeList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| storeList | array |  |  |

### store  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| geoStoreId | string | Unique Identifier for the geoStore | No |
| storeId | string | Unique Identifier for the store | No |
| name | string | Name of the store | No |
| zipCode | string | Zipcode of the store | No |
| address | string | Address of the store | No |
| city | string | Used to show the agency schedules | No |
| state | string | Country of the store | No |
| latitude | string | Latitude coordinate of the store | No |
| longitude | string | Longitude coordinate of the store | No |
| estimatedWaitingTime | string | Estimated waiting time for the store | No |
| waitingCount | string | Waiting count for the store | No |

### Appointment  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| appointmentId | string | Unique Identifier for the Appointment | No |
| calendarId | string | Unique Identifier for the calendar | No |
| caseId | string | Unique Identifier for the case. | No |
| processId | string | Unique Identifier for the process | No |
| ticketNumber | string | Ticket number for the appointment | No |

### error  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| errorType | string |  | No |
| code | integer |  | No |
| description | string |  | No |
| reason | string |  | No |

### proxyError  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| statusCode | integer |  | No |
| message | string |  | No |
| developerMessage | string |  | No |

### CreateCustomerAppointmentRequest  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| firtsName | string |  | Yes |
| secondName | string |  | Yes |
| email | string |  | Yes |
| appointmentDate | string |  | Yes |
| idAppointmentType | string | Unique identifier of AppointmentType | Yes |
| idStore | string |  | Yes |