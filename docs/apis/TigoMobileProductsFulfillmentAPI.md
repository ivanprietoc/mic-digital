FORMAT: 1A
HOST: https://test.api.tigo.com/v1/tigo/mobile

# Tigo Mobile Products Fulfillment API
Provides Information and Methods about the Mobile Products a Tigo Mobile Subscriber may acquire.

## Authentication
1. Each Client application MUST register and request its client credentials from Tigo/Millicom.  
2. With your client credentials, an **access_token** needs to be obtained. Please see http://docs.tigooauth.apiary.io on how to obtain access tokens
3. In each request, you need to present the **access_token** in the HTTP **Authorization** header like this:  
`Authorization: Bearer <access_token goes here>`

# Group Fulfillment
These are the APIs related to the particular Products Tigo Mobile Subscribers can acquire
using the local "Fulfillment Engine".

## Products Collection [/{country}/fulfillment/subscribers/{msisdn}/products{?acquisitionTypeId}]
Represents an Array of **products** objects that may be acquired by 
a particular Tigo Mobile Subscriber identified by its `msisdn` 
over a specific sales channel identified by the OAuth `clientId` (configuration) 
filtered by payment method identified by `acquisitionTypeId`.

Each **product** object has the following attributes:

- **acquisitionMethods**: (array of **acquistionMethod** objects) contains information on the different prices and acquisition methods available for this product.
- **classifications**: (string or array of strings) it describes the product type and category hierarchy. multiple values possible.
- **description**: (string) Human readable full description of the product.
- **durationTime**: (number) validity time for the package/product in hours. For subscriptions with a renewal period, expect `-1`.
- **id**: (number) unique Product Id, this is the code that should be use when acquiring a product for the customer.
- **name**: (string) Human readable name for the product/package.,
- **planTypes**: (array of strings) list of billing account types compatible with the product. Example: "PREPAID_HS", "POSTPAID_HS".
- **segments**: (array of strings) list of customer segments white-listed to acquire the product. Example: "Navidad", "Default", "Internet Increible"
- **shortName**: (string) Human-readable short name for the Product.

Each **acquisitionMethod** object contains the following attributes:

- **acquisitionMethod**: (string) name of acquisition method. The following are known acquistion Methods:
    - `PURCHASE` means The Product is available for purchase
    - `LOAN` means The product is available for lending
    - `ACTIVATION` means the product is available for free activation (no charge)
    - `DEACTIVATION` means the product can be un-subscribed or canceled
    - `PURCHASE and LOAN` means the product is available for Purchase and Lending simultaneously
- **id**: (number) Id for the acquition Method. This is equivalent to `acquisitionTypeId` in the Request. Used to filter out products by their available payment methods as follows:
    - `1` - products for PURCHASE
    - `3` - products for LOAN
    - `4` - products for ACTIVATION
    - `6` - products for DEACTIVATION
    - `7` - products for PURCHASE and LOAN simultaneously
- **priceList**: ( **priceList** Object or Array of **priceList** objects) array of Payment Methods each with its corresponding Pricing for this Product.

Each **PriceList** object containst the following attributes:

- **currentPrice**: (number) The Price in local currency for this particular Payment Method.
- **paymentMethodId**: (number) unique Id for this payment method. This parameter should be used as `desiredPaymentMethod` when acquiring a product.
- **paymentMethodName**: (string) name of the Payment method. The following are known Payment Methods and their meaning:
    - `CHARGE_ACCOUNT` this is the price charged at product activation
    - `DAILY_CHARGE` this is the price charged every day, applicable to subscription products only.
    - `LoanConnector` this is the price to Loan the product, which will be paid in the next recharge (top-up).
    - `DEFAULT_PRICE` this is the default price for activating the product, usually 0, use as last resort.
- **priceParameters** (array of Key-Value objects, Optional) further specify the price components. Used for Loan pricing, were the PRICE is composed of COST and FEE.
    - **paramKey** (string) the Price component name, the following are know values:
        - `COST` - the lending cost
        - `FEE` - the lending fee
    - **paramValue** (number) the price component (amount) in local currency.
    
### Query Eligible Products for Subscriber [GET]

+ Parameters
    + country: `py` (enum[string], required) - Country code of the Tigo Market
        + Members
            + `py` - Paraguay
            + `sv` - El Salvador
    + msisdn: `595981400007` (string, required) - Mobile number of tigo subscriber in international format.
    + acquisitionTypeId: `1` (enum[string], optional) - Filter products that have a specific Acquisition Method Identifier.
        + Members
            + `1` - products for PURCHASE
            + `3` - products for LOAN
            + `4` - products for ACTIVATION
            + `6` - products for DEACTIVATION
            + `7` - products for PURCHASE and LOAN simultaneously


+ Request

    + Headers
    
            Authorization: Bearer {access_token}

+ Response 200 (application/json)
    
    + Attributes (ProductsResponse)
                
    + Body

            {
              "responseCode": 0,
              "responseMessage": "Operation Finished OK",
              "customer": {
                "coreBalance": 81000,
                "customerSegment": "Internet Increible",
                "planType": "PREPAGO HANDSET",
                "planTypeId": 1
              },
              "products": [
                {
                  "acquisitionMethods": [
                    {
                      "acquisitionMethod": "PURCHASE",
                      "id": 1,
                      "priceList": {
                        "currentPrice": 2500,
                        "paymentMethodId": 1,
                        "paymentMethodName": "CHARGE_ACCOUNT"
                      }
                    },
                    {
                      "acquisitionMethod": "ACTIVATION",
                      "id": 4,
                      "priceList": {
                        "currentPrice": 0,
                        "paymentMethodId": 0,
                        "paymentMethodName": "DEFAULT_PRICE"
                      }
                    }
                  ],
                  "classifications": "ROOT/PAQUETIGOS/Internet/Musica+Internet/",
                  "description": "Deezer x dia 2500Gs",
                  "durationTime": 24,
                  "id": 321,
                  "name": "Deezer x dia 2500Gs",
                  "planTypes": "PREPAID_HS",
                  "segments": [
                    "Default",
                    "Internet Increible"
                  ],
                  "shortName": "Deezer 70MB + 30MB Extras"
                },
                {
                  "acquisitionMethods": [
                    {
                      "acquisitionMethod": "PURCHASE",
                      "id": 1,
                      "priceList": [
                        {
                          "currentPrice": 2000,
                          "paymentMethodId": 1,
                          "paymentMethodName": "CHARGE_ACCOUNT"
                        },
                        {
                          "currentPrice": 2200,
                          "paymentMethodId": 10,
                          "paymentMethodName": "LoanConnector"
                        }
                      ]
                    },
                    {
                      "acquisitionMethod": "ACTIVATION",
                      "id": 4,
                      "priceList": {
                        "currentPrice": 0,
                        "paymentMethodId": 0,
                        "paymentMethodName": "DEFAULT_PRICE"
                      }
                    }
                  ],
                  "classifications": "ROOT/PAQUETIGOS/Internet/Promo Dia/",
                  "description": "80MB+45MBx2000Gsx24hs",
                  "durationTime": 24,
                  "id": 399,
                  "name": "80MB+45MBx2000Gsx24hs",
                  "planTypes": [
                    "PREPAID_HS",
                    "POSTPAID_HS",
                    "PREPAID_DC",
                    "POSTPAID_DC"
                  ],
                  "segments": "Internet Increible",
                  "shortName": "Promo WhatsApp +80MB +45MB MAS"
                },
                {
                  "acquisitionMethods": [
                    {
                      "acquisitionMethod": "PURCHASE",
                      "id": 1,
                      "priceList": [
                        {
                          "currentPrice": 1500,
                          "paymentMethodId": 1,
                          "paymentMethodName": "CHARGE_ACCOUNT"
                        },
                        {
                          "currentPrice": 1500,
                          "paymentMethodId": 20,
                          "paymentMethodName": "DAILY_CHARGE"
                        }
                      ]
                    },
                    {
                      "acquisitionMethod": "DEACTIVATION",
                      "id": 6
                    }
                  ],
                  "classifications": [
                    "ROOT/PAQUETIGOS/Invencible Increible/",
                    "ROOT/PAQUETIGOS/Internet/Z|Internet Increible - Autocompra/"
                  ],
                  "description": "Promo Whatsapp +50MB+30MB EXTRAS x DIA. Activa solo una vez y disfruta todos los d�as!",
                  "durationTime": -1,
                  "id": 394,
                  "name": "50MB+30MBx1500Gs",
                  "planTypes": [
                    "PREPAID_HS",
                    "POSTPAID_HS",
                    "CONTROL_ACCOUNT",
                    "PREPAID_DC",
                    "POSTPAID_DC"
                  ],
                  "segments": [
                    "Navidad",
                    "Default",
                    "Internet Increible"
                  ],
                  "shortName": "Internet Incre�ble 1.500Gs"
                },
                {
                  "acquisitionMethods": [
                    {
                      "acquisitionMethod": "PURCHASE",
                      "id": 1,
                      "priceList": {
                        "currentPrice": 0,
                        "paymentMethodId": 1,
                        "paymentMethodName": "CHARGE_ACCOUNT"
                      }
                    },
                    {
                      "acquisitionMethod": "ACTIVATION",
                      "id": 4,
                      "priceList": {
                        "currentPrice": 0,
                        "paymentMethodId": 0,
                        "paymentMethodName": "DEFAULT_PRICE"
                      }
                    }
                  ],
                  "classifications": [
                    "ROOT/PAQUETIGOS/Internet/",
                    "ROOT/PAQUETIGOS/LLAMADAS/A Tigo/"
                  ],
                  "description": "50min todo destino+100MB+Facebook+Whatsapp Libres. Validez 48hs.",
                  "durationTime": 48,
                  "id": 387,
                  "name": "Promo Tigo Shop",
                  "planTypes": [
                    "PREPAID_HS",
                    "POSTPAID_HS"
                  ],
                  "segments": [
                    "Navidad",
                    "Default",
                    "Internet Increible"
                  ],
                  "shortName": "Regalo 100Mb +50min Todo Dest "
                },
                {
                  "acquisitionMethods": [
                    {
                      "acquisitionMethod": "PURCHASE",
                      "id": 1,
                      "priceList": [
                        {
                          "currentPrice": 1500,
                          "paymentMethodId": 1,
                          "paymentMethodName": "CHARGE_ACCOUNT"
                        },
                        {
                          "currentPrice": 1500,
                          "paymentMethodId": 20,
                          "paymentMethodName": "DAILY_CHARGE"
                        }
                      ]
                    },
                    {
                      "acquisitionMethod": "DEACTIVATION",
                      "id": 6
                    }
                  ],
                  "classifications": [
                    "ROOT/PAQUETIGOS/Invencible Increible/",
                    "ROOT/PAQUETIGOS/Internet/Z|Internet Increible - Autocompra/"
                  ],
                  "description": "Promo Whatsapp +50MB+30MB EXTRAS x DIA. Activa solo una vez y disfruta todos los d�as! - Automatico",
                  "durationTime": -1,
                  "id": 435,
                  "name": "50MB+30MBx1500Gs Auto",
                  "planTypes": [
                    "PREPAID_HS",
                    "POSTPAID_HS",
                    "PREPAID_DC",
                    "POSTPAID_DC"
                  ],
                  "segments": [
                    "Navidad",
                    "Default",
                    "Internet Increible"
                  ],
                  "shortName": "II 50m Aut"
                },
                {
                  "acquisitionMethods": [
                    {
                      "acquisitionMethod": "PURCHASE",
                      "id": 1,
                      "priceList": {
                        "currentPrice": 3000,
                        "paymentMethodId": 1,
                        "paymentMethodName": "CHARGE_ACCOUNT"
                      }
                    },
                    {
                      "acquisitionMethod": "ACTIVATION",
                      "id": 4,
                      "priceList": {
                        "currentPrice": 0,
                        "paymentMethodId": 0,
                        "paymentMethodName": "DEFAULT_PRICE"
                      }
                    }
                  ],
                  "classifications": "ROOT/PAQUETIGOS/Internet/Promo Dia/",
                  "description": "200MBx3000x24hs",
                  "durationTime": 24,
                  "id": 340,
                  "name": "200MBx3000x24hs",
                  "planTypes": [
                    "PREPAID_HS",
                    "POSTPAID_HS",
                    "CONTROL_ACCOUNT",
                    "PREPAID_DC",
                    "POSTPAID_DC",
                    "TRAVELER_SIM"
                  ],
                  "segments": [
                    "Default",
                    "Internet Increible"
                  ],
                  "shortName": "Promo WhatsApp + 200MB"
                },
                {
                  "acquisitionMethods": [
                    {
                      "acquisitionMethod": "PURCHASE",
                      "id": 1,
                      "priceList": [
                        {
                          "currentPrice": 1000,
                          "paymentMethodId": 1,
                          "paymentMethodName": "CHARGE_ACCOUNT"
                        },
                        {
                          "currentPrice": 1000,
                          "paymentMethodId": 20,
                          "paymentMethodName": "DAILY_CHARGE"
                        }
                      ]
                    },
                    {
                      "acquisitionMethod": "DEACTIVATION",
                      "id": 6
                    }
                  ],
                  "classifications": [
                    "ROOT/PAQUETIGOS/Invencible Increible/",
                    "ROOT/PAQUETIGOS/Internet/Z|Internet Increible - Autocompra/"
                  ],
                  "description": "Promo Whatsapp +25MB+15MB EXTRAS x DIA. Activa solo una vez y disfruta todos los d�as!",
                  "durationTime": -1,
                  "id": 395,
                  "name": "25MB+15MBx1000Gs",
                  "planTypes": [
                    "PREPAID_HS",
                    "POSTPAID_HS",
                    "PREPAID_DC",
                    "POSTPAID_DC"
                  ],
                  "segments": [
                    "Navidad",
                    "Default",
                    "Internet Increible"
                  ],
                  "shortName": "Internet Incre�ble 1.000Gs"
                },
                {
                  "acquisitionMethods": [
                    {
                      "acquisitionMethod": "PURCHASE",
                      "id": 1,
                      "priceList": [
                        {
                          "currentPrice": 8000,
                          "paymentMethodId": 10,
                          "paymentMethodName": "LoanConnector"
                        },
                        {
                          "currentPrice": 8000,
                          "paymentMethodId": 1,
                          "paymentMethodName": "CHARGE_ACCOUNT"
                        }
                      ]
                    },
                    {
                      "acquisitionMethod": "LOAN",
                      "id": 3,
                      "priceList": [
                        {
                          "currentPrice": 8000,
                          "paymentMethodId": 10,
                          "paymentMethodName": "LoanConnector"
                        },
                        {
                          "currentPrice": 8000,
                          "paymentMethodId": 1,
                          "paymentMethodName": "CHARGE_ACCOUNT"
                        }
                      ]
                    }
                  ],
                  "classifications": "ROOT/PAQUETIGOS/Internet/Promo Dia/",
                  "description": "FUTBOLx8000Gsx24hs",
                  "durationTime": 24,
                  "id": 404,
                  "name": "FUTBOLx8000Gsx24hs",
                  "planTypes": [
                    "PREPAID_HS",
                    "POSTPAID_HS",
                    "PREPAID_DC",
                    "POSTPAID_DC"
                  ],
                  "segments": [
                    "Default",
                    "Internet Increible"
                  ],
                  "shortName": "Paquete Futbol + 150MB"
                },
                {
                  "acquisitionMethods": [
                    {
                      "acquisitionMethod": "PURCHASE",
                      "id": 1,
                      "priceList": [
                        {
                          "currentPrice": 1000,
                          "paymentMethodId": 1,
                          "paymentMethodName": "CHARGE_ACCOUNT"
                        },
                        {
                          "currentPrice": 1100,
                          "paymentMethodId": 10,
                          "paymentMethodName": "LoanConnector"
                        }
                      ]
                    },
                    {
                      "acquisitionMethod": "ACTIVATION",
                      "id": 4,
                      "priceList": {
                        "currentPrice": 0,
                        "paymentMethodId": 0,
                        "paymentMethodName": "DEFAULT_PRICE"
                      }
                    }
                  ],
                  "classifications": "ROOT/PAQUETIGOS/Internet/Promo Dia/",
                  "description": "25MB+15MBx1000Gsx24hs",
                  "durationTime": 24,
                  "id": 397,
                  "name": "25MB+15MBx1000Gsx24hs",
                  "planTypes": [
                    "PREPAID_HS",
                    "POSTPAID_HS",
                    "PREPAID_DC",
                    "POSTPAID_DC"
                  ],
                  "segments": "Internet Increible",
                  "shortName": "Promo WhatsApp +25MB +15MB MAS"
                },
                {
                  "acquisitionMethods": [
                    {
                      "acquisitionMethod": "PURCHASE",
                      "id": 1,
                      "priceList": [
                        {
                          "currentPrice": 2500,
                          "paymentMethodId": 10,
                          "paymentMethodName": "LoanConnector"
                        },
                        {
                          "currentPrice": 2500,
                          "paymentMethodId": 1,
                          "paymentMethodName": "CHARGE_ACCOUNT"
                        }
                      ]
                    },
                    {
                      "acquisitionMethod": "ACTIVATION",
                      "id": 4,
                      "priceList": {
                        "currentPrice": 0,
                        "paymentMethodId": 0,
                        "paymentMethodName": "DEFAULT_PRICE"
                      }
                    },
                    {
                      "acquisitionMethod": "LOAN",
                      "id": 3,
                      "priceList": [
                        {
                          "currentPrice": 65,
                          "paymentMethodId": 10,
                          "paymentMethodName": "LoanConnector"
                        },
                        {
                          "currentPrice": 2500,
                          "paymentMethodId": 1,
                          "paymentMethodName": "CHARGE_ACCOUNT"
                        }
                      ]
                    }
                  ],
                  "classifications": [
                    "ROOT/PAQUETIGOS/Internet/Promo Dia/",
                    "ROOT/PAQUETIGOS/COMBOS/"
                  ],
                  "description": "65MB+25Min+65SMSXGs2500X1D",
                  "durationTime": 24,
                  "id": 429,
                  "name": "65MB+25Min+65SMSXGs2500X1D",
                  "planTypes": [
                    "PREPAID_HS",
                    "POSTPAID_HS",
                    "PREPAID_DC",
                    "POSTPAID_DC"
                  ],
                  "segments": "Internet Increible",
                  "shortName": "65MB+25MIN"
                },
                {
                  "acquisitionMethods": [
                    {
                      "acquisitionMethod": "PURCHASE",
                      "id": 1,
                      "priceList": [
                        {
                          "currentPrice": 2000,
                          "paymentMethodId": 1,
                          "paymentMethodName": "CHARGE_ACCOUNT"
                        },
                        {
                          "currentPrice": 2200,
                          "paymentMethodId": 10,
                          "paymentMethodName": "LoanConnector",
                          "priceParameters": [
                            {
                              "paramKey": "FEE",
                              "paramValue": 200
                            },
                            {
                              "paramKey": "COST",
                              "paramValue": 2000
                            }
                          ]
                        }
                      ]
                    },
                    {
                      "acquisitionMethod": "ACTIVATION",
                      "id": 4,
                      "priceList": {
                        "currentPrice": 0,
                        "paymentMethodId": 0,
                        "paymentMethodName": "DEFAULT_PRICE"
                      }
                    },
                    {
                      "acquisitionMethod": "LOAN",
                      "id": 3,
                      "priceList": [
                        {
                          "currentPrice": 2000,
                          "paymentMethodId": 1,
                          "paymentMethodName": "CHARGE_ACCOUNT"
                        },
                        {
                          "currentPrice": 2200,
                          "paymentMethodId": 10,
                          "paymentMethodName": "LoanConnector",
                          "priceParameters": [
                            {
                              "paramKey": "COST",
                              "paramValue": 2000
                            },
                            {
                              "paramKey": "FEE",
                              "paramValue": 200
                            }
                          ]
                        }
                      ]
                    },
                    {
                      "acquisitionMethod": "PURCHASE and LOAN",
                      "id": 7
                    }
                  ],
                  "classifications": "ROOT/PAQUETIGOS/LLAMADAS/",
                  "description": "15 min a todo destino.",
                  "durationTime": 24,
                  "id": 260,
                  "name": "15MINx2000Gs",
                  "planTypes": [
                    "PREPAID_HS",
                    "POSTPAID_HS"
                  ],
                  "segments": [
                    "Navidad",
                    "Default",
                    "Internet Increible"
                  ],
                  "shortName": "15 Minutos a Todo Destino"
                },
                {
                  "acquisitionMethods": [
                    {
                      "acquisitionMethod": "PURCHASE",
                      "id": 1,
                      "priceList": {
                        "currentPrice": 3000,
                        "paymentMethodId": 1,
                        "paymentMethodName": "CHARGE_ACCOUNT"
                      }
                    },
                    {
                      "acquisitionMethod": "ACTIVATION",
                      "id": 4,
                      "priceList": {
                        "currentPrice": 0,
                        "paymentMethodId": 0,
                        "paymentMethodName": "DEFAULT_PRICE"
                      }
                    }
                  ],
                  "classifications": [
                    "ROOT/PAQUETIGOS/",
                    "ROOT/PAQUETIGOS/LLAMADAS/"
                  ],
                  "description": "25 min a todo destino",
                  "durationTime": 24,
                  "id": 284,
                  "name": "25MINx3000Gs",
                  "planTypes": [
                    "PREPAID_HS",
                    "POSTPAID_HS"
                  ],
                  "segments": [
                    "Navidad",
                    "Default",
                    "Internet Increible"
                  ],
                  "shortName": "25 Minutos a Todo Destino"
                },
                {
                  "acquisitionMethods": [
                    {
                      "acquisitionMethod": "PURCHASE",
                      "id": 1,
                      "priceList": {
                        "currentPrice": 800,
                        "paymentMethodId": 1,
                        "paymentMethodName": "CHARGE_ACCOUNT"
                      }
                    },
                    {
                      "acquisitionMethod": "ACTIVATION",
                      "id": 4,
                      "priceList": {
                        "currentPrice": 0,
                        "paymentMethodId": 0,
                        "paymentMethodName": "DEFAULT_PRICE"
                      }
                    }
                  ],
                  "classifications": "ROOT/PAQUETIGOS/MENSAJES/",
                  "description": "20 SMS a todo destino x 800 Gs.",
                  "durationTime": 24,
                  "id": 364,
                  "name": "20SMSx800Gs",
                  "planTypes": [
                    "PREPAID_HS",
                    "POSTPAID_HS",
                    "PREPAID_DC",
                    "POSTPAID_DC"
                  ],
                  "segments": [
                    "Navidad",
                    "Default",
                    "Internet Increible"
                  ],
                  "shortName": "20 SMS a Todo Destino"
                },
                {
                  "acquisitionMethods": [
                    {
                      "acquisitionMethod": "PURCHASE",
                      "id": 1,
                      "priceList": [
                        {
                          "currentPrice": 1500,
                          "paymentMethodId": 1,
                          "paymentMethodName": "CHARGE_ACCOUNT"
                        },
                        {
                          "currentPrice": 1650,
                          "paymentMethodId": 10,
                          "paymentMethodName": "LoanConnector"
                        }
                      ]
                    },
                    {
                      "acquisitionMethod": "ACTIVATION",
                      "id": 4,
                      "priceList": {
                        "currentPrice": 0,
                        "paymentMethodId": 0,
                        "paymentMethodName": "DEFAULT_PRICE"
                      }
                    }
                  ],
                  "classifications": "ROOT/PAQUETIGOS/Internet/Promo Dia/",
                  "description": "50MB+30MBx1500Gsx24hs",
                  "durationTime": 24,
                  "id": 398,
                  "name": "50MB+30MBx1500Gsx24hs",
                  "planTypes": [
                    "PREPAID_HS",
                    "POSTPAID_HS",
                    "PREPAID_DC",
                    "POSTPAID_DC"
                  ],
                  "segments": "Internet Increible",
                  "shortName": "Promo WhatsApp +50MB +30MB MAS"
                },
                {
                  "acquisitionMethods": [
                    {
                      "acquisitionMethod": "PURCHASE",
                      "id": 1,
                      "priceList": [
                        {
                          "currentPrice": 300,
                          "paymentMethodId": 1,
                          "paymentMethodName": "CHARGE_ACCOUNT"
                        },
                        {
                          "currentPrice": 330,
                          "paymentMethodId": 10,
                          "paymentMethodName": "LoanConnector",
                          "priceParameters": [
                            {
                              "paramKey": "FEE",
                              "paramValue": 30
                            },
                            {
                              "paramKey": "COST",
                              "paramValue": 300
                            }
                          ]
                        }
                      ]
                    },
                    {
                      "acquisitionMethod": "ACTIVATION",
                      "id": 4,
                      "priceList": {
                        "currentPrice": 0,
                        "paymentMethodId": 0,
                        "paymentMethodName": "DEFAULT_PRICE"
                      }
                    },
                    {
                      "acquisitionMethod": "LOAN",
                      "id": 3,
                      "priceList": [
                        {
                          "currentPrice": 300,
                          "paymentMethodId": 1,
                          "paymentMethodName": "CHARGE_ACCOUNT"
                        },
                        {
                          "currentPrice": 330,
                          "paymentMethodId": 10,
                          "paymentMethodName": "LoanConnector",
                          "priceParameters": [
                            {
                              "paramKey": "COST",
                              "paramValue": 300
                            },
                            {
                              "paramKey": "FEE",
                              "paramValue": 30
                            }
                          ]
                        }
                      ]
                    },
                    {
                      "acquisitionMethod": "PURCHASE and LOAN",
                      "id": 7
                    }
                  ],
                  "classifications": "ROOT/PAQUETIGOS/LLAMADAS/A Tigo/",
                  "description": "3min x 300Gs (ahorro 85%)",
                  "durationTime": 24,
                  "id": 257,
                  "name": "3min300gs",
                  "planTypes": [
                    "PREPAID_HS",
                    "POSTPAID_HS"
                  ],
                  "segments": [
                    "Navidad",
                    "Default",
                    "Internet Increible"
                  ],
                  "shortName": "3 minutos"
                },
                {
                  "acquisitionMethods": {
                    "acquisitionMethod": "PURCHASE",
                    "id": 1,
                    "priceList": {
                      "currentPrice": 3000,
                      "paymentMethodId": 0,
                      "paymentMethodName": "DEFAULT_PRICE"
                    }
                  },
                  "classifications": [
                    "ROOT/PAQUETIGOS/MENSAJES/",
                    "ROOT/PAQUETIGOS/MENSAJES/MENSAJES A TIGO/"
                  ],
                  "description": "ILIMITADO de Tigo a Tigo x 3000Gs x 3 dias",
                  "durationTime": 72,
                  "id": 279,
                  "name": "Ilim3000gs",
                  "planTypes": [
                    "PREPAID_HS",
                    "POSTPAID_HS"
                  ],
                  "segments": [
                    "Navidad",
                    "Default",
                    "Internet Increible"
                  ],
                  "shortName": "SMS Ilimitado a Tigo"
                },
                {
                  "acquisitionMethods": [
                    {
                      "acquisitionMethod": "PURCHASE",
                      "id": 1,
                      "priceList": [
                        {
                          "currentPrice": 1500,
                          "paymentMethodId": 0,
                          "paymentMethodName": "DEFAULT_PRICE"
                        },
                        {
                          "currentPrice": 1650,
                          "paymentMethodId": 10,
                          "paymentMethodName": "LoanConnector",
                          "priceParameters": [
                            {
                              "paramKey": "FEE",
                              "paramValue": 150
                            },
                            {
                              "paramKey": "COST",
                              "paramValue": 1500
                            }
                          ]
                        }
                      ]
                    },
                    {
                      "acquisitionMethod": "LOAN",
                      "id": 3,
                      "priceList": [
                        {
                          "currentPrice": 1500,
                          "paymentMethodId": 0,
                          "paymentMethodName": "DEFAULT_PRICE"
                        },
                        {
                          "currentPrice": 1650,
                          "paymentMethodId": 10,
                          "paymentMethodName": "LoanConnector",
                          "priceParameters": [
                            {
                              "paramKey": "COST",
                              "paramValue": 1500
                            },
                            {
                              "paramKey": "FEE",
                              "paramValue": 150
                            }
                          ]
                        }
                      ]
                    },
                    {
                      "acquisitionMethod": "PURCHASE and LOAN",
                      "id": 7
                    }
                  ],
                  "classifications": "ROOT/PAQUETIGOS/MENSAJES/",
                  "description": "ILIMITADO x 1500Gs (a todas las operadoras)",
                  "durationTime": 24,
                  "id": 275,
                  "name": "Ilim1500gs",
                  "planTypes": [
                    "PREPAID_HS",
                    "POSTPAID_HS"
                  ],
                  "segments": [
                    "Navidad",
                    "Default",
                    "Internet Increible"
                  ],
                  "shortName": "Ilimitado Tigo+50SMS Todo Dest"
                },
                {
                  "acquisitionMethods": [
                    {
                      "acquisitionMethod": "PURCHASE",
                      "id": 1,
                      "priceList": {
                        "currentPrice": 0,
                        "paymentMethodId": 1,
                        "paymentMethodName": "CHARGE_ACCOUNT"
                      }
                    },
                    {
                      "acquisitionMethod": "DEACTIVATION",
                      "id": 6
                    }
                  ],
                  "classifications": [
                    "ROOT/SUSCRIPCION/",
                    "ROOT/PAQUETIGOS/Invencible Increible/"
                  ],
                  "description": "Llama y mensajea a TODAS las operadoras a la MEJOR tarifa. Tu saldo NO VENCE si no usas y tu beneficio es para siempre!",
                  "durationTime": -1,
                  "id": 333,
                  "name": "Saldo Invencible",
                  "planTypes": [
                    "PREPAID_HS",
                    "POSTPAID_HS",
                    "PREPAID_DC",
                    "POSTPAID_DC"
                  ],
                  "segments": [
                    "Navidad",
                    "Default",
                    "Internet Increible"
                  ],
                  "shortName": "Saldo Invencible"
                },
                {
                  "acquisitionMethods": [
                    {
                      "acquisitionMethod": "PURCHASE",
                      "id": 1,
                      "priceList": [
                        {
                          "currentPrice": 2000,
                          "paymentMethodId": 1,
                          "paymentMethodName": "CHARGE_ACCOUNT"
                        },
                        {
                          "currentPrice": 2000,
                          "paymentMethodId": 20,
                          "paymentMethodName": "DAILY_CHARGE"
                        }
                      ]
                    },
                    {
                      "acquisitionMethod": "DEACTIVATION",
                      "id": 6
                    }
                  ],
                  "classifications": [
                    "ROOT/PAQUETIGOS/Invencible Increible/",
                    "ROOT/PAQUETIGOS/Internet/Z|Internet Increible - Autocompra/"
                  ],
                  "description": "Promo Whatsapp +80MB+45MB EXTRAS x DIA. Activa solo una vez y disfruta todos los d�as!",
                  "durationTime": -1,
                  "id": 396,
                  "name": "80MB+45MBx2000Gs",
                  "planTypes": [
                    "PREPAID_HS",
                    "POSTPAID_HS",
                    "PREPAID_DC",
                    "POSTPAID_DC"
                  ],
                  "segments": [
                    "Navidad",
                    "Default",
                    "Internet Increible"
                  ],
                  "shortName": "Internet Incre�ble 2.000Gs"
                },
                {
                  "acquisitionMethods": [
                    {
                      "acquisitionMethod": "PURCHASE",
                      "id": 1,
                      "priceList": [
                        {
                          "currentPrice": 1000,
                          "paymentMethodId": 1,
                          "paymentMethodName": "CHARGE_ACCOUNT"
                        },
                        {
                          "currentPrice": 1000,
                          "paymentMethodId": 20,
                          "paymentMethodName": "DAILY_CHARGE"
                        }
                      ]
                    },
                    {
                      "acquisitionMethod": "DEACTIVATION",
                      "id": 6
                    }
                  ],
                  "classifications": [
                    "ROOT/PAQUETIGOS/Invencible Increible/",
                    "ROOT/PAQUETIGOS/Internet/Z|Internet Increible - Autocompra/"
                  ],
                  "description": "Promo Whatsapp +25MB+15MB EXTRAS x DIA. Activa solo una vez y disfruta todos los d�as! - Automatico",
                  "durationTime": -1,
                  "id": 436,
                  "name": "25MB+15MBx1000Gs Auto",
                  "planTypes": [
                    "PREPAID_HS",
                    "POSTPAID_HS",
                    "PREPAID_DC",
                    "POSTPAID_DC"
                  ],
                  "segments": [
                    "Navidad",
                    "Default",
                    "Internet Increible"
                  ],
                  "shortName": "II 25m Aut"
                },
                {
                  "acquisitionMethods": [
                    {
                      "acquisitionMethod": "PURCHASE",
                      "id": 1,
                      "priceList": [
                        {
                          "currentPrice": 2000,
                          "paymentMethodId": 1,
                          "paymentMethodName": "CHARGE_ACCOUNT"
                        },
                        {
                          "currentPrice": 2000,
                          "paymentMethodId": 20,
                          "paymentMethodName": "DAILY_CHARGE"
                        }
                      ]
                    },
                    {
                      "acquisitionMethod": "DEACTIVATION",
                      "id": 6
                    }
                  ],
                  "classifications": [
                    "ROOT/PAQUETIGOS/Invencible Increible/",
                    "ROOT/PAQUETIGOS/Internet/Z|Internet Increible - Autocompra/"
                  ],
                  "description": "Promo Whatsapp +80MB+45MB EXTRAS x DIA. Activa solo una vez y disfruta todos los d�as! - Automatico",
                  "durationTime": -1,
                  "id": 437,
                  "name": "80MB+45MBx2000Gs Auto",
                  "planTypes": [
                    "PREPAID_HS",
                    "POSTPAID_HS",
                    "PREPAID_DC",
                    "POSTPAID_DC"
                  ],
                  "segments": [
                    "Navidad",
                    "Default",
                    "Internet Increible"
                  ],
                  "shortName": "II 80m Aut"
                },
                {
                  "acquisitionMethods": [
                    {
                      "acquisitionMethod": "PURCHASE",
                      "id": 1,
                      "priceList": [
                        {
                          "currentPrice": 1000,
                          "paymentMethodId": 0,
                          "paymentMethodName": "DEFAULT_PRICE"
                        },
                        {
                          "currentPrice": 1100,
                          "paymentMethodId": 10,
                          "paymentMethodName": "LoanConnector",
                          "priceParameters": [
                            {
                              "paramKey": "FEE",
                              "paramValue": 100
                            },
                            {
                              "paramKey": "COST",
                              "paramValue": 1000
                            }
                          ]
                        }
                      ]
                    },
                    {
                      "acquisitionMethod": "ACTIVATION",
                      "id": 4,
                      "priceList": {
                        "currentPrice": 0,
                        "paymentMethodId": 0,
                        "paymentMethodName": "DEFAULT_PRICE"
                      }
                    },
                    {
                      "acquisitionMethod": "LOAN",
                      "id": 3,
                      "priceList": [
                        {
                          "currentPrice": 1000,
                          "paymentMethodId": 0,
                          "paymentMethodName": "DEFAULT_PRICE"
                        },
                        {
                          "currentPrice": 1100,
                          "paymentMethodId": 10,
                          "paymentMethodName": "LoanConnector",
                          "priceParameters": [
                            {
                              "paramKey": "COST",
                              "paramValue": 1000
                            },
                            {
                              "paramKey": "FEE",
                              "paramValue": 100
                            }
                          ]
                        }
                      ]
                    },
                    {
                      "acquisitionMethod": "PURCHASE and LOAN",
                      "id": 7
                    }
                  ],
                  "classifications": [
                    "ROOT/PAQUETIGOS/MENSAJES/",
                    "ROOT/PAQUETIGOS/MENSAJES/MENSAJES A TIGO/"
                  ],
                  "description": "50SMS x 1000Gs (ahorro 82%)",
                  "durationTime": 24,
                  "id": 274,
                  "name": "50sms1000gs",
                  "planTypes": [
                    "PREPAID_HS",
                    "POSTPAID_HS"
                  ],
                  "segments": [
                    "Navidad",
                    "Default",
                    "Internet Increible"
                  ],
                  "shortName": "50 SMS a Tigo"
                },
                {
                  "acquisitionMethods": [
                    {
                      "acquisitionMethod": "PURCHASE",
                      "id": 1,
                      "priceList": {
                        "currentPrice": 10000,
                        "paymentMethodId": 1,
                        "paymentMethodName": "CHARGE_ACCOUNT"
                      }
                    },
                    {
                      "acquisitionMethod": "ACTIVATION",
                      "id": 4,
                      "priceList": {
                        "currentPrice": 0,
                        "paymentMethodId": 0,
                        "paymentMethodName": "DEFAULT_PRICE"
                      }
                    }
                  ],
                  "classifications": "ROOT/PAQUETIGOS/Internet/Musica+Internet/",
                  "description": "Deezer x 7dias 10000Gs",
                  "durationTime": 168,
                  "id": 295,
                  "name": "Deezer x 7dias 10000Gs",
                  "planTypes": [
                    "PREPAID_HS",
                    "PREPAID_DC"
                  ],
                  "segments": [
                    "Default",
                    "Internet Increible"
                  ],
                  "shortName": "Deezer 200MB + 100MB Extras"
                },
                {
                  "acquisitionMethods": [
                    {
                      "acquisitionMethod": "PURCHASE",
                      "id": 1,
                      "priceList": [
                        {
                          "currentPrice": 2500,
                          "paymentMethodId": 1,
                          "paymentMethodName": "CHARGE_ACCOUNT"
                        },
                        {
                          "currentPrice": 2500,
                          "paymentMethodId": 20,
                          "paymentMethodName": "DAILY_CHARGE"
                        }
                      ]
                    },
                    {
                      "acquisitionMethod": "DEACTIVATION",
                      "id": 6
                    }
                  ],
                  "classifications": [
                    "ROOT/PAQUETIGOS/Internet/Internet Increible/",
                    "ROOT/PAQUETIGOS/Internet/Z|Internet Increible - Autocompra/",
                    "ROOT/Internet TigoShopApp/"
                  ],
                  "description": "Promo Whatsapp +65MB+25Min+65SMS EXTRAS x DIA. Activa solo una vez y disfruta todos los d�as!",
                  "durationTime": 24,
                  "id": 428,
                  "name": "65MB+25Min+65SMSX2500Gs",
                  "planTypes": [
                    "PREPAID_HS",
                    "POSTPAID_HS"
                  ],
                  "segments": [
                    "Default",
                    "Internet Increible"
                  ],
                  "shortName": "65MB+25MIN"
                }
              ]
            }

## Subscriber Products [/{country}/fulfillment/subscribers/{msisdn}/products/{productId}]
Represents the Products a specific Tigo Mobile subscriber identified by its `msisdn` has or will acquire.

+ Parameters
    
    + country: `py` (enum[string], required) - Country code of the Tigo Market
        + Members
            + `py` - Paraguay
            + `sv` - El Salvador
    + msisdn: `595981400007` (string, required) - Mobile number of tigo subscriber in international format.
    + productId: `428` (string, required) - Product `id` that we're acquiring
    
### Acquire a Product [POST]
Acquire a Product identified by `productId` for Subscriber identified by `msisdn` using Payment Method `desiredPaymentMethodId`

The following parameters **MAY** be present in the Request body with **Content-Type:** `application/x-www-form-urlencoded`:

- **desiredPaymentMethodId**: (number) same as **id** in **products[].acquisitionMethods[].priceList[].paymentMethodId** in [Products Collection].
- **externalTransactionId**: (number) a unique transaction identifier logged in your Application. for future use to correlate transactions between the Developer and Tigo

If the transaction is succesful the HTTP Response Status code is 201  
if the transaction cannot be fulfilled the HTTP Response Status code 400 and the payload will have a `error` property with the following `code` and `message`:  

|`code`|`message`|Reason|
|------|---------|------|
|`1 `|Error retreiving product list |Error Message for offer module|
|`2 `|Error user exist |Error user exist|
|`3 `|Error user not exist |Error user not exist|
|`4 `|Error profile not exist |Error profile not exist|
|`5 `|Error user and profile not exist |Error user and profile not exist|
|`6 `|Error user and profile exist |Error user and profile exist|
|`7 `|Error customer cannot purchase product |Error customer cannot purchase product|
|`8 `|Could not find transaction data for this request |Could not find transaction data for this request|
|`9 `|Product parameters for provisioning actions are not complete |Product parameters for provisioning actions are not complete|
|`10`|Error instanciating class |Error instanciating class|
|`11`|Error connecting to platfform |Error connecting to platfform|
|`12`|Unknown Error |Unknown Error|
|`13`|Error executing action in platforn |Error executing action in platforn|
|`13`|ROLLBACK_DONE : No se pueden agregar mas Paquetes |This happens when multiple data packs are purchased above the limit|
|`14`|Error executing validator |Error executing validator|
|`15`|Payment framework processing error |Payment framework processing error|
|`16`|Rollback error |Rollback error|
|`17`|Error validating REST request |Error validating REST request|
|`18`|Error while load balancing |Error while load balancing|
|`19`|Error executing payment |Error executing payment|
|`20`|Customer msysdn is a mandatory parameter |Customer msysdn is a mandatory parameter|
|`21`|ChannelID is a mandatory parameter |ChannelID is a mandatory parameter|
|`22`|referenced value is not a valid adquisition type |referenced value is not a valid adquisition type|
|`23`|referenced value is not a valid channel |referenced value is not a valid channel|
|`24`|ExternalTransactionID must be a integer value |ExternalTransactionID must be a integer value|
|`25`|Origin AgentID is a mandatory parameter |Origin AgentID is a mandatory parameter|
|`26`|Destination AgentID is a mandatory parameter |Destination AgentID is a mandatory parameter|
|`27`|Product current status is off |Product current status is off|
|`28`|Customer and product are not in the same segment |Customer and product are not in the same segment|
|`29`|Product can not be acquired using that channel |Product can not be acquired using that channel|
|`30`|The customer plan is incompatible with this product |The customer plan is incompatible with this product|
|`31`|Product can not be acquired using this method |Product can not be acquired using this method|
|`32`|Customer is not in product's white list |Customer is not in product's white list|
|`33`|Customer is in product's black list |Customer is in product's black list|
|`34`|Product validity period has expired |Product validite period has expired|
|`35`|Product is inconpatible with other previusly acquired products |Product is inconpatible with other previusly acquired products|
|`36`|External parameters for provisioning actions are not complete |External parameters for provisioning actions are not complete|
|`37`|Product parameters for payment actions are not complete |Product parameters for payment actions are not complete|
|`38`|External parameters for payment actions are not complete |External parameters for payment actions are not complete|
|`39`|Selected transaction can not be reprocessed |Selected transaction can not be reprocessed|
|`40`|Insufficient balance to make the charge |Insufficient balance to make the charge|

additionally, the `error` will contain a platform-specific `platformCode` that can be used to further identify the cause of the error.
See [https://jira.tigo.com.hn/browse/TSA-292] and [https://jira.tigo.com.hn/browse/TSA-134] for more details.

+ Request (application/x-www-form-urlencoded)
    
    + Attributes
        + desiredPaymentMethod: `1` (string, optional) - The `paymentMethodId` to be used for paying the product `id`
        + externalTransactionId: `123456789` (string, optional) - an unique transaction identifier supplied by the App
        
    + Headers
    
            Authorization: Bearer {access_token}

+ Response 201 (application/json)

    + Attributes (SuccesfulPurchase)
    
    + Body

            {
                "msisdn" : "595981400007",
                "productId" : 40,
                "responseCode" : 0,
                "responseMessage" : "Operation Finished OK",
                "platformCode" : "Producto fue activado con exito!"
            }
    
+ Response 403 (application/json)

    + Attributes (FailedPurchase)
    
    + Body

            {
                "error": {
                    "code": "13",
                    "message": "Error executing action in platforn",
                    "platformCode": "99997"
                }
            }

# Data Structures

## ProductsResponse (object, required)

+ responseCode: 0 (number, required)
+ responseMessage: "Operation Finished OK" (string, required)
+ customer (Customer, optional) - Customer balance and planType. Only available in PY.
+ products (array[Product], required) - Array of Product Objects.

## Customer (object)

+ coreBalance: 81000 (number, required) -  Main Balance amount, in local currency
+ customerSegment: "Internet Increible" (string, required) - Customer Segmentation information.
+ planType: "PREPAGO HANDSET" (string, required) -  Account Type
+ planTypeId: 1 (string, required) - Plan Type Id

## Product (object)

+ acquisitionMethods (array[acquisitionMethod], required) - Array of configured acquisition Methods for this product
+ classifications (enum, required) - Product Type and Product Category information. Expect a string with "/" separators
    + "ROOT/PAQUETIGOS/Internet/Musica+Internet/" (string)
    + (array[string])
+ description: "Deezer x dia 2500Gs" (string, required) - Product Description
+ durationTime: 24 (number, required) - Product validity in hours
+ id: 321 (number, required) -  Product Id
+ name: "Deezer x dia 2500Gs" (string, required) -  Product Name
+ planTypes: PREPAID_HS, POSTPAID_HS (array[string], optional) - Array of Plan Types eligible for this product.
+ segments: Default, Navidad, NoDataUser (array[string], optional) - Array of customer segments eligible for this product.
+ shortName: "Deezer 70MB + 30MB Extras" (string, required) - Short name for the product

## acquisitionMethod (object)
+ acquisitionMethod (enum, required) - acquisition method name
    - "PURCHASE" (string) - means The Product is available for purchase
    - "LOAN" (string) - means The product is available for lending
    - "ACTIVATION" (string) - means the product is available for free activation (no charge)
    - "DEACTIVATION" (string) - means the product can be un-subscribed or canceled
    - "PURCHASE and LOAN" (string) - means the product is available for Purchase and Lending simultaneously
+ id (enum, required)
    + 1 (number) - products for PURCHASE
    + 3 (number) - products for LOAN
    + 4 (number) - products for ACTIVATION
    + 6 (number) - products for DEACTIVATION
    + 7 (number) - products for PURCHASE and LOAN simultaneously
+ priceList (enum, optional)
    + (PriceList)
    + (array[PriceList])
    
## PriceList (object)
+ currentPrice (number, required) - Price in local currency
+ paymentMethodId (number, required) - Payment Method Id, use this in request parameter "desiredPaymentMethod"
+ paymentMethodName (enum, required) - Payment Method Name
    + "CHARGE_ACCOUNT" (string) - this is the price charged at product activation
    + "DAILY_CHARGE" (string) - this is the price charged every day, applicable to subscription products only.
    + "LoanConnector" (string) - this is the price to Loan the product, which will be paid in the next recharge (top-up).
    + "DEFAULT_PRICE" (string) - this is the default price for activating the product, usually 0, use as last resort.
+ priceParameters (array[object], optional) - Optional Price components
    + (object)
        + paramKey (enum)
            + "COST" (string) - Lending Cost
            + "FEE" (string) - Lending Fee
        + paramValue (number)

## SuccesfulPurchase (object)

+ msisdn: 595981400007 (string, required) - Subscriber's MSISDN
+ productId: 123 (number, required) - Product Id
+ responseCode: 0 (number, required) - Result Code, 0 = succesful
+ responseMessage: "Operation Finished OK" (string, required) - Result Message
+ platformCode: "Producto fue activado con exito!" (string, optional) - Platform-specific result code.

## FailedPurchase (object)

+ error (object)
    + code (string, required) - Result Code. See table.
    + message (string, required) - Result Message describing why the transaction failed
    + platformCode (string, optional) - Platform-specific result code.
