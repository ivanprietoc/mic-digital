FORMAT: 1A
HOST: https://test.api.tigo.com/v2/tigo

# OpenTIGO - CRM
2nd Gen Tigo API.



# Group Customers
## Customer Information [/mobile/{country}/crm/subscribers/{msisdn}/{?fields,expand}]
### Get a Customer [GET]

The following properties are supported by this API:

####Response Body
- **name**: first name of the customer. if the backend does not discriminate between 
name and last name or if it is a company, _name_ will contain the full name 
- **lastName**: last name of the customer. 
- **phoneNumbers**: (array of **phoneNumber**) list of phone numbers associated to the customer. 
Each **phoneNumber** contains the following attributes:
    - **type**: phone number type: fax, home, mobile, etc. 
    - **number**: phone number. 
- **emailAddresses**: (array of **emailAddress**) list of email addresses associated to the customer. 
Each **emailAddress** contains the following attributes:
    - **email**: the email address of the customer. 
- **links**: (array of **link**) expandable links for the customer object.
The following links are supported and expandable:
    - **contracts**: the contracts associated to the customer
    - **documents**: identification documents of the customer
    - **plans**: plans of the customer. 
    - **raw**: additional (unnormalized) information returned by the country. contents of this array
    may change without further notice. If a field gets normalized (aka 'promoted'), will appear in 
    the formal definition of the method. 


+ Parameters
    + country (required, string) ... country code. see Common Parameters.
    + msisdn (required, string) ... identifier of the contact. `me` and `self` are  acceptable 
    if the request contains an enriched token.
    + fields (optional, string, `fields=name,lastName,phone`) ... comma separated field names 
    that will be included on the response. only scalar attributes are supported. links are 
    excluded from the response. 
    
    + expand (optional, string) 
    
        fields (comma separated) to be expanded to full contents.
        
        + values
            + `documents`
            + `contracts`
            + `plans`
            + `raw`


+ Response 200 (application/json)

    + Body
    
            {
                "name": "Courage",
                "lastName": "the Cowardly Dog",
                "phoneNumbers": [
                    {
                        "type": "main",
                        "number": "021613434"
                    },
                    {
                        "type": "mobile",
                        "number": "595981613434"
                    }
                ],
                "emailAddresses": [
                    {
                        "email": "courage@eustaceandmuriel.com"
                    },
                    {
                        "email": "courage@gmail.com"
                    }
                ],
                "links": [
                    {
                        "documents": "/documents",
                        "contracts" : "/contracts",
                        "plans": "/plans",
                        "raw" : "/raw"
                    }
                ]
            }


#Group Contracts
## Contracts Collection [/mobile/{country}/crm/subscribers/{msisdn}/contracts]
### List Subscriber Contracts [GET]
Obtain a list of contracts associated to the subscriber

The following properties are supported by this API:

####Response Body
- **contracts**: (array of **contract**). list of contracts of the customer.
Each **contract** contains the following attributes:
    - **contract**: number of the contract.
    - **clientCode**: the client internal code.
    - **billingProfile**: (object of type **billingProfile**). billing profile associated to the contract. Contains the following attributes:
        - **id**: the identifier of the billing profile
        - **cycle**: the billing cycle identifier.
        - **invoiceName** : name that will appear on the invoice for this billing profile.
        - **address**: (object of type **address**) billing main address line. Contains the following attributes:
            - **type**: text description of the address type. Always _billing address_
            - **addressLines**: (array of **addressLine**) list of lines of the address.
            - **city**: name of the city.
            - **zip**: zip or postal code if available. 
            - **state**: state where applicable.
            - **province**: province or department where applicable.
            - **country** : ISO 3166-1 alpha-2 country code.

+ Parameters
    + country (required, string) ... country code. see Common Parameters. 
    + msisdn (required, string) ... identifier of the contact. `me` and `self` are  acceptable 
    if the request contains an enriched token.

+ Response 200 (application/json)

    + Body
    
            {
                "contracts": [
                    {
                        "contract": "123456789",
                        "clientCode": "555444333",
                        "billingProfile": {
                            "id": "333341",
                            "cycle": "H",
                            "invoiceName" : "SpongeBob Squarepants",
                            "address": {
                                "type": "billing address",
                                "addressLines": [
                                    {
                                        "line": "1234 Middle of Nowhere"
                                    },
                                    {
                                        "line": "Isolated Farm Creek"
                                    },
                                    {
                                        "line": "apt #2150"
                                    }
                                ],
                                "city": "ASUNCION",
                                "zip": null,
                                "state": null,
                                "province": null,
                                "country": "PY"
                            }
                        }
                    },
                    {
                        "contract": "123456789",
                        "clientCode": "555444333",
                        "billingProfile": {
                            "id": "333341",
                            "cycle": "H",
                            "invoiceName" : "SpongeBob Squarepants",
                            "address": {
                                "type": "billing address",
                                "addressLines": [
                                    {
                                        "line": "1234 Middle of Nowhere"
                                    },
                                    {
                                        "line": "Isolated Farm Creek"
                                    },
                                    {
                                        "line": "apt #2150"
                                    }
                                ],
                                "city": "ASUNCION",
                                "zip": null,
                                "state": null,
                                "province": null,
                                "country": "PY"
                            }
                        }
                    }
                ]
            }


## Contract [/mobile/{country}/crm/subscribers/{msisdn}/contracts/{contractId}]
###Query a Contract [GET]
Obtain a single contract associated to the subscriber

The following properties are supported by this API:

####Response Body
- **contract**: (object of type **contract**). the contract contains the following properties:
    - **contract**: number of the contract.
    - **clientCode**: the client internal code.
    - **billingProfile**: (object of type **billingProfile**). billing profile associated to the contract. Contains the following attributes:
        - **id**: the identifier of the billing profile
        - **cycle**: the billing cycle identifier.
        - **invoiceName** : name that will appear on the invoice for this billing profile.
        - **address**: (object of type **address**) billing main address line. Contains the following attributes:
            - **type**: text description of the address type. Always _billing address_
            - **addressLines**: (array of **addressLine**) list of lines of the address.
            - **city**: name of the city.
            - **zip**: zip or postal code if available. 
            - **state**: state where applicable.
            - **province**: province or department where applicable.
            - **country** : ISO 3166-1 alpha-2 country code.

+ Parameters
    + country (required, string) ... country code. see Common Parameters. 
    + msisdn (required, string) ... identifier of the contact. `me` and `self` are  acceptable 
    if the request contains an enriched token.
    + contractId (required, string) ... the identifier of the contract. 

+ Response 200 (application/json)

    + Body
    
            {
                "contract": "123456789",
                "clientCode": "555444333",
                "billingProfile": {
                    "id": "333341",
                    "cycle": "H",
                    "invoiceName" : "SpongeBob Squarepants",
                    "address": {
                        "type": "billing address",
                        "addressLines": [
                            {
                                "line": "1234 Middle of Nowhere"
                            },
                            {
                                "line": "Isolated Farm Creek"
                            },
                            {
                                "line": "apt #2150"
                            }
                        ],
                        "city": "ASUNCION",
                        "zip": null,
                        "state": null,
                        "province": null,
                        "country": "PY"
                    }
                }
            }


# Group Documents
##Documents Collection [/mobile/{country}/crm/subscribers/{msisdn}/documents]
###List Subscriber Documents [GET]
Obtain a list of identification documents associated to the customer

The following properties are supported by this API:
- **documents**: (array of **document**). list of documents of the customer.
Each **document** contains the following attributes:
    - **type**: text description of the document type. examples are _CI_, _DUI_, _RUC_
    - **number**: the document number.

+ Parameters
    + country (required, string) ... country code. see Common Parameters. 
    + msisdn (required, string) ... identifier of the contact. `me` and `self` are  acceptable 
    if the request contains an enriched token.

+ Response 200 (application/json)

    + Body

            {
                "documents": [
                    {
                        "type": "CI",
                        "number": "12345678"
                    },
                    {
                        "type": "RUC",
                        "number": "87654321"
                    }
                ]
            }
            

#Group Plans
##Plans Collection [/mobile/{country}/crm/subscribers/{msisdn}/plans{?ql,limit}]
###List Subscriber Plans [GET]
Obtains information about the plans of the customer. All plans are returned by this call unless 
you use the provided filter or limit the output to the first n entries specifying by `limit=n`

The following properties are supported by this API:
- **plans**: (array of **plan**). list of plans of the contact.
Each **plan** contains the following attributes:
    - **identifier**: object of type identifier. Contains the following attributes:
        - **type**: the type of the identifier. Enumerated. Values: `msisdn`, `contract`.
        - **value**: the identifier number. some types of identifiers have no associated numbers. 
    - **contract** : object of type contract. Contains the following attributes:
        - **number**: the contract number
        - **clientCode**: internal identifier of the client
        - **type**: type of contract. Country dependant.
    - **name**: plan name or description. Example "PLAN EMPLEADO PREMIUM MOVIL TIGO (10GB)",
    - **type** : type of plan. Example "POS"
    - **code** : internal plan code. 
    - **description**: textual description of the plan. Example "PLAN EMPLEADO PREMIUM MOVIL TIGO (10GB)",
    - **dataOnly** : indicates if the plan is a Data plan only (true) or not (false)
                  

+ Parameters
    + country (required, string) ... country code. see Common Parameters. 
    + msisdn (required, string) ... identifier of the contact. `me` and `self` are  acceptable 
    if the request contains an enriched token.
    + ql (optional,string)
    
        provides one or more parameters that filters the result collection
        in this version the fields to be filtered are limited and only `AND` is supported. 
        
        + values
            + `identifier_type = 'msisdn'`
            + `identifier_value = '5040000222 | me | self'`
    
    + limit (optional,number)
    
        provides a way to limit the number of items returned in a collection. The root element
        must be a collection for this parameter to work. 


+ Response 200 (application/json)

    + Body

            {
                "plans": [
                    {
                        "identifier": {
                            "type" : "msisdn",
                            "value" : "5040000222"
                        },
                        "contract" : {
                            "number" : "112287",
                            "clientCode" : "875849",
                            "type" : "A"
                        },
                        "name": "PLAN EMPLEADO PREMIUM MOVIL TIGO (10GB)",
                        "type": "POS",
                        "code": "24",
                        "description": "PLAN EMPLEADO PREMIUM MOVIL TIGO (10GB)",
                        "dataOnly": true
                    },
                    {
                        "identifier": {
                            "type" : "msisdn",
                            "value" : "5041111222"
                        },
                        "contract" : {
                            "number" : "112288",
                            "clientCode" : "875849",
                            "type" : "A"
                        },
                        "name": "PLAN CONTROL BUNDLE BBFULL $76.55+IVA",
                        "type": "HIB",
                        "code": "1166",
                        "description": "PLAN CONTROL BUNDLE BBFULL $76.55+IVA",
                        "dataOnly": false
                    }
                ]
            }


#Group Misc
##Unformatted Data [/mobile/{country}/crm/subscribers/{msisdn}/raw{?ql}]
###Get unformatted data from the backend [GET]

All Tigo Countries have different data representation and capabilities. In order to provide a common way to consume
both data that is common between operations (first class information) and specific information only relevant for a 
particular country, API consumption endpoint `raw` represents those attributes that are:
- available only for an specific country or situation.
- models information that cannot be normalized in a programmatic way.
- represents chunks of information that wasn't promoted to first class for some reasons:
 - the modeled data is time bounded
 - it's being evaluated to be promoted to first class information.
 - it simply does not make sense to put effort to normalize the data
 - nobody uses the data attribute, but is returned by the backend nonetheless.
 

**Warning**: the data contained in the raw representation should not be relied upon and for all development purposes
should be considered as _volatile_ for it may change or even dissapear at any time without notice. Only `frozen` marked
attributes will survive in time, but just until they are promoted to first class attributes; which also marks the
attribute as _deprecated = true_

+ Parameters
    + country (required, string) ... country code. see Common Parameters. 
    + msisdn (required, string) ... identifier of the contact. `me` and `self` are  acceptable 
    if the request contains an enriched token.
    + ql (optional,string)
    
        provides one or more parameters that filters the result collection
        here only `identifier` field can be included in the response. 
        Example:
            /raw?ql=WHERE identifier in ('a value', 'another value'...)
        
       

+ Response 200 (application/json)

    + Body

            {
                "dataAttributes": [
                    {
                        "identifier": "string attribute",
                        "value" : "value of the identifier",
                        "frozen" : false,
                        "deprecated" : false
                    },
                    {
                        "identifier": "number attribute",
                        "value" : 123456,
                        "frozen" : true,
                        "deprecated" : false
                    },
                    {
                        "identifier": "boolean attribute",
                        "value" : false,
                        "frozen" : true,
                        "deprecated" : true
                    }
                ]
            }



#Group Experimental
The following methods should be considered as **UNSTABLE** and they are not intended to be implemented by
developers. They're volatile, will change for sure and responses / contract will vary. 

##Subscriber [/mobile/{country}/crm/subscribers/{msisdn}/{?expand}]
###Subscriber Relationship [GET]

Entry point for accessing a _Subscriber_. Each _Subscriber_ represents a single service the customer 

can have with the company (a mobile line, a cable service, an internet service). 

The Subscriber object is an internal representation but is the entry point for accessing customer, 

service,and billing information. 


The following properties are supported by this API:
####Response Body
- **subscriber_id**: id of the subscriber service that the provided identifier points to.
- **client_id**: client id. the owner of the subscriber service. 
- **links**: (array of **link**) expandable links for the subscriber object.
The following links are supported and expandable:
    - **customer**: main client associated to the subscriber. expands to a **_contact_** object

+ Parameters
    + country (required, string) ... country code. see Common Parameters.
    + msisdn (required, string, `595981786431`) ... msisdn identifier of the customer. 
    + expand (optional, string) 
    
        fields (comma separated) to be expanded to full contents.
        
        + values
            + `client_id`
            + `bearer_id`
            


+ Response 200 (application/json)

    + Body
    
            {
                "subscriberId": "12345",
                "clientId" : "c12345",
                "links": [
                    {
                        "customer": "/crm/contacts/client_id/c12345",
                        "bearer" : "/crm/contacts/bearer_id/b12345"
                    }
                ]
            }

