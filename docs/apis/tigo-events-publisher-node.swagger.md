FORMAT: 1A
//HOST: http://polls.apiblueprint.org/

# tigo-events-publisher-node

Tigo events publisher is a node application that can be configured to send events defined by a configuration `schema` to different publishers.
Currently events are only configured for kinesis publishing, but with minimal refactoring (in the works) there can be a plugin based arquitecture that enables multi-casting to different platforms (in mind redis, apache kafka).

This is a private API that is to be consumed by the apigee proxies wanting to record into our streams their events. 

This is currently only secured by an `apikey` that is to be sent within an HTTP header `apikey`

###[TO DO]
* add multicast capabilities

## Configuration collection endpoint [/conf]

### List all current configurations [GET]

With this endpoint you can get the currently redis stored and node loaded configurations.

Return value is a JSON object whose first level keys are schema names, within their value, the configuration they are using.

+ Request (application/json)

    + Headers
    
            apikey: <apikeyvalue>
        
+ Response 200 (application/json)

        {
            "gt_tigo_shop_purchase": {
                "stream_name": "tigo_gt_tigo_shop_purchase_stream",
                "buffer_size": 1,
                "validate_track": 0,
                "store": true
            },
            "tigo-test": {
                "stream_name": "mic-dump",
                "buffer_size": 1,
                "validate_track": 0,
                "store": true
            }
        }

### Add or modify a current configuration [POST]

You can create or overwrite a current configuration. The configurations are stored to redis and will soon trigger a `reload config` so that all concurrent nodes can reload and start using that configuration.

<!--+ Parameters-->
<!--    + schema_name (required , string , `tigo-test`) ... schema for the configuration-->
<!--    + stream_name (required , string , `mic-dump`) ... stream identifier to where we will push the information -->
<!--    + buffer_size (optional , string , `2`) ... integer for buffering count. defaults to 1 if not set.-->
    

+ Request (application/json)

    + Headers
    
            apikey:<apikey>
    + Body
    
            {
                "schema_name": {schema_name},
                "stream_name": {stream_name},
                "buffer_size": {buffer_size}
            }

+ Response 200 (application/json)
        
        {
            "status": "ok",
            "msg": "chill"
        }

### Delete configuration section [DELETE]

Delete current configuration by schema_name . Return value is currently remaining configurations.
+ Request (application/json)

    + Headers
    
            apikey:<apikey>
    + Body
    
            {
                "schema_name": {schema_name},
            }

+ Response 200 (application/json)
        
        {
            "gt_tigo_shop_purchase": {
                "stream_name": "tigo_gt_tigo_shop_purchase_stream",
                "buffer_size": 1,
                "validate_track": 0,
                "store": true
            },
            "tigo-test": {
                "stream_name": "mic-dump",
                "buffer_size": 1,
                "validate_track": 0,
                "store": true
            }
        }


## Status of the calls [/status]

### Get current status of the application [GET]
You can get a clear view of what requests have failed with this the `no_header` portion of the response indicates how many requests have not contained the necesary `x-mic-schema` header.

The `unknown_schema` section shows which schemas have come in the header but were not found in the configuration.


+ Response 200 (application/json)
        
    + Body
            
            {
                no_header: 0,
                unknown_schema: { }
            }

## Publish events [/events]

### Publish new event to stream [POST]
Publish a new event to the stream.

The schema name defines to which stream and with which configuration. The schema name must be sent in the `x-mic-schema` header.
+ Request (application/json)

    + Headers
    
            x-mic-schema:<schema_name>
            
+ Response 202 (application/json)
        
    + Body
            
            {
                status:"ok",
                msg:"added"
            }
