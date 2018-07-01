FORMAT: 1A

# OpenTIGO - Common
### This entry defines generic information useful to publish / consume Tigo APIs


# Group Common Parameters
|`Attribute`|`Description`|`Example`|`Comments`|
|------|---------|------|------|------|
|country|ISO 3166-1 alpha-2 country code|PY (paraguay)<br>GT (guatemala)<br>SV (el salvador) <br>CO (colombia)<br>BO (bolivia)<br>HN (honduras)||
|version|base path version of the resource|v1 represents the first version of the resource<br>v2 represents the second version. More on this on Versioning Section|base path version is part of the URL itself and is not specified as a parameter. it is represented here for informative purposes only|
|msisdn|Mobile number of tigo subscriber in international or local format|595985334650 (intl) 0985334650(loc)|Due to some backend restrictions some api might require the full international format while others can use only portion of the identifier|

# Group Expandable Links
Allows the developer to request additional information included in the `links` section to be appended to the response by expanding the full contents. 
Example:
URL:
    
    /someurl/1234:

Will return:

    "data" : "some data",
    "links" : [
        {
            "expandableLink1" : "/someurl/1234/expand1",
            "expandableLink2" : "/someurl/1234/expand2",
        }
    ]

URL:
    
    /someurl/1234?expand=expandableLink1
    
Will return:

    "data" : "some data",
    "links" : [
        {
            "expandableLink2" : "/someurl/1234/expand2",
        }
    ],
    "expandableLink1" : [
        {
            "property1" : "some value",
            "property2" : "some other value"
        },
        ...
    ]


Circular expansions are not allowed:

    /lines/

has a link to expand /customer

we can expand the customer inside the lines body by specifying 

    expand=customer

/customer/ has a link to expand /lines/

the following expression is invalid, as it is circular:

    expand=customer.lines

and will return `400 BAD_REQUEST`

**Hints**
* You can expand more than one field by specifying comma separated list. 
* If you expanded into an object that contains links, you can use dotted notation to specify 
nested expansions

#Group Implicit Authentication
When _Header Enrichment_ is an option or a _Enriched token_ is present on the invocation, some endpoints
might allow the use of Implicit Authentication, which means that attributes that otherwise must be 
specified as parameters could be omitted by replacing them by the noun `self` or the pronoun `me`

Examples:

An URL containing `MSISDN` identifier :
    
    /crm/customers/595981123456

Can be replaced by 

    /crm/customers/msisdn/me
    
or by

    /crm/customers/msisdn/self

Failing to detect Header Enrichment or to extract the `MSISDN` from Enriched token will result in error 
`401 UNAUTHORIZED`


#Group User Identifier Type
Different types of users can be identified by different methods. For example, in Mobile, a subscriber can be identified by `MSISDN`, 
`contract number` or `email`, while Home users can use either `email` or `home id`

The standard identifier for URLs is `MSISDN`. To specify that the identifier is something different than a `MSISDN`, use the following 
**_userIdentifierType_** query string as follows:

    /crm/customers/courage@nowhere.com?userIdentifierType=email
    
This specifies that `courage@nowhere.com` es an `email` instead of a `msisdn`. If you don't specify the parameter, all APIs will 
assume that you are using an `MSISDN` so the following invocation will **FAIL**:

    /crm/customers/courage@nowhere.com
    







# Group Versioning
Versioning is supported at two levels:
+ **URL Versioning:** determines major updates to either the URL (forcing a resource to have another URI) or the resource itself (it is not the same or has breaking changes making it incompatible with current clients). This is defined on the best practices document. 
+ **Header Versioning:** used to introduce minor revisions in the payload but not breaking changes. 
The revision is a date string using the format YYYYMMDD.

        x-api-revision : 20141118

The following conditions apply:
+ Header versioning is **ONLY** for minor changes that could represent incompatible changes on the code, like removing, renaming, changing datatype of an existing attribute. Addition of new attributes is perfectly compatible so it doesn't  require revision header.
+ Adding a revision to the API means it is FROZEN, meaning that no further changes will be introduced in that version. 
+ By no means revision header should be used to introduce alternative behavior in the code. It's only purpose is to serve the payload representation. This excludes dynamic parameter evaluation, proxy selectivity, payload modification, etc. 


# Group Pagination
|`Attribute`|`Description`|`Example`|`Comments`|
|------|---------|------|------|------|
|Limit|to limit the number of entities returned cursor|?limit=10|depending on the api, server will apply a sensible default.|
|Cursor|to enable pagination when using limit|?cursor=hash7yh9ahda|
|Offset|to enable pagination when using limit|?offset=20|defaults to 0|


#### Parameter Fix
Specifying an invalid offset or limits will be automatically fixed by the server:
+ Negative / NaN offsets will be converted to 0
+ Negative / NaN limits will be converted to API default limit
+ Limits greater than the maximum allowed will be fixed to the maximum allowed by the API. 
+ Offsets greater than the maximum allowed will be fixed to the maximum allowed by the API.


# Group Rate Limiting
TBD

# Group Common Errors
### Common Error Body
Usually the HTTP Status returned by the service should be enough to understand the server side behavior, 
like HTTP 404 (not found) or 401 (unauthorized)
However, in most situations, further level of details are required by the developer to fully understand what
went wrong. For those cases, the ENTITY in a response will contain whe following JSON data:
        
        {
            "error": {
                "statusCode": "404",
                "code": "15",
                "message": "Thespecifiednumberwasnotfound",
                "developerMessage": "provided MSISDN was not found. Exception was: NotFoundException: MSISDN not found",
                "errorURL": null
            }
        }

An extended form of the same error body can contain an additional attribute, `_debug` that will provide developer specific 
information about the error. This is for internal use only and will disappear from the response once we have an stable API. 
The `_debug` info *MUST NOT* be used by clients

        {
            "error": {
                "statusCode": "404",
                "code": "15",
                "message": "Thespecifiednumberwasnotfound",
                "developerMessage": "provided MSISDN was not found. Exception was: NotFoundException: MSISDN not found",
                "errorURL": null
            },
            "_debug": {}
        }


### Common Error Body Definition
+ `statusCode`: duplicates the HTTP Status returned by the server. OPTIONAL
+ `code`: internal development error code. useful to identify the error when reporting to API owner. 
+ `message`: user friendly description of what went wrong. 
+ `developerMessage`: developer oriented fine grained description of the server condition preventing the action 
to be completed.
+ `errorURL`: optional URL pointing to a common developer friendly site that will provide more information about 
the situation. OPTIONAL
+ `_debug` : developer specific information to determine the cause of an error with more level of detail. It's a free form
object that will change continually until the api is stable and will be removed afterwards. 



### Common Status Code List
The following list summarizes the common errors that might be returned for API invocation. Specific lists can 
extend the api definition:

- 200 `OK` - The request was successful (some API calls may return 201 instead).
- 201 `Created` - The request was successful and a resource was created.
- 204 `No Content` - The request was successful but there is no representation to return (that is, the response is empty).
- 304 `Not Modified` - the copy stored on the client is still valid as the server didnt made changes on the cache. Requires the client using ETag and If-None-Match and local caching.  
- 400 `Bad Request` - The request could not be understood or was missing required parameters.
- 401 `Unauthorized` - Authentication failed or user does not have permissions for the requested operation.
- 403 `Forbidden` - Access denied. Differs from 401 in that Authentication DID succeed, but permission check failed.
- 404 `Not Found` - Resource was not found.
- 405 `Method Not Allowed` - Requested method is not supported for the specified resource.
- 429 `Too Many Requests` - Exceeded API execution limits. Pause requests, wait one minute, and try again. 
- 500 `Internal Server Error` - Something bad has happened :( We might be already aware and working on the solution. 
- 503 `Service Unavailable` - The service is temporary unavailable (e.g. scheduled Platform Maintenance). Try again later.



# Group Caching
### ETag Caching
When an API enables caching the client can decide to cache the data locally. For this purpose, those APIs that
provide caching support will return the corresponding headers as follows:

        ETag: "686897696a7c876b7e"

Client must in turn, in the succesive requests send the obtained ETag:
        
        If-None-Match: "686897696a7c876b7e"
        
If locally cached data is still valid, server will return `HTTP 304 Not Modified` status, without a body.

### Cache Control
Server support for cache control methods as defined in standard [RFC2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)