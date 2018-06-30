FORMAT: 1A
HOST: https://test.api.tigo.com/v2/tigo/intcomex
# OpenTIGO - Intcomex

The Intcomex Web Services, or IWS for short, is a set of web services that allow clients to interact with
Intcomex to perform operations like obtaining information about products or placing orders
programmatically.

# Polls API Root [/v2/tigo/intcomex]

asd


## Group Products

Resources related to obtain producs informations.



## Catalog  [/{countryCode}/catalog]

The GetCatalog method can be used to obtain a full list of products that are available to a client for pricing
and purchasing. The list returned contains information about each of the products.

 + Parameters

     + countryCode : gt (string, required) - gt
### Get Catalog [GET]

+ Request
        This resource is protected via oauth2

 

 + Headers
    
            Authorization: Bearer {{AuthToken}}

+ Response 200 (application/json)

   + Attributes
      + products (array) - List of Product
        + Product(object)      
        + Sku : "SE001MSE01" (string) - Sku String The unique SKU identifier for the product.,
        + Mpn : `AAA-01148` (string) - The manufacturer part number of the product,
        - Manufacturer(object) - Details about the product’s manufacturer.
          - ManufacturerId: "msf" (string),
          - Description: "Microsoft" (string),
        + Brand(object) - Details about the product’s brand.
           + ManufacturerId: "msf",
           + BrandId: "msf",
           + Description: "Microsoft"
        + Category(object) - The multilevel categorization of the product (from Intcomex’s internal categorization structure) 
           + CategoryId: "sfw",
           + Description: "Software",
           + Subcategories(object)
              + CategoryId: "sfw.business",
              + Description: "Business & Office Applications",
              + Subcategories(array)
        + Description": "Microsoft Word 2013 " (string) - The description of the product, in the language specified by the Locale parameter.,
        + Price(object) - Pricing details
            + UnitPrice: 103.5294 (number),
            + CurrencyId: "US" (string)
        + InStock: 0 (number) - The number of units of the product that are in stock (at the moment the method was requested),
        + Type: "Downloadable" (string) - The type of the product.


## Products Collection [/{countryCode}/products{?productsIds}]

The GetProducts method is very similar to the GetCatalog method with the difference that it can be used
to obtain information about a specific list of products instead of the entire catalog of products. Just as
with GetCatalog, this method can be used for pricing and purchasing and the response returned contains
information about all the products requested.

+ Parameters
      + countryCode : gt (string, required) - gt
      + productsIds (required, number, `SE001MSE01,SE001MSE02`) ... Comma separated values
      
### List Products [GET]


+ Request
     
        This resource is protected via oauth2


    + Headers
    
            Authorization: Bearer {{AuthToken}}

+ Response 200 (application/json)

   + Attributes
      + products (array) - List of Product
        + Product(object)      
        + Sku : "SE001MSE01" (string) - Sku String The unique SKU identifier for the product.,
        + Mpn : `AAA-01148` (string) - The manufacturer part number of the product,
        - Manufacturer(object) - Details about the product’s manufacturer.
          - ManufacturerId: "msf" (string),
          - Description: "Microsoft" (string),
        + Brand(object) - Details about the product’s brand.
           + ManufacturerId: "msf",
           + BrandId: "msf",
           + Description: "Microsoft"
        + Category(object) - The multilevel categorization of the product (from Intcomex’s internal categorization structure) 
           + CategoryId: "sfw",
           + Description: "Software",
           + Subcategories(object)
              + CategoryId: "sfw.business",
              + Description: "Business & Office Applications",
              + Subcategories(array)
        + Description": "Microsoft Word 2013 " (string) - The description of the product, in the language specified by the Locale parameter.,
        + Price(object) - Pricing details
            + UnitPrice: 103.5294 (number),
            + CurrencyId: "US" (string)
        + InStock: 0 (number) - The number of units of the product that are in stock (at the moment the method was requested),
        + Type: "Downloadable" (string) - The type of the product.

 + Body
 
             [
                {
            "Sku": "SE001MSE01",
            "Mpn": "AAA-01148",
            "Manufacturer": {
            "ManufacturerId": "msf",
            "Description": "Microsoft"
            },
            "Brand": 
            {
            "ManufacturerId": "msf",
            "BrandId": "msf",
            "Description": "Microsoft"
            },
            "Category":
            {
            "CategoryId": "sfw",
            "Description": "Software",
            "Subcategories":
            [
            {
                "CategoryId": "sfw.business",
                "Description": "Business & Office Applications",
                "Subcategories": []
            }
            ]
            },
            "Description": "Microsoft Access 2013 - License - 1 PC - download - 32/64-bit",
            "Price": 
            {
                "UnitPrice": 103.5294,
                "CurrencyId": "US"
            },
            "InStock": 0,
            "Type": "Downloadable"
            },
            {
            “Sku": "SE001MSE02",
            "Mpn": "AAA-01147",
            "Manufacturer": 
            {
                "ManufacturerId": "msf",
                "Description": "Microsoft"
            },
            "Brand": 
            {
            "ManufacturerId": "msf",
            "BrandId": "msf",
            "Description": "Microsoft"
            },
            "Category": {
            "CategoryId": "sfw",
            "Description": "Software",
            "Subcategories": [
            {
                "CategoryId": "sfw.business",
                "Description": "Business & Office Applications",
                "Subcategories": []
            }
            ]
            },
            "Description": "Microsoft Access 2013 - License - 3 PC - download - 32/64-bit",
            "Price": 
            {
            "UnitPrice": 103.5294,
            "CurrencyId": "US"
            },
            "InStock": 0,
            "Type": "Downloadable"
            }]


## Product  [/{countryCode}/products/{productId}]

The GetProduct method is very similar to both the GetCatalog and GetProducts method with the
difference that it can be used to obtain information about a single product instead of a list of products.
Just as with GetCatalog and GetProducts, this method can be used for pricing and purchasing and the
response returned contains information about the product requested.


+ Parameters
      + countryCode : gt (string, required) - gt
      
### Product Detail [GET]

+ Request

        This resource is protected via oauth2

 + Headers
    
                Authorization: Bearer {{AuthToken}}

+ Parameters
    + productId: SE001MSE04 (required, string) - ProductId


+ Response 200 (application/json)

 + Attributes
     + Product(object)      
        + Sku : "SE001MSE01" (string) - Sku String The unique SKU identifier for the product.,
        + Mpn : "AAA01148" (string) - The manufacturer part number of the product,
        + Manufacturer(object) - Details about the product’s manufacturer.
          + ManufacturerId": "msf" (string),
          + Description": "Microsoft" (string),
        + Brand(object) - Details about the product’s brand.
           + ManufacturerId: "msf",
           + BrandId: "msf",
           + Description: "Microsoft"
        + Category(object) - The multilevel categorization of the product (from Intcomex’s internal categorization structure) 
           + CategoryId: "sfw",
           + Description: "Software",
           + Subcategories(object)
              + CategoryId: "sfw.business",
              + Description: "Business & Office Applications",
              + Subcategories(array)
        + Description": "Microsoft Word 2013 " (string) - The description of the product, in the language specified by the Locale parameter.,
        + Price(object) - Pricing details
            + UnitPrice: 103.5294 (number),
            + CurrencyId: "US" (string)
        + InStock: 0 (number) - The number of units of the product that are in stock (at the moment the method was requested),
        + Type: "Downloadable" (string) - The type of the product.


 + Body
 
            {
               "Sku": "SE001MSE01",
                "Mpn": "AAA-01148",
                "Manufacturer": 
                {
                    "ManufacturerId": "msf",
                    "Description": "Microsoft"
                },
                "Brand":
                {
                    "ManufacturerId": "msf",
                    "BrandId": "msf",
                    "Description": "Microsoft"
                },
                "Category": 
                {
                    "CategoryId": "sfw",
                    "Description": "Software",
                    "Subcategories": 
                    [
                    {
                        "CategoryId": "sfw.business",
                        "Description": "Business & Office Applications",
                        "Subcategories": []
                    }
                    ]
                },
                "Description": "Microsoft Access 2013 - License - 1 PC - download - 32/64-bit",
                "Price": 
                {
                    "UnitPrice": 103.5294,
                    "CurrencyId": "US"
                },
                "InStock": 0,
                "Type": "Downloadable"
            }


## Group Orders

Resources related to questions in the API.

## Orders [/{countryCode}/orders]

When the client is ready to place an order, the method PlaceOrder is called, which expects a list of
products with quantities to be included in the order and then generates an Intcomex order, which is finally
returned back to the client, where it can be processed in any way needed.

+ Parameters
      + countryCode : gt (string, required) - gt

### Place Order [POST]

+ Request (application/json)
    
        This resource is protected via oauth2
  
   A JSON array listing all product SKUs with their respective quantities to be included in the order to place. 

    + `Sku` The unique SKU identifier for the product.
    + `Quantity` Desired Quantity

    + Headers
    
                Authorization: Bearer {{AuthToken}}


    + Body 
    
            [
             {
                "Sku": "SE001MSE09",
                "Quantity":"10"
             }
            ]



+ Response 200 (application/json)

 + Attributes
     + Order (object)
        + OrderNumber:"" (string) - The unique SKU identifier for the product
        + Customer(object) - The manufacturer part number of the product
            + CustomerId:"" (string)
            + Name: ""(string)
        + OrderDate: "2015-08-19T00:00:00" (string)
        + Currency(object)
             + CurrencyId : "us",
             + CurrencyCode : "USD",
             + Description : "Dollars",
             + Symbol : "US$"
        + TaxRate : "7.72" (string),
        + OtherFees : "" (string),
        + Subtotal(object) - The subtotal amount of the order.
             + UsAmount : 2050.25 (number),
             + HomeAmount : 2050.25 (number),
             + HomeCurrencyId : "US" (string),
        + Discounts (object) - Total of discounts applied.
             + UsAmount: 0 (number),
             + HomeAmount: null (number),
             + HomeCurrencyId: "US" (string),
        + Tax(object) - Tax amount charged.
              + UsAmount : 246.03 (number),
              + HomeAmount : 246.03 (number),
              + HomeCurrencyId : "US" (string)
        + ShippingFee(object) - Shipping fees charged.
            + UsAmount: 0 (number),
            + HomeAmount: null,
            + HomeCurrencyId": "US" (string)
        + Total(object) - The grand total of the order.
             + UsAmount: 2296.28 (number),
             + HomeAmount: 2296.28 (number),
             + HomeCurrencyId: "US" (string)
        + Items(array)- A list of OrderItem ojects representing the product items included in the order.
        + OrderItem(object)
         + Line:0 (number) -The line number within the order
         + Product(object)      
          + Sku : "SE001MSE01" (string) - Sku String The unique SKU identifier for the product.,
          + Mpn : `AAA-01148` (string) - The manufacturer part number of the product,
          - Manufacturer(object) - Details about the product’s manufacturer.
           - ManufacturerId: "msf" (string),
           - Description: "Microsoft" (string),
          + Brand(object) - Details about the product’s brand.
           + ManufacturerId: "msf",
           + BrandId: "msf",
           + Description: "Microsoft"
          + Category(object) - The multilevel categorization of the product (from Intcomex’s internal categorization structure) 
           + CategoryId: "sfw",
           + Description: "Software",
           + Subcategories(object)
            + CategoryId: "sfw.business",
            + Description: "Business & Office Applications",
            + Subcategories(array)
          + Description": "Microsoft Word 2013 " (string) - The description of the product, in the language specified by the Locale parameter.,
          + Price(object) - Pricing details
            + UnitPrice: 103.5294 (number),
            + CurrencyId: "US" (string)
          + InStock: 0 (number) - The number of units of the product that are in stock (at the moment the method was requested),
          + Type: "Downloadable" (string) - The type of the product.
         + Quantity:0 (number)
         + UnitPrice(object)
          + Amount
          + HomeAmount
          + Currency (object)
           + CurrencyId
           + CurrencyCode
           + Description
           + Symbol
         + ExtendedPrice
          + Amount
          + HomeAmount
          + Currency
           + CurrencyId
           + CurrencyCode
           + Description
           + Symbol
        + Status (object)
         + StatusCode
         + Description
        + ItemCount:1 (number)
 + Body
 
            {
                "OrderNumber": "601445",
                "Customer": 
                {
                    "CustomerId": "XECWEBDEMO1",
                    "Name": "INTCOMEX DEL ECU"
                },
                "OrderDate": "2015-03-16T00:00:00",
                "CurrencyId": "US",
                "TaxRate": "1",
                "OtherFees": "",
                "Subtotal": 
                {
                    "UsAmount": 2050.25,
                    "HomeAmount": 2050.25,
                    "HomeCurrencyId": "US"
                },
                "Discounts": 
                {
                    "UsAmount": 0,
                    "HomeAmount": null,
                    "HomeCurrencyId": "US"
                },
                "Tax": 
                {
                    "UsAmount": 246.03,
                    "HomeAmount": 246.03,
                    "HomeCurrencyId": "US"
                },
                "ShippingFee": 
                {
                    "UsAmount": 0,
                    "HomeAmount": null,
                    "HomeCurrencyId": "US"
                },
                "Total": 
                {
                    "UsAmount": 2296.28,
                    "HomeAmount": 2296.28,
                    "HomeCurrencyId": "US"
                },
                "Items": [
                {
                    "LineNumber": 1,
                    "Product": 
                    {
                        “Sku": "SE001MSE09",
                        "Mpn": "AAA-04580",
                        "Manufacturer": 
                        {
                            "ManufacturerId": "msf",
                            "Description": "Microsoft"
                        },
                        "Brand": 
                        {
                            "ManufacturerId": "msf",
                            "BrandId": "msf",
                            "Description": "Microsoft"
                        },
                        "Category": 
                        {
                            "CategoryId": "sfw",
                            "Description": "Software",
                            "Subcategories": [
                            {
                                "CategoryId": "sfw.business",
                                "Description": "Business & Office Applications",
                                "Subcategories": []
                            }
                        ]
                        },
                        "Description": "Microsoft Office 365 Small Business Premium - …",
                        "Price": {
                        "UnitPrice": 0,
                        "CurrencyId": null
                        },
                        "Type": "Downloadable"
                        },
                        "Quantity": 10,
                        "UnitPrice": {
                        "UsAmount": 163.26,
                        "HomeAmount": null,
                        "HomeCurrencyId": null
                         },
                         "ExtendedPrice": {
                         "UsAmount": 1632.6,
                        "HomeAmount": 1632.6,
                        "HomeCurrencyId": null
                         }
                         },
                         {
                         "LineNumber": 2,
                         "Product": {
                         "Sku": "SE001MSE12",
                        "Mpn": "AAA-02904",
                        "Manufacturer": {
                         "ManufacturerId": "msf",
                        "Description": "Microsoft"
                         },
                        "Brand": {
                         "ManufacturerId": "msf",
                        "BrandId": "msf",
                        "Description": "Microsoft"
                         },
                         "Category": {
                         "CategoryId": "sfw",
                        "Description": "Software",
                        "Subcategories": [
                         {
                         "CategoryId": "sfw.business",
                         "Description": "Business & Office Applications",
                         "Subcategories": []
                         }
                         ]
                         },
                        "Description": "Microsoft Office Home and Student 2013 …",
                         "Price": {
                         "UnitPrice": 0,
                        "CurrencyId": null
                         },
                        "Type": "Downloadable"
                         },
                         "Quantity": 5,
                         "UnitPrice": {
                         "UsAmount": 83.53,
                        "HomeAmount": null,
                        "HomeCurrencyId": null
                         },
                         "ExtendedPrice": {
                         "UsAmount": 417.65,
                        "HomeAmount": 417.65,
                        "HomeCurrencyId": null
                         }
                         }
                         ]
            }


## Orders Detail [/{countryCode}/orders/{orderNumber}]

The GetOrder method can be used to obtain the details of a specific order. The response returned is the
same one as the one returned from the PlaceOrder method which contains the order requested and its
details

+ Parameters
      + countryCode : gt (string, required) - gt

### Get Order Detail [GET] 

+ Request

        This resource is protected via oauth2

 + Headers
    
                Authorization: Bearer {{AuthToken}}
+ Parameters
      + orderNumber: 1160483 (required, number) - OrderNumber
         

+ Response 200 (application/json)
 
 + Attributes
     + Order (object)
        + OrderNumber:"1160483" (string) - The number of the order generated
        + Customer(object) - The details of the client’s Intcomex customer account {CustomerId:XGTCOM5512,Name:Tigo}.
            + CustomerId:"XGTCOM5512" (string)
            + Name: "Tigo"(string)
        + OrderDate: `2015-08-19T00:00:00` (string)
        + Currency(object)- The currency in use for the price amounts displayed in the order
        + TaxRate : "1" (string)-The tax rate applied to the order.,
        + OtherFees : "" (string) - Other fees that may have been added to the order.,
        + Subtotal(object) - The subtotal amount of the order
          + UsAmount : 2050.25 (number),
          + HomeAmount : 2050.25 (number),
          + HomeCurrencyId : "US" (string),
        + Discounts (object) - Total of discounts applied.
          + UsAmount: 0 (number),
          + HomeAmount: null (number),
          + HomeCurrencyId: "US" (string),
        + Tax(object) - Tax amount charged.
          + UsAmount : 246.03 (number),
          + HomeAmount : 246.03 (number),
          + HomeCurrencyId : "US" (string)
        + ShippingFee(object) - Shipping fees charged.
         + UsAmount: 0 (number),
         + HomeAmount: null,
         + HomeCurrencyId": "US" (string)
        + Total(object) - The grand total of the order.
         + UsAmount: 2296.28 (number),
         + HomeAmount: 2296.28 (number),
         + HomeCurrencyId: "US" (string)
        + Items (array) - TypeOrderItem
        + TypeOrderItem(object) - Line Numeric The line number within the order Product Object The details of the product assigned to the OrderItem 
          + Line: "1" (number),
          + Product(object)      
             + Sku : "SE001MSE01" (string) - Sku String The unique SKU identifier for the product.,
             + Mpn : `AAA-01148` (string) - The manufacturer part number of the product,
             + Manufacturer(object) - Details about the product’s manufacturer.
                + ManufacturerId: "msf" (string),
                + Description: "Microsoft" (string),
            + Brand(object) - Details about the product’s brand.
                + ManufacturerId: "msf",
                + BrandId: "msf",
                + Description: "Microsoft"
            + Category(object) - The multilevel categorization of the product (from Intcomex’s internal categorization structure) 
            + CategoryId: "sfw",
            + Description: "Software",
            + Subcategories(object)
              + CategoryId: "sfw.business",
              + Description: "Business & Office Applications",
              + Subcategories(array)
            + Description": "Microsoft Word 2013 " (string) - The description of the product, in the language specified by the Locale parameter.,
            + Price(object) - Pricing details
                + UnitPrice: 103.5294 (number),
                + CurrencyId: "US" (string)
            + InStock: 0 (number) - The number of units of the product that are in stock (at the moment the method was requested),
            + Type: "Downloadable" (string) - The type of the product.          
          + Quantity: 0 (number),
          + UnitPrice: "" (string)


        + Status (object)
        + ItemCount (string)
        + Tag (string)

 + Body
 
            {
            "OrderNumber": "1160483",
            "Customer": {
            "CustomerId": "XGTCOM5512",
            "Name": "Tigo",
            "Company": {
                "Id": "XGT",
                "Description": null,
                "Name": "Guatemala",
                "Address1": null,
                "Address2": null,
                "City": null,
                "State": null,
                "PostalCode": null,
                "CountryId": null,
                "CountryName": null,
                "Telephone1": null,
                "Telephone2": null,
                "Fax": null,
                "FaxRma": null,
                "Website": null,
                "CurrencyId": null,
                "CurrencyPreference": null,
                "TaxValue": null,
                "TaxLabel": null,
                "Status": null,
                "Image1": null,
            "Image2": null,
            "Image3": null,
            "InfoEmail": null,
            "DisplayOrder": null,
            "Locale": null,
            "IwsEnabled": null
            },
            "Country": {
                "CountryId": 0,
                "Id": "gt",
                "Iso3": null,
                "Name": "Guatemala",
                "DateCreated": "0001-01-01T00:00:00+00:00",
                "DateModified": "0001-01-01T00:00:00+00:00"
            },
            "ApiKey": "89f15c4b-b81e-455b-bca4-e20dfbdff06b",
            "AccessKey": "16aa2ed0-cc8c-4f88-860e-792766b84f8c",
            "TraxUserId": "XGTCOM5512WS",
            "TraxPassword": "UbL4jd5BkzKR2OxCaIk7XA==",
            "Status": "a",
            "Users": [
                {
                    "Id": "XGTCOM5512WS",
                    "Password": null,
                    "FirstName": "Tigo Admin",
                    "LastName": null,
                    "Email": null,
                    "Country": null,
                    "Company": null,
                    "Customer": {
                        "CustomerId": "XGTCOM5512",
                        "Name": "Tigo",
                        "Company": null,
                        "Country": null,
                        "ApiKey": "00000000-0000-0000-0000-000000000000",
                    "AccessKey": "00000000-0000-0000-0000-000000000000",
                    "TraxUserId": null,
                    "TraxPassword": null,
                    "Status": "\u0000",
                    "Users": null,
                    "Settings": null,
                    "IpAddresses": null
                },
                "Status": "\u0000",
                "AdminAuthenticationToken": "00000000-0000-0000-0000-000000000000",
                "AdminAuthenticationTokenCreationDate": "0001-01-01T00:00:00",
                "AdminAccessLevel": 2,
                "Settings": null
            }
                ],
                "Settings": [
                    {
                        "SettingId": "methods.additemtoshoppingcart",
                        "Description": "Allow calling the AddItemToShoppingCart method.",
                        "Value": "0"
                    },
                    {
                        "SettingId": "methods.getcatalog",
                        "Description": "Allow calling the GetCatalog method.",
                        "Value": "1"
                    },
                    {
                        "SettingId": "methods.getcustomer",
                        "Description": "Allow calling the GetCustomer method.",
                        "Value": "1"
                    },
                    {
                        "SettingId": "methods.getcustomers",
                        "Description": "Allow calling the GetCustomers method.",
                        "Value": "0"
                    },
                    {
                        "SettingId": "methods.getorder",
                        "Description": "Allow calling the GetOrder method.",
                        "Value": "0"
                    },
                    {
                        "SettingId": "methods.getproduct",
                        "Description": "Allow calling the GetProduct method.",
                        "Value": "1"
                    },
                    {
                        "SettingId": "methods.getproductkeystatus",
                        "Description": "Allow calling the GetProductKeyStatus method.",
                        "Value": "1"
                    },
                    {
                        "SettingId": "methods.getproducts",
                        "Description": "Allow calling the GetProducts method.",
                        "Value": "1"
                    },
                    {
                        "SettingId": "methods.getshoppingcart",
                        "Description": "Allow calling the GetShoppingCart method.",
                        "Value": "0"
                    },
                    {
                        "SettingId": "methods.getuser",
                        "Description": "Allow calling the GetUser method.",
                        "Value": "1"
                    },
                    {
                        "SettingId": "methods.getusers",
                        "Description": "Allow calling the GetUsers method.",
                        "Value": "1"
                    },
                    {
                        "SettingId": "methods.placeorder",
                        "Description": "Allow calling the PlaceOrder method.",
                        "Value": "1"
                    },
                    {
                        "SettingId": "methods.purchaseesdproducts",
                        "Description": "Allow calling the PurchaseEsdProducts",
                        "Value": "1"
                    },
                    {
                        "SettingId": "general.locale",
                        "Description": "Default locale.",
                        "Value": "es"
                    },
                    {
                        "SettingId": "security.ipvalidationenabled",
                        "Description": "Enable validation of client IP addresses.",
                        "Value": "false"
                    },
                    {
                        "SettingId": "requests.timestampcheck",
                        "Description": "Validate request timestamps.",
                        "Value": "false"
                    },
                    {
                        "SettingId": "products.fields.view.all",
                        "Description": "View all product fields.",
                        "Value": "0"
                    }
                ],
                "IpAddresses": []
            },
            "OrderDate": "2015-08-19T00:00:00",
            "Currency": {
                "CurrencyId": "us",
                "CurrencyCode": "USD",
                "Description": "Dollars",
                "Symbol": "US$"
            },
            "TaxRate": "7.72",
            "OtherFees": "",
            "Subtotal": {
                "Amount": 103.53,
                "HomeAmount": 799.25,
                "Currency": {
                    "CurrencyId": "us",
                    "CurrencyCode": "USD",
                    "Description": "Dollars",
                    "Symbol": "US$"
                }
            },
            "Discounts": {
                "Amount": 0,
                "HomeAmount": null,
                "Currency": {
                    "CurrencyId": "us",
                    "CurrencyCode": "USD",
                    "Description": "Dollars",
                    "Symbol": "US$"
                }
            },
            "Tax": {
                "Amount": 12.42,
                "HomeAmount": 95.88,
                "Currency": {
                    "CurrencyId": "us",
                    "CurrencyCode": "USD",
                    "Description": "Dollars",
                    "Symbol": "US$"
                }
            },
            "ShippingFee": {
                "Amount": 0,
                "HomeAmount": null,
                "Currency": {
                    "CurrencyId": "us",
                    "CurrencyCode": "USD",
                    "Description": "Dollars",
                    "Symbol": "US$"
                }
            },
            "Total": {
                "Amount": 115.95,
                "HomeAmount": 895.13,
                "Currency": {
                    "CurrencyId": "us",
                    "CurrencyCode": "USD",
                    "Description": "Dollars",
                    "Symbol": "US$"
                }
            },
            "Items": [
                {
                    "LineNumber": 1,
                    "Product": {
                        "Sku": "SE001MSE02",
                        "Mpn": "AAA-01147",
                        "Manufacturer": {
                            "ManufacturerId": "msf",
                            "Description": "Microsoft"
                        },
                        "Brand": {
                            "ManufacturerId": "msf",
                            "BrandId": "msf",
                            "Description": "Microsoft"
                        },
                        "Category": {
                            "CategoryId": "sfw",
                            "Description": "Software",
                            "Subcategories": [
                                {
                                    "CategoryId": "sfw.business",
                                    "Description": "Aplicaciones para Negocio y Oficina",
                                    "Subcategories": []
                                }
                            ]
                        },
                        "Description": "Microsoft Access 2013 - Licencia - 1 PC - descarga - 32/64-bit, ESD, Click-to-Run - Win - Español",
                        "Price": {
                            "UnitPrice": 115.9494,
                            "CurrencyId": "US"
                        },
                        "InStock": 0,
                        "Type": "Downloadable"
                    },
                    "Quantity": 1,
                    "UnitPrice": {
                        "Amount": 103.5294,
                        "HomeAmount": null,
                        "Currency": {
                            "CurrencyId": "us",
                            "CurrencyCode": "USD",
                            "Description": "Dollars",
                            "Symbol": "US$"
                        }
                    },
                    "ExtendedPrice": {
                        "Amount": 103.53,
                        "HomeAmount": 799.25,
                        "Currency": {
                            "CurrencyId": "us",
                            "CurrencyCode": "USD",
                            "Description": "Dollars",
                            "Symbol": "US$"
                        }
                    }
                }
            ],
            "Status": {
                "StatusCode": "1",
                "Description": "Open"
            },
            "ItemCount": 1,
            "Tag": "HUAWEI"

            }

## Group Esd Products

## Purchase Esd Product [/{countryCode}/orders/{orderId}/esd]

The PurchaseEsdProducts method is used to request the ESD fulfillments from all downloadable products
within an order, which will contain the product keys, download links, etc.
Obviously, this method only works on ESD products (product type = “downloadable”) within a purchase
order. ESD fulfillments can only be requested once per order

+ Parameters
      + countryCode : gt (string, required) - gt


### Purchase Esd Product [POST]


+ Parameters

    + orderNumber:12323 (number, required) - Order containing esd products.


+ Request

        This resource is protected via oauth2
    



    + Headers
        
            Authorization: Bearer {{Authtoken}}
    
    + Body
    

            
  
  
+ Response 200 (application/json)

 + Attributes
 
        + DownloadProducts(array)
        + DownloadProduct(object)
         + Product(object)      
             + Sku : "SE001MSE01" (string) - Sku String The unique SKU identifier for the product.,
             + Mpn : `AAA-01148` (string) - The manufacturer part number of the product,
             + Manufacturer(object) - Details about the product’s manufacturer.
                + ManufacturerId: "msf" (string),
                + Description: "Microsoft" (string),
            + Brand(object) - Details about the product’s brand.
                + ManufacturerId: "msf",
                + BrandId: "msf",
                + Description: "Microsoft"
            + Category(object) - The multilevel categorization of the product (from Intcomex’s internal categorization structure) 
            + CategoryId: "sfw",
            + Description: "Software",
        + EsdFulfillmentStatus(object) - The status of the ESD fulfillments.
          + Status:"ok" (string)
        + EsdFulfillments(array) Contains all the ESD fulfillments obtained for the product.
        + EsdFulfillment(object)
              + FulfillmentDate:`2015-08-20T11:34:28.13` (string)
              + PoNumber:"XGT1160485" (string)
              + Products(array)
              + Product(object)
               + Mpn : "",
               + Token(object) - Object
                + Description :""  - Descripiton
                + ProductKey:"GKKY9-FHDJT-V6GJF-7WXH6-8QKC4"
                + Type : "PIN",
               + Links(array)
               + Link(object)
                + Description: "Points to a Microsoft website to redeem the token provided.",
                + Uri:"http://vms95us.intcomex.com:8080/Guatemala/Web/api/ESDStandardApi/DownloadLink?downloadKey=658efb8b-0def-4d53-a6e4-fdbd6d1fa0d4",
                + Type: "Redemption",
                + ExpirationDate:"0001-01-01T00:00:00"
             + Instructions:"",
             + DescriptionKey:2 (number)
        + TokenCount:0 (number)
    + Body
    
            [ { "Sku": "SE001MSE02", "Mpn": "AAA-01147", 
            "Manufacturer": 
            { "ManufacturerId": "msf", "Description": "Microsoft" },
            "Brand": { 
            "ManufacturerId": "msf", 
            "BrandId": "msf", "Description": "Microsoft" 
            }, 
            "Category":
            { "CategoryId": "sfw", "Description": "Software",
            "Subcategories": 
            [ { "CategoryId": "sfw.business", 
            "Description": "Aplicaciones para Negocio y Oficina",
            "Subcategories": [] } ] }, 
            "Description": "Microsoft Access 2013 - Licencia - 1 PC - descarga - 32/64-bit, ESD, Click-to-Run - Win - Español",
            "EsdFulfillmentStatus": "Ok", 
            "EsdFulfillments":
            [ { "FulfillmentDate": "2015-08-20T11:16:23.09", 
              "PoNumber": "XGT-1160483", 
              "Products":
               [ { "Mpn": "AAA-01147", 
               "Tokens": [ { "Description": "Token which must be exchanged for a key to activate a product.", "ProductKey": "WYV3H-YPXYJ-X9WVP-4DJ2V-XRQH8", "Type": "PIN", "Status": { "Status": null, "Description": null, "PromotionName": null, "RedemptionDate": null, "LastStatusUpdate": null } } ], 
               "Links": [ { "Description": "Points to a Microsoft website to redeem the token provided.", "Uri": "http://vms95us.intcomex.com:8080/Guatemala/Web/api/ESDStandardApi/DownloadLink?downloadKey=b7ab67ad-e032-49e9-80e6-faa88451af42", "Type": "Redemption", "ExpirationDate": "0001-01-01T00:00:00" } ] } ],
               "Instructions": null, "DescriptionKey": 2 } ], "TokenCount": 0 } ]


## Obtain Esd Status [/{countryCode}/esd/{productKey}/status]

The GetProductKeyStatus method can be used to obtain the status of a specific product key obtained
after purchasing an ESD product. The response returned displays the status of the product key along with
the description of the product it belongs to and expiration date if it applies.


+ Parameters
      + countryCode : gt (string, required) - gt
   

### Obtain Status [GET]



+ Parameters
 
     + productKey:`WYV3H-YPXYJ-X9WVP-4DJ2V-XRQH8` (string, required) - Product Key.
 
+ Request


      This resource is protected via oauth2
      
  
    
 + Headers
        
            Authorization: Bearer {{Authtoken}}

+ Response 200 (application/json)
    
    + Attributes
     + StatusObject(object)
      + Status:"Activated" (string)
      + Description:`OMXTC-11135 O15 - Access 2013 - Perp - Token - Retail - WW` (string)
      + PromotionName:"" (string)
      + LastStatusUpdate: `0001-01-01T00:00:00` (string)
    + Body
    
            {
             "Status": "Activated",
             "Description": "OMXTC-11135 O15 - Access 2013 - Perp - Token - Retail - WW",
             "PromotionName": "",
             "RedemptionDate": null,
             "LastStatusUpdate": "0001-01-01T00:00:00"
            }



