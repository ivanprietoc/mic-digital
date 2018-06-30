tigo_b2b_co_selfcare_crm_v2
===========================
Standard API related to CRM for Colombia B2B services


**Version:** 2.0.0

**Terms of service:**  
http://swagger.io/terms/

**Contact information:**  
Carlos Carvallo  
https://edge.com.py  
carlos.carvallo@edge.com.py  

**License:** [MIT](http://github.com/gruntjs/grunt/blob/master/LICENSE-MIT)

### Security
---
**application**  

|oauth2|*OAuth 2.0*|
|---|---|
|Token URL|https://test.api.tigo.com/oauth/client_credential/accesstoken?grant_type=client_credentials|
|Flow|application|
|**Scopes**||
|read|customer accounts|

### /accounts
---
##### ***GET***
**Summary:** Consulta Cuentas ATP Corporativo por Numero Doc

**Description:** Consulta de cuentas Atp Corporativo por n�mero de documento (NIT)

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| idType | query | Identifier Type of the Identification Number | Yes | string |
| id | query | Identification Number | Yes | integer |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Succesful Response | [accountsResponse](#accountsresponse) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unathorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /accounts/{accountId}
---
##### ***GET***
**Summary:** Consulta cliente ATP Corporativo por su ID

**Description:** Consulta de detalle de una cuenta (contrato) Atp Corporativo por id de cuenta

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| accountId | path | Account Identification Number | Yes | integer |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Succesful Response | [accountsDetailsResponse](#accountsdetailsresponse) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unathorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /accounts/{accountId}/profiles
---
##### ***GET***
**Summary:** Consulta de perfiles de un cliente ATP Corporativo por ID

**Description:** Consulta de perfiles de una cuenta ATP Corporativo buscando por un id de cuenta

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| accountId | path | Account Identification Number | Yes | integer |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Succesful Response | [profilesResponse](#profilesresponse) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unathorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /accounts/profiles/{profileId}
---
##### ***GET***
**Summary:** Detalle de un perfil ATP Corporativo por ID

**Description:** Consulta de detalle de un perfil buscando por su id de perfil

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| profileId | path | Profile Identification Number | Yes | integer |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Succesful Response | [profilesDetailsResponse](#profilesdetailsresponse) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unathorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /accounts/profiles/{profileId}/lines
---
##### ***GET***
**Summary:** Consulta Lineas asociadas a un Profile por ID

**Description:** Consulta de las l�neas asociadas a un perfil, buscando por un id de perfil

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| profileId | path | Profile Identification Number | Yes | integer |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Succesful Response | [linesResponse](#linesresponse) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unathorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /accounts/profiles/{profileId}/services
---
##### ***GET***
**Summary:** Consulta planes/servicios asociados al perfil por ID

**Description:** Consulta de los servicios/planes de un perfil Atp Corporativo, buscando por el id perfil

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| profileId | path | Profile Identification Number | Yes | integer |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Succesful response | [servicesResponse](#servicesresponse) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unathorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /accounts/profiles
---
##### ***GET***
**Summary:** Consulta detalle l�nea asociada a ATP Corporativo por Msisdn

**Description:** Consulta de informaci�n de una l�nea Atp Corporativo, buscando por su MSISDN

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | query | Customers MSISDN | Yes | integer |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Succesful response | [linesDetailsResponse](#linesdetailsresponse) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unathorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /documents/{documentId}
---
##### ***GET***
**Summary:** Returns the url of the digital document for massive and corporate clients.

**Description:** Taking as initial parameter the client id returns the url of the digital document for massive and corporate clients.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| documentId | path | Is the document number. | Yes | integer |
| movil | query | Msisdn to consult. | Yes | integer |
| segment | query | Segment to consult can be one of the CORPORATE / MASIVE values. | No | string |
| document | query | Corresponds to the id of the document found in computer. | No | string |
| additional | query | Additional parameters. | No | string |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [documents](#documents) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /customers/{nit}/portfolio
---
##### ***GET***
**Summary:** Obtain the Unified Communications sites of the clients and their respective extensions, taking the nit as the initial parameter.

**Description:** Taking as initial parameter the client's nit returns the Unified Communications sites and their respective extensions.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| nit | path | It's the customer's nit. | Yes | integer |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [portfolioList](#portfoliolist) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /lines/recordings
---
##### ***POST***
**Summary:** Get the recordings generated for the client extensions for a defined period of time.

**Description:** Defining a period of time obtains the generated recordings for the client extensions.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| recordingsParameters | body | Parameters required to obtain the generated recordings for the client extensions for a defined period of time | Yes | [recordingsParameters](#recordingsparameters) |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [recordingsList](#recordingslist) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /calls/{idFormat}/{idCall}/recordings
---
##### ***GET***
**Summary:** It allows to download the recordings that have been generated on the calls of the customer extensions.

**Description:** Taking as the initial parameter the id of the call download the recordings of the client extensions.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| idCall | path | It's the call's id. | Yes | integer |
| idFormat | path | It's the call's format. | Yes | integer |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [callsList](#callslist) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /calls/{idCall}/recordings
---
##### ***GET***
**Summary:** It allows to erase the generated recordings on the calls of the extensions of the client.

**Description:** Taking as the initial parameter the id of the call allows you to erase the recordings generated on that call.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| idCall | path | It's the call's id. | Yes | integer |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [recordings](#recordings) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /customers/{MSISDN}/calls/details
---
##### ***GET***
**Summary:** Find the detail of the calls taking the msisdn as the initial parameter.

**Description:** Returns the detail of the calls made from the msisdn.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| MSISDN | path | Customers MSISDN | Yes | integer |
| dateFrom | query | Date of start | Yes | string |
| dateTill | query | Date of end | Yes | integer |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [details](#details) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /profiles/{profileId}/services
---
##### ***POST***
**Summary:** Operation that receives a list of services / packages to add to a profile.

**Description:** To add to a profile, the operation that receives a list of services / packages .

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| profileId | path | Profile Identification Number | Yes | integer |
| postServicesParameters | body | Parameters needed to add a perfil | Yes | [servicesParameters](#servicesparameters) |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [servicesList](#serviceslist) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /profiles/{profileId}
---
##### ***DELETE***
**Summary:** Operation that receives a list of services / packages to remove to a profile.

**Description:** To remove to a profile, the operation that receives a list of services / packages.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| profileId | path | Profile Identification Number | Yes | integer |
| deleteServicesParameters | body | Parameters needed to remove a perfil | Yes | [servicesParameters](#servicesparameters) |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [servicesList](#serviceslist) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /profile/{profileId}
---
##### ***PUT***
**Summary:** Operation that receives a list of services / packages to update to a profile.

**Description:** To update to a profile, the operation that receives a list of services / packages.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| profileId | path | Profile Identification Number | Yes | integer |
| updateServicesParameters | body | Parameters needed to update a perfil | Yes | [updateServicesParameters](#updateservicesparameters) |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [servicesList](#serviceslist) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /services/{partnum}
---
##### ***GET***
**Summary:** Operation that receives as input parameter the partnum of a service / package and returns the information of the consulted package.

**Description:** It returns the information of the consulted package, receiving as the input parameter the name of a service / package.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| partnum | path | Customer Document | Yes | integer |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [getServicesList](#getserviceslist) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /accounts/{accountId}/processes
---
##### ***POST***
**Summary:** Process secondary transactions necessary to complete the purchase process.

**Description:** Performs the processing of secondary transactions necessary to complete the purchase process.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| accountId | path | Account Identification Number | Yes | integer |
| postAccountsParameters | body | Parameters needed to process secondary transactions necessary to complete the purchase | Yes | [postAccountsParameters](#postaccountsparameters) |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [servicesList](#serviceslist) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### Models
---

### servicesParameters  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| serviceCollection | [ [service](#service) ] |  | No |

### service  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| partnum | string |  | No |

### updateServicesParameters  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| service | [ [serviceList](#servicelist) ] |  | No |

### serviceList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | integer |  | No |
| partnum | string |  | No |

### postAccountsParameters  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| consultantId | integer |  | No |

### servicesList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| payload | string |  | No |
| msgCode | string |  | No |
| description | string |  | No |
| severity | string |  | No |

### getServicesList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| payload | string |  | No |
| service | object |  | No |

### details  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| msisdn | integer |  | No |
| company | string |  | No |
| callType | string |  | No |
| callFrom | string |  | No |
| callDateTime | dateTime |  | No |
| callDuration | integer |  | No |
| airTime | integer |  | No |
| airAmount | string |  | No |
| interconnectionTime | integer |  | No |
| interconnectionAmount | string |  | No |
| callAmount | string |  | No |

### portfolioList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| portfolioList | array |  |  |

### extensions  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| number | integer |  | No |
| recording | string |  | No |
| name | string |  | No |

### recordingsParameters  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| extensions | [ integer ] |  | No |
| start | dateTime |  | No |
| end | dateTime |  | No |
| direction | string |  | No |

### recordingsList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| recordingsList | array |  |  |

### callsList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| weight | integer |  | No |
| route | string |  | No |

### recordings  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| message | string |  | No |
| code | integer |  | No |

### documents  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| url | string | Url of the digital document (Contract) found on the Computec platform in pdf format. | No |

### accountsResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| accountCollection | [ object ] |  | No |

### accountsDetailsResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| accountId | string |  | No |
| accountName | string |  | No |
| billingAccount | string |  | No |
| consultantName | string |  | No |
| contactName | string |  | No |
| contactPhone | string |  | No |
| contractCollection | [ object ] |  | No |
| cycle | string |  | No |
| documentNumber | string |  | No |
| email | string |  | No |
| imsi | string |  | No |
| msisdn | string |  | No |
| parentAccountId | string |  | No |
| parentName | string |  | No |

### profilesResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| profileCollection | [ object ] |  | No |

### profilesDetailsResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| documentNumber | string |  | No |
| value | integer |  | No |
| totalValue | integer |  | No |
| accountId | string |  | No |
| billingAccount | string |  | No |
| billingAccountFather | string |  | No |
| cycle | integer |  | No |
| description | string |  | No |
| id | string |  | No |
| imsi | string |  | No |
| lineCollection | [ object ] |  | No |
| linesAmount | string |  | No |
| msisdn | string |  | No |
| msisdnFather | string |  | No |
| name | string |  | No |
| serviceCollection | [ object ] |  | No |
| servicesAmount | string |  | No |
| status | string |  | No |

### linesResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| lineCollection | [ object ] |  | No |

### servicesResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| serviceCollection | [ object ] |  | No |

### linesDetailsResponse  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| account | object |  | No |
| contractCollecion | [ object ] |  | No |
| msisdn | string |  | No |
| profileList | [ object ] |  | No |

### errorBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error | object |  | No |