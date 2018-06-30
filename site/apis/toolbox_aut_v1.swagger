FORMAT: 1A
HOST: http://polls.apiblueprint.org/

# toolbox_aut_v1


This API is responisble to obtain authorization for ToolBox products.



## Toolbox Collection [/authorization_endpoint]

### Obtain Authorization [POST]


Applies to:
==========
| Country        | PATH     |
| ------------- |:-------------:|
| GT    | /TigoPlay/IsAuthorizedToolboxUser/V1|
| PY    | /osb/SEC/Platforms/Lucas/GetPlayerAuthorizationInfo/V1|
| CR    | SIGA-WS-TG/servlet/awsconsumotigoplay |



+ Request (application/xml)

        <?xml version="1.0" encoding="UTF-8"?>
             <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:tem="http://tempuri.org/">
                <soapenv:Header/>
                <soapenv:Body>
                <tem:authorization_endpoint>
                <tem:subscriber_id>PY-4208330728</tem:subscriber_id>
                <tem:country_code>PY</tem:country_code>
                <tem:resource_id>tv:ren</tem:resource_id>
                <tem:action_id>VIEW</tem:action_id>
                <tem:ip_address>200.85.12.124</tem:ip_address>
                </tem:authorization_endpoint>
                </soapenv:Body>
                </soapenv:Envelope>


+ Response 200 (application/xml)

        <?xml version="1.0" encoding="UTF-8"?>
        <authorization_endpointResult xmlns="http://tempuri.org/" 
              xmlns:xsd="http://www.w3.org/2001/XMLSchema"
              xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/"
              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"> 
        <access>false</access> 
        <max_rating>G</max_rating>
        <ttl>86400</ttl> 
        </authorization_endpointResult>



# Data Structures


Declaración de los distintos tipos de respuestas a ser entregeados por el API.


## bodyRequest (object)

 <?xml version="1.0" encoding="UTF-8"?>
      <SOAP-ENV:Envelope xmlns:SOAP-ENV="" xmlns:xsd="" xmlns:xsi="">
         <SOAP-ENV:Body>
            <m:transaction-identity-verification xmlns:m="">
            </m:transaction-identity-verification>
         </SOAP-ENV:Body>
      </SOAP-ENV:Envelope>