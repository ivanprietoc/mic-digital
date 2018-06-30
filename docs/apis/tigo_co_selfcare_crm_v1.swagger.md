tigo_co_selfcare_crm_v1
=======================
This is a standard Api for CO B2B and B2C Selfcare CRM 


**Version:** 2.0.0

**Terms of service:**  
http://swagger.io/terms/

**Contact information:**  
Andrea Forneron  
https://edge.com.py  
andrea.forneron@edge.com.py  

**License:** [MIT](http://github.com/gruntjs/grunt/blob/master/LICENSE-MIT)

### Security
---
**application**  

|oauth2|*OAuth 2.0*|
|---|---|
|Token URL|https://test.api.tigo.com/oauth/client_credential/accesstoken?grant_type=client_credentials|
|Flow|application|
|**Scopes**||
|read|Customer CRM|

### /customers/{idType}/{id}/damages/causes
---
##### ***GET***
**Summary:** Find the list of damages for common causes taking the customer's document as the initial parameter.

**Description:** Taking the customer's document as the initial parameter, return the list of damages for common causes

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | Customer Document | Yes | integer |
| idType | path | Type of Customer Document | Yes | string |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [detailsCauses](#detailscauses) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /services/{idService}
---
##### ***POST***
**Summary:** Executes automatic diagnostic tests of standard services taking the service id as the initial parameter.

**Description:** Taking as initial parameter the id of the service executes automatic tests of diagnosis of standard services.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| idService | path | Id of Service | Yes | integer |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [detailsServices](#detailsservices) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /test/{idTest}/reports
---
##### ***GET***
**Summary:** Find the query on a specific integrated test taking the id of the test as the initial parameter.

**Description:** Taking as the initial parameter the id of the test, find the query on a specific integrated test

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| idTest | path | Id of Test | Yes | integer |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [detailsReports](#detailsreports) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /damages
---
##### ***POST***
**Summary:** Creates damage that will be taken care of by tigoune.

**Description:** Taking initial parameters creates damage that will be addressed by tigoune.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| damagesParameters | body | Parameters necessary to create damages | Yes | [damagesParameters](#damagesparameters) |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [detailsDamages](#detailsdamages) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /quotas/availables
---
##### ***POST***
**Summary:** Returns the available quotas taking the SR number as the initial parameter.

**Description:** Taking the SR number as initial parameter, returns the available spaces.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| queryQuotasParameters | body | Parameters needed to perform the agenda query | Yes | [queryQuotasParameters](#queryquotasparameters) |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [queryQuotasList](#queryquotaslist) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /quotas
---
##### ***POST***
**Summary:** Allow cancellation of the agenda by taking additional parameters.

**Description:** Taking additional parameters, It allows the cancellation of the scheduled technical visit.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| cancellQuotasParameters | body | Parameters needed to cancel the technical visit reservation | Yes | [cancellQuotasParameters](#cancellquotasparameters) |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [cancellQuotasList](#cancellquotaslist) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### /quotas/reservations
---
##### ***POST***
**Summary:** It allows to make the reservation of the technical visit.

**Description:** It allows to register the technical visit reservation in the agenda.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| reservationQuotasParameters | body | Parameters needed to book a technical visit | Yes | [reservationQuotasParameters](#reservationquotasparameters) |
| Authorization | header | Access Token provided by the Authorization Url | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Successful response | [reservationQuotasList](#reservationquotaslist) |
| 400 | Bad Request. | [errorBody](#errorbody) |
| 401 | Unauthorized. | [errorBody](#errorbody) |
| 404 | Not Found. | [errorBody](#errorbody) |
| default | Unhandled resource | [errorBody](#errorbody) |

### Models
---

### queryQuotasParameters  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| wsFlag | string |  | No |
| srNumber | string |  | No |

### cancellQuotasParameters  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| wsFlag | string |  | No |
| spcId | object |  | No |

### reservationQuotasParameters  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| wsFlag | string |  | No |
| activityId | string |  | No |
| tipoFranja | string |  | No |
| descripcion | string |  | No |
| agendaId | integer |  | No |
| horaFinal | string |  | No |
| horaInicial | string |  | No |
| fechaFinal | date |  | No |
| cantidadAgendada | integer |  | No |
| objectId | string |  | No |
| areaTrabajo | string |  | No |
| agenda | integer |  | No |
| number | string |  | No |
| areaOperativa | string |  | No |
| grupoCupo | integer |  | No |
| subZona | string |  | No |
| disponible | string |  | No |
| pedido | string |  | No |
| fechaInicial | date |  | No |
| fechaOrden | date |  | No |
| capacidadMaxima | string |  | No |

### queryQuotasList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| errorSpecificCode | string |  | No |
| errorSpecificMessage | string |  | No |
| availableAgendaList | [ [availableAgenda](#availableagenda) ] |  | No |

### availableAgenda  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| subzonaId | string |  | No |
| activitySrId | string |  | No |
| idAgenda | integer |  | No |
| idGrupoCupo | integer |  | No |
| idOrderGTC | integer |  | No |
| integrationId | integer |  | No |
| areaOperativaId | string |  | No |
| areaTrabajoId | string |  | No |
| fechaFinal | date |  | No |
| fechaOrden | date |  | No |
| horaFinal | string |  | No |
| horaInicial | string |  | No |
| tipoFranja | string |  | No |

### cancellQuotasList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| errorSpecificCode | string |  | No |
| errorSpecificMessage | string |  | No |

### reservationQuotasList  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| errorSpecificCode | string |  | No |
| errorSpecificMessage | string |  | No |

### damagesParameters  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| measuringElement | string |  | No |
| description | string |  | No |
| mobile | integer |  | No |
| rootCause | string |  | No |
| symptomCode | string |  | No |

### detailsDamages  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| status | integer |  | No |
| code | string |  | No |
| userMessage | string |  | No |
| technicalMessage | string |  | No |
| dataResponse | dateTime |  | No |
| contentCollection | [contentDamages](#contentdamages) |  | No |

### contentDamages  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| cun | string |  | No |
| errorSpecificCode | string |  | No |
| errorSpecificMessage | string |  | No |
| objectSpecificId | string |  | No |
| srNumber | string |  | No |
| serviceRequestCollection | [ [servicesArray](#servicesarray) ] |  | No |

### servicesArray  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| measuringElement | string |  | No |
| accountId | string |  | No |
| contactId | string |  | No |
| rootCause | string |  | No |
| ticketType | string |  | No |
| description | string |  | No |
| mobile | integer |  | No |

### detailsCauses  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| userMessage | string |  | No |
| technicalMessage | string |  | No |
| dataResponse | dateTime |  | No |
| contentCollection | [content](#content) |  | No |

### content  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| errorSpecificCode | string |  | No |
| errorSpecificMessage | string |  | No |
| assetManagementCollection | [ [assetManagement](#assetmanagement) ] |  | No |

### assetManagement  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| productName | string |  | No |
| serviceId | string |  | No |
| infoCollection | [ [uneSRCCCInfo](#unesrcccinfo) ] |  | No |

### uneSRCCCInfo  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| commitTime | string |  | No |
| integrationId | integer |  | No |
| srNumber | string |  | No |
| status | string |  | No |
| subType | string |  | No |
| effectiveDate | dateTime |  | No |

### detailsServices  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| userMessage | string |  | No |
| technicalMessage | string |  | No |
| dataResponse | dateTime |  | No |
| contentCollection | [contentServices](#contentservices) |  | No |

### contentServices  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| statusTest | string |  | No |
| startDateTest | dateTime |  | No |
| endDateTest | dateTime |  | No |
| idTest | integer |  | No |
| diagnostic | string |  | No |
| diagnosticDescription | string |  | No |
| results | [ [resultsArray](#resultsarray) ] |  | No |

### detailsReports  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| status | integer |  | No |
| code | string |  | No |
| userMessage | string |  | No |
| technicalMessage | string |  | No |
| dataResponse | dateTime |  | No |
| contentCollection | [contentReports](#contentreports) |  | No |

### contentReports  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| statusTest | string |  | No |
| startDateTest | dateTime |  | No |
| endDateTest | dateTime |  | No |
| idTest | integer |  | No |
| diagnostic | string |  | No |
| diagnosticDescription | string |  | No |
| results | [ [resultsArray](#resultsarray) ] |  | No |

### resultsArray  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| unitTest | string |  | No |
| result | string |  | No |
| diagnostics | [ [diagnosticsArray](#diagnosticsarray) ] |  | No |

### diagnosticsArray  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| category | string |  | No |
| diagnosticCode | string |  | No |
| automaticFix | string |  | No |
| clientDescription | string |  | No |

### errorBody  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error | object |  | No |