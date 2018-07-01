FORMAT: 1A
HOST: http://test.api.tigo.com/tigoid/orm/v2/db/operations/churn/

# Tigo Churn


# ID types
Tigo ID recognizes several ID types, so an ID parameter is usually paired with another specifying its format. 
These are the ID types supported by churn operations.

| ID type  | Format | Example | 
|----------|----------|----------|
| homeid |Tigo Star ID|PY-0203023|
| mobileid |MSISDN|595981555222|


# Scopes
A scope limits the set of returned objects. Whenever a scope is provided without an ID type, TigoID will assumed the default ID type for that scope.  

| Scopes   | Default ID type |
|----------|----------|
| homeid |homeid|
| mobileid |mobileid|


## Search [/search]


### Search [POST]
Retuns objects identified by, and associations to, an Identifier

+ Parameters
    + target_id (string,`595983471906`) ... ID that'll be searched
    + target_type (string,`mobileid`) ... Format of the ID. See table above. Optional, but recommended.
    + scope (string, `mobileid`)... Scope of returned objects. See the table above. Required if target_type is not provided.

+ Request 
    + Headers
    
            apikey: Hd9AGq5CAFbo6YbX-------
            
+ Response 200 (application/json)

    + Attributes(searchResponse)

## Recycle [/recycle]

### Recycle [POST]
Deletes objects and associations to an Identifier

+ Request 
    + Headers
    
            apikey: Hd9AGq5CAFbo6YbXGK-----------

+ Parameters
    + target_id (string,`595983471906`) ... ID that'll be searched
    + target_type (string,`mobileid`) ... Format of the ID. See table above. Optional, but recommended.
    + scope (string, `mobileid`)... Scope of returned objects. See the table above. Required if target_type is not provided.
            
+ Response 200 (application/json)
 
   + Attributes(recycleResponse)

    

## Data Structure

## searchResponse(object)
  + churn (object)
    + operation: search
    + objects: (array)

## recycleResponse(object)
  + churn (object)
    + operation: recycle
    + objects: (array)
