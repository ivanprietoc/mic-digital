Convergent Payment API
======================
From Credit Card Tokenization to Credit Card Processing, this API can be used by any Tigo Web/App to allow users to pay their bills.

**Version:** 1.0.0

**Terms of service:**  
http://swagger.io/terms/

**Contact information:**  
Andres Cavallin  
http://www.millicom.com  
andres.cavallin@millicom.com  

**License:** [MIT](http://github.com/gruntjs/grunt/blob/master/LICENSE-MIT)

### /credit-cards
---
##### ***GET***
**Description:** Returns all credit-cards from the system that the user has access to
Nam sed condimentum est. Maecenas tempor sagittis sapien, nec rhoncus sem sagittis sit amet. Aenean at gravida augue, ac iaculis sem. Curabitur odio lorem, ornare eget elementum nec, cursus id lectus. Duis mi turpis, pulvinar ac eros ac, tincidunt varius justo. In hac habitasse platea dictumst. Integer at adipiscing ante, a sagittis ligula. Aenean pharetra tempor ante molestie imperdiet. Vivamus id aliquam diam. Cras quis velit non tortor eleifend sagittis. Praesent at enim pharetra urna volutpat venenatis eget eget mauris. In eleifend fermentum facilisis. Praesent enim enim, gravida ac sodales sed, placerat id erat. Suspendisse lacus dolor, consectetur non augue vel, vehicula interdum libero. Morbi euismod sagittis libero sed lacinia.
Sed tempus felis lobortis leo pulvinar rutrum. Nam mattis velit nisl, eu condimentum ligula luctus nec. Phasellus semper velit eget aliquet faucibus. In a mattis elit. Phasellus vel urna viverra, condimentum lorem id, rhoncus nibh. Ut pellentesque posuere elementum. Sed a varius odio. Morbi rhoncus ligula libero, vel eleifend nunc tristique vitae. Fusce et sem dui. Aenean nec scelerisque tortor. Fusce malesuada accumsan magna vel tempus. Quisque mollis felis eu dolor tristique, sit amet auctor felis gravida. Sed libero lorem, molestie sed nisl in, accumsan tempor nisi. Fusce sollicitudin massa ut lacinia mattis. Sed vel eleifend lorem. Pellentesque vitae felis pretium, pulvinar elit eu, euismod sapien.


**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| tags | query | tags to filter by | No | [ string ] |
| limit | query | maximum number of results to return | No | integer |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | credit-card response | [ [Credit-card](#credit-card) ] |
| default | unexpected error | [Error](#error) |

##### ***POST***
**Description:** Creates a new credit-card in the store.  Duplicates are allowed

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| credit-card | body | Credit-card to add to the store | Yes | [NewCredit-card](#newcredit-card) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | credit-card response | [Credit-card](#credit-card) |
| default | unexpected error | [Error](#error) |

### /credit-cards/{id}
---
##### ***GET***
**Description:** Returns a user based on a single ID, if the user does not have access to the credit-card

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | ID of credit-card to fetch | Yes | long |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | credit-card response | [Credit-card](#credit-card) |
| default | unexpected error | [Error](#error) |

##### ***DELETE***
**Description:** deletes a single credit-card based on the ID supplied

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | ID of credit-card to delete | Yes | long |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 204 | credit-card deleted |  |
| default | unexpected error | [Error](#error) |

### Models
---

### Credit-card  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| Credit-card |  |  |  |

### NewCredit-card  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| name | string |  | Yes |
| tag | string |  | No |

### Error  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| code | integer |  | Yes |
| message | string |  | Yes |