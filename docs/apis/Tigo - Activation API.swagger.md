Tigo - Activation API
=====================
Administraci�n de servicios activados

**Version:** 1.0.0

### /subscribers/{msisdn}/services/{service}
---
##### ***GET***
**Description:** Permite consultar informacion de servicios activados a un suscriptor

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| Authorization | header | API key | Yes | string |
| msisdn | path | N�mero del suscriptor | Yes | string |
| service | path | Servicio a consultar | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Datos de activaci�n del servicio | [ [Service](#service) ] |
| 401 | Error de autenticaci�n | [Error](#error) |
| 404 | El recurso solicitado no existe. | [Error](#error) |
| 503 | No hay comunicacion con el servicio. | [Error](#error) |

### Models
---

### Service  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| state | string | Estado de la activaci�n | No |
| simEnabled | boolean | Indica si la sim est� habilitada para el servicio | No |
| deviceEnabled | boolean | Indica si el dispositivo est� habilitado para el servicio | No |

### Error  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| errorType | integer | Indica el tipo de error, posibles valores COM (Comunicaci�n NEG (Negocio), SEG (Seguridad), INF (Informativo), MSG (Mensaje) | No |
| code | string | C�digo n�merico de error | No |
| reason | string | Mensaje a nivel t�cnico que explica el motivo del error | No |
| description | string | Descripci�n del error. | No |