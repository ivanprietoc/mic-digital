Payment Gateway
===============
This the especific description for the API for Regional Payment Gateway. in the swagger-2.0 specification. 

This solution is to meet in all countries of the region, covers the payment needs for different products and applications. The payment gateway will be able to process payments through credit cards, debit card and Tigo Money.

Fulfillment module needs to learn how to provision or deliver the service. For this MVP, consider only two different integrations- Paying for a Mobile Invoice and Paying for a Cable Invoice.

In this section will be summarized all the doubts that are raised with the teams of the different teams to remain with the questions and their respective answers.

The details of the related concepts are described in the following document-

https://millicom-my.sharepoint.com/personal/andres_cavallin_millicom_com/_layouts/15/guestaccess.aspx?guestaccesstoken=JvRZ65J8I9FUZpUwLQRYJWRPu8%2fgVvaA2zUCn0BMm4s%3d&docid=2_121c58b7e6f6043a1a37d9ff3edf9a2d5&rev=1


**Version:** 1.0.0

**Terms of service:**  
http://swagger.io/terms/

**Contact information:**  
Armando Umerez  
http://www.millicom.com  
armando.umerez@millicom.com  

**License:** [MIT](http://github.com/gruntjs/grunt/blob/master/LICENSE-MIT)

### /payment
---
##### ***GET***
**Description:** Returns all pets from the system that the user has access to
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
| 200 | pet response | [ [Pet](#pet) ] |
| default | unexpected error | [Error](#error) |

##### ***POST***
**Description:** Creates a new pet in the store.  Duplicates are allowed

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| pet | body | Pet to add to the store | Yes | [NewPet](#newpet) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | pet response | [Pet](#pet) |
| default | unexpected error | [Error](#error) |

### /pets/{id}
---
##### ***GET***
**Description:** Returns a user based on a single ID, if the user does not have access to the pet

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | ID of pet to fetch | Yes | long |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | pet response | [Pet](#pet) |
| default | unexpected error | [Error](#error) |

##### ***DELETE***
**Description:** deletes a single pet based on the ID supplied

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | ID of pet to delete | Yes | long |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 204 | pet deleted |  |
| default | unexpected error | [Error](#error) |

### Models
---

### Pet  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| Pet |  |  |  |

### NewPet  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| name | string |  | Yes |
| tag | string |  | No |

### Error  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| code | integer |  | Yes |
| message | string |  | Yes |