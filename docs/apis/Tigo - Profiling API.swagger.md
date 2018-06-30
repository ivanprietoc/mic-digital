Tigo - Profiling API
====================
Informaci�n de suscriptores basada en profiling

**Version:** 1.0.0

### /subscribers/{msisdn}/suggestedProducts/{category}
---
##### ***GET***
**Description:** Listado de productos sugeridos por categor�a

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| Authorization | header | API key | Yes | string |
| msisdn | path | N�mero del suscriptor | Yes | string |
| category | path | Servicio a consultar | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Datos de activaci�n del servicio | [ [Product](#product) ] |
| 401 | Error de autenticaci�n | [Error](#error) |
| 404 | El recurso solicitado no existe. | [Error](#error) |
| 503 | No hay comunicacion con el servicio. | [Error](#error) |
| 504 | Timeout en request al servicio legado | [Error](#error) |

### /subscribers/{msisdn}/suggestedProduct
---
##### ***GET***
**Description:** Listado de productos sugeridos

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| Authorization | header | API key | Yes | string |
| msisdn | path | N�mero del suscriptor | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Datos de activaci�n del servicio | [ [Product](#product) ] |
| 401 | Error de autenticaci�n | [Error](#error) |
| 404 | El recurso solicitado no existe | [Error](#error) |
| 503 | No hay comunicacion con el servicio | [Error](#error) |
| 504 | Timeout en request al servicio legado | [Error](#error) |

### Models
---

### Product  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| product | string | C�digo de producto | No |
| category | string | Categor�a del producto | No |

### Error  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| errorType | integer | Indica el tipo de error, posibles valores COM (Comunicaci�n NEG (Negocio), SEG (Seguridad), INF (Informativo), MSG (Mensaje) | No |
| code | string | C�digo n�merico de error | No |
| reason | string | Mensaje a nivel t�cnico que explica el motivo del error | No |
| description | string | Descripci�n del error. | No |