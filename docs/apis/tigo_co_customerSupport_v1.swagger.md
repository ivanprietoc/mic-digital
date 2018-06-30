tigo_co_customerSupport_v1
==========================
This is the Standard API related to Customer Support in version 1


**Version:** 0.0.1

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
|read|collections of tasks for repairment|

### /subscribers/{msisdn}/claims
---
##### ***GET***
**Summary:** Get PQR by Subscriber's MSISDN

**Description:** Permite consultar las solicitudes asociadas a un **n�mero de l�nea de cliente**, la API acepta el formato internacional o local, es el valor esperado por defecto.


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| msisdn | path | Customer's MSISDN | Yes | number |
| lastMonths | query | Number of last months required | No | number |
| Authorization | header | Access Token provided according to the Developer App | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Succesful response | [ListaDeSolicitudes](#listadesolicitudes) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unathorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /subscribers/{idType}/{identification}/claims
---
##### ***GET***
**Summary:** Get PQR by Subscriber's Identification

**Description:** Permite consultar _PQRs_ asociadas al n�mero de **identificaci�n de cliente** y el **tipo de identificacion.** Los tipos de Id aceptados son CC, NIT de otra manera la API respondera con un 400 _Bad Request_.


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| idType | path | Document Type | Yes | string |
| identification | path | Customer Identification number | Yes | number |
| lastMonths | query | Number of last months required | No | number |
| Authorization | header | Access Token provided according to the Developer App | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Succesful response | [ListaDeSolicitudes](#listadesolicitudes) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unathorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /claims/{idType}/{identification}
---
##### ***GET***
**Summary:** Get PQR by Claim's Identification

**Description:** Permite consultar _PRQs_ asociadas a la **identificacion del reclamo** y el **tipo de identificacion.** El formato esperado del CUN Id es: los 4 primeros digitos son el codigo de la empresa, guion, dos digitos que representan al a�o, guion, el numero consecutivo.


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| idType | path | Claim Id Type (CUN), etc | Yes | string |
| identification | path | Claim Id identification | Yes | string |
| lastMonths | query | Number of last months required | No | number |
| Authorization | header | Access Token provided according to the Developer App | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Succesful response | [Solicitud](#solicitud) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unathorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /suscribers/{idType}/{id}/devices
---
##### ***GET***
**Summary:** Find Subscribers devices under repair by the Subscriber Id

**Description:** This feature returns a Collection of Subscriber Devices that are under repair through the Subscriber Id, optionally it can be filtered by the ServiceOrder


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | Identifier of the Customer | Yes | integer |
| idType | path | Identifier type related to the Identification Number of the Customer | Yes | string |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |
| ods | query | Is the service order number. | No | integer |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response. | [devices](#devices) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource. | [errorBody](#errorbody) |

### /devices/{idType}/{id}
---
##### ***GET***
**Summary:** Find Devices by the Imei or the Service Order

**Description:** This feature returns a Collection of Devices that are under repair through the IMEI or the ServiceOrder

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| idType | path | Identifier type related to the Identification Number of the Customer | Yes | string |
| id | path | Identifier of the Customer | Yes | integer |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response. | [devices](#devices) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource. | [errorBody](#errorbody) |

### Models
---

### ListaDeSolicitudes  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| ListaDeSolicitudes | array |  |  |

### Solicitud  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| numberCUN | string | The number CUN is the legal number for issues to report in the national system | No |
| numberTicket | number | Unique number in the system. This number is generated in the country. | No |
| nameUser | string | The name the user register in the ticket. | No |
| typeDocumentUser | string | Type of document used to identify the user in the Colombian case the option can be CC or NIT can  number in the system. This number is generated in the country. | No |
| numberDocumentUser | number | The number of the legal document that belongs the | No |
| msisdn | number | Msisdn of the customer | No |
| emailUser | string | Unique number in the system. This number is generated in the country. | No |
| addressUser | string | The address registered for the user in the ticket. | No |
| typeRequest | string | Unique number in the system. This number is generated in the country. | No |
| subtypeRequest | string | Is the description of the user about the ticket. | No |
| classApplication | string | This is the type of PQR. | No |
| reason | string | Is the description of the user about the ticket. | No |
| radicationDate | string | This is the date of the creation of the ticket. | No |
| expirationDate | string | This is the date of the expiration of the ticket. | No |
| subState | string | Description of the state with details in the priorization. | No |
| state | string | General status of the ticket . | No |
| stateCun | string | Description of the state with details in the priorization of the ticket | No |
| meanInput | string | General calsificatin of the ticket. | No |
| channelInput | string | Specify the clasification of the ticket. | No |
| descriptionRequest | string | Is the description of the user about the ticket. | No |
| urlsPdf | object |  | No |

### devices  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | integer |  | Yes |
| idType | string |  | Yes |
| authorization | string |  | Yes |
| dateOrder | string |  | No |
| subscriberName | string |  | No |
| phone | string |  | No |
| email | string |  | No |
| city | string |  | No |
| placeReceipt | string |  | No |
| ods | integer |  | No |
| imei | integer |  | No |
| model | string |  | No |
| accessories | string |  | No |
| failure | string |  | No |
| reentry | integer |  | No |
| status | string |  | No |

### errorBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error | object |  | No |