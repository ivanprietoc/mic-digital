FORMAT: 1A

# Tigo Mobile Co Payment Gateway
El servicio de pasarela de pagos es una plataforma que permite realizar transacciones de pagos con tarjeta débito y crédito.

# Pagos

Notas relacionadas a los resursos del **Payment Gateway API**

El id de transaccion tiene que ser un valor que debe autoincrementarse con cada llamada al servicio.

## Obtener los métodos de pago [/payments/methods?processId=N&plataformId=X&userTransaction=X&transactionId=N]
### Lista de todos los metodos de pagos disponibles [GET]
+ Response 200 (application/json)

        {
            "getPaymentMethodsResponse": {
                "generalResponse": {
                    "generalResponse": {
                        "code": 100,
                        "description": "Transacción efectuada correctamente."
                    }
                },
                "paymentMethods": [
                    {
                        "paymentMethod": {
                            "id": 253,
                            "description": "DINERS",
                            "country": "CO"
                        }
                    },
                    {
                        "paymentMethod": {
                            "id": 251,
                            "description": "MASTERCARD",
                            "country": "CO"
                        }
                    },
                    {
                        "paymentMethod": {
                            "id": 12,
                            "description": "AMEX",
                            "country": "CO"
                        }
                    },
                    {
                        "paymentMethod": {
                            "id": 27,
                            "description": "CASH_ON_DELIVERY",
                            "country": "CO"
                        }
                    },
                    {
                        "paymentMethod": {
                            "id": 35,
                            "description": "BALOTO",
                            "country": "CO"
                        }
                    },
                    {
                        "paymentMethod": {
                            "id": 250,
                            "description": "VISA",
                            "country": "CO"
                        }
                    },
                    {
                        "paymentMethod": {
                            "id": 11,
                            "description": "MASTERCARD",
                            "country": "CO"
                        }
                    },
                    {
                        "paymentMethod": {
                            "id": 37,
                            "description": "EFECTY",
                            "country": "CO"
                        }
                    },
                    {
                        "paymentMethod": {
                            "id": 26,
                            "description": "ACH_DEBIT",
                            "country": "CO"
                        }
                    },
                    {
                        "paymentMethod": {
                            "id": 254,
                            "description": "PSE",
                            "country": "CO"
                        }
                    }
                ]
            }
        }

## Obtener entidades bancarias [/payments/banks?processId=N&plataformId=X&userTransaction=X&transactionId=N]
### Listado de todas las entidades bancarias [GET]
+ Response 200 (application/json)

        {
            "paymentResponse": {
                "generalResponse": {
                    "generalResponse": {
                        "code": 100,
                        "description": "Transacción efectuada correctamente."
                    }
                },
                "payment": {
                    "orderId": 6746870,
                    "platformName": "Pruebas",
                    "paymentNetworkResponseCode": "BANK_UNREACHABLE",
                    "state": "DECLINED",
                    "submit_dateTime": "2015-03-19T14:43:22.124-05:00",
                    "transactionId": 520,
                    "payuTransactionId": "ffda018d-6753-49b3-911f-38a9442e2210",
                    "payuData": {
                        "currency": "COP",
                        "description": "Pesos colombianos",
                        "language": "es",
                        "referenceCode": "SO_123",
                        "value": 120,
                        "taxValue": 1,
                        "taxReturnValue": 1
                    },
                    "buyerData": {
                        "city": "Bogota",
                        "contactPhome": 1234567890,
                        "country": "CO",
                        "email": "email@domain.com",
                        "name": "John Smith",
                        "street": "Some street 123",
                        "documentType": {
                            "type": "CC",
                            "number": 12345678
                        }
                    },
                    "payerData": {
                        "city": "Bogota",
                        "contactPhome": 1234567890,
                        "country": "CO",
                        "email": "email@domain.com",
                        "name": "John Smith",
                        "street": "Some street 123",
                        "documentType": {
                            "type": "CC",
                            "number": 12345678
                        },
                        "personType": "NATURAL"
                    },
                    "deviceData": {
                        "cookie": "no-cookie",
                        "deviceSessionId": {},
                        "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_2) AppleWebKit/537.36 (KHTML,like Gecko) Chrome/41.0.2272.89 Safari/537.36"
                    }
                }
            }
        }

## Pagos por referencia [/payments/reference?processId=N&plataformId=X&userTransaction=X&transactionId=N&referenceId=&limit=&offset=]
### Obtener pagos por referencia [GET]

+ Parameter
    + referenceId
    + limit
    + offset

+ Response 200 (application/json)

        {
            "getPaymentsByReferenceResponse": {
                "generalResponse": {
                    "generalResponse": {
                        "code": 100,
                        "description": "Transacción efectuada correctamente."
                    }
                },
                "Payments": [
                    {
                        "payment": {
                            "orderId": 6747125,
                            "platformName": "Pruebas",
                            "paymentResponseCode": "BANK_UNREACHABLE",
                            "state": "DECLINED",
                            "submit_dateTime": "2015-03-19T15:27:35.572-05:00",
                            "transactionId": 526,
                            "buyerData": {
                                "city": "Bogota",
                                "contactPhone": 1234567890,
                                "country": "CO",
                                "email": "email@domain.com",
                                "name": "John Smith",
                                "street": "Some street 123",
                                "documentType": {
                                    "number": 12345678
                                }
                            },
                            "payerData": {
                                "city": "Bogota",
                                "contactPhone": 1234567890,
                                "country": "CO",
                                "email": "email@domain.com",
                                "name": "John Smith",
                                "street": "Some street 123",
                                "documentType": {
                                    "type": "CC",
                                    "number": 12345678
                                },
                                "personType": "NATURAL"
                            },
                            "deviceData": {
                                "cookie": "no-cookie",
                                "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_2) AppleWebKit/537.36 (KHTML,like Gecko) Chrome/41.0.2272.89 Safari/537.36"
                            }
                        }
                    },
                    {
                        "payment": {
                            "platformName": "Pruebas",
                            "paymentResponseCode": "Error plataforma de pagos: Parametro [cookie] es requerido",
                            "state": "ERROR",
                            "submit_dateTime": "2015-03-19T14:22:56.393-05:00",
                            "transactionId": 515,
                            "buyerData": {
                                "city": "Bogota",
                                "contactPhone": 1234567890,
                                "country": "CO",
                                "email": "email@domain.com",
                                "name": "John Smith",
                                "street": "Some street 123",
                                "documentType": {
                                    "number": 12345678
                                }
                            },
                            "payerData": {
                                "city": "Bogota",
                                "contactPhone": 1234567890,
                                "country": "CO",
                                "email": "email@domain.com",
                                "name": "John Smith",
                                "street": "Some street 123",
                                "documentType": {
                                    "type": "CC",
                                    "number": 12345678
                                }
                            },
                            "deviceData": {}
                        }
                    }
                ]
            }
        }

## Pagos por id de transacción [/payments/transaction?processId=N&plataformId=X&userTransaction=X&transactionId=N]
### Obtener pagos por id de transacción [GET]
+ Response 200 (application/json)

        {
            "getPaymentByTransactionIdResponse": {
                "generalResponse": {
                    "generalResponse": {
                        "code": 100,
                        "description": "Transacción efectuada correctamente."
                    }
                },
                "payment": {
                    "orderId": 6746980,
                    "platformName": "Pruebas",
                    "paymentResponseCode": "ENTITY_DECLINED",
                    "state": "DECLINED",
                    "submit_dateTime": "2015-03-19T14:56:45.727-05:00",
                    "payuTransactionId": 524,
                    "maskedCreditCardNumber": "3797******31077",
                    "payuData": {
                        "currency": "COP",
                        "description": "Pesos colombianos",
                        "language": "es",
                        "referenceCode": "SO_123",
                        "value": 120,
                        "taxValue": {
                            "nil": "true"
                        },
                        "taxReturnValue": {
                            "nil": "true"
                        }
                    },
                    "buyerData": {
                        "city": "Bogota",
                        "contactPhone": 1234567890,
                        "country": "CO",
                        "email": "email@domain.com",
                        "name": "John Smith",
                        "street": "Some street 123",
                        "documentType": {
                            "number": 12345678
                        }
                    },
                    "payerData": {
                        "city": "Bogota",
                        "contactPhone": 1234567890,
                        "country": "CO",
                        "email": "email@domain.com",
                        "name": "John Smith",
                        "street": "Some street 123",
                        "documentType": {
                            "type": "CC",
                            "number": 12345678
                        }
                    },
                    "deviceData": {}
                }
            }
        }

## Obtener los pagos por documento de identidad [/payments/payer/document?processId=N&plataformId=X&userTransaction=X&transactionId=N&docType=&docNumber=&limit=&offset=]
### Get by payer id num [GET]

+ Parameters
    + docType
    + docNumber
    + limit
    + offset

+ Response 200 (application/json)

            {
                "getPaymentsByPayerDocumentResponse": {
                    "generalResponse": {
                        "generalResponse": {
                            "code": 100,
                            "description": "Transacción efectuada correctamente."
                        }
                    },
                    "Payments": {
                        "payment": {
                            "platformName": "Pruebas",
                            "state": "ERROR",
                            "submit_dateTime": "2015-03-19T14:22:56.393-05:00",
                            "transactionId": 515,
                            "buyerData": {
                                "city": "Bogota",
                                "contactPhome": 1234567890,
                                "country": "CO",
                                "email": "email@domain.com",
                                "name": "John Smith",
                                "street": "Some street 123",
                                "documentType": {
                                    "number": 12345678
                                }
                            },
                            "payerData": {
                                "city": "Bogota",
                                "contactPhome": 1234567890,
                                "country": "CO",
                                "email": "email@domain.com",
                                "name": "John Smith",
                                "street": "Some street 123",
                                "documentType": {
                                    "type": "CC",
                                    "number": 12345678
                                }
                            },
                            "deviceData": {}
                        }
                    }
                }
            }

## Credit card payments [/payments/creditcard?processId=N&plataformId=X&userTransaction=X&transactionId=N]
### Create a payment via credit card [POST]
+ Request (application/json)

           {
                "payment": {
                    "buyer": {
                        "city": "Bogota",
                        "name": "John Smith",
                        "country": "CO",
                        "phone": "1234567890",
                        "street": "Some street 123",
                        "postalCode": "1234",
                        "state": "BO",
                        "document": {
                            "type": "CC",
                            "number": 12345678
                        },
                        "email": "email@domain.com"
                    },
                    "payU": {
                        "currency": "COP",
                        "value": 10,
                        "taxValue": 1,
                        "taxReturnValue": 1,
                        "description": "Pesos colombianos",
                        "language": "es",
                        "referenceCode": "SO_123"
                    },
                    "payer": {
                        "city": "Bogota",
                        "name": "John Smith",
                        "country": "CO",
                        "phone": "1234567890",
                        "street": "Some street 123",
                        "document": {
                          "type": "CC",
                          "number": 12345678
                        },
                        "email": "email@domain.com"
                    },
                    "creditcard": {
                        "country": "CO",
                        "installmentsNumber": 1,
                        "number": "379711148531077",
                        "securityCode": "1983",
                        "paymentMethod": "AMEX",
                        "expirationDate": "2019/09"
                    }
                }
            }

+ Response 200 (application/json)

        {
            "paymentResponse": {
                "generalResponse": {
                    "generalResponse": {
                        "code": 100,
                        "description": "Transacción efectuada correctamente."
                    }
                },
                "payment": {
                    "orderId": 6746980,
                    "platformName": "Pruebas",
                    "paymentNetworkResponseCode": "ENTITY_DECLINED",
                    "state": "DECLINED",
                    "submit_dateTime": "2015-03-19T14:56:48.899-05:00",
                    "transactionId": 524,
                    "payuTransactionId": "83b87e6b-4295-4c1b-9224-e93e4139ec62",
                    "maskedCreditCardNumber": "3797******31077",
                    "payuData": {
                        "currency": "COP",
                        "description": "Pesos colombianos",
                        "language": "es",
                        "referenceCode": "SO_123",
                        "value": 120,
                        "taxValue": 1,
                        "taxReturnValue": 1
                    },
                    "buyerData": {
                        "city": "Bogota",
                        "contactPhome": 1234567890,
                        "country": "CO",
                        "email": "email@domain.com",
                        "name": "John Smith",
                        "street": "Some street 123",
                        "documentType": {
                            "type": "CC",
                            "number": 12345678
                        }
                    },
                    "payerData": {
                        "city": "Bogota",
                        "contactPhome": 1234567890,
                        "country": "CO",
                        "email": "email@domain.com",
                        "name": "John Smith",
                        "street": "Some street 123",
                        "documentType": {
                            "type": "CC",
                            "number": 12345678
                        }
                    },
                    "deviceData": {
                        "cookie": {},
                        "deviceSessionId": {},
                        "userAgent": {}
                    }
                }
            }
        }

## Bank transfer payments [/payments/bank-transfer?processId=N&plataformId=X&userTransaction=X&transactionId=N]
### Create a payment via bank transfer [POST]
+ Request (application/json)

            {
              "payment": {
                    "financialInstitutionCode": "1040",
                    "country": "CO",
                    "buyer": {
                        "city": "Bogota",
                        "name": "John Smith",
                        "country": "CO",
                        "phone": "1234567890",
                        "street": "Some street 123",
                        "postalCode": "1234",
                        "state": "BO",
                        "document": {
                            "type": "CC",
                            "number": 12345678
                        },
                        "email": "email@domain.com"
                  },
                    "payU": {
                        "currency": "COP",
                        "value": 10,
                        "taxValue": 1,
                        "taxReturnValue": 1,
                        "description": "Pesos colombianos",
                        "language": "es",
                        "referenceCode": "SO_123"
                    },
                    "payer": {
                        "city": "Bogota",
                        "name": "John Smith",
                        "country": "CO",
                        "phone": "1234567890",
                        "street": "Some street 123",
                        "street2": "*",
                        "postalCode": "1234",
                        "personType": 1,
                        "state": "BO",
                        "document": {
                            "type": "CC",
                            "number": 12345678
                        },
                        "email": "email@domain.com"
                    }
               }
           }

+ Response 200 (application/json)

            {
                "paymentResponse": {
                    "generalResponse": {
                        "generalResponse": {
                            "code": 100,
                            "description": "Transacción efectuada correctamente."
                        }
                    },
                    "payment": {
                        "orderId": 6747125,
                        "platformName": "Pruebas",
                        "paymentNetworkResponseCode": "BANK_UNREACHABLE",
                        "state": "DECLINED",
                        "submit_dateTime": "2015-03-19T15:27:41.295-05:00",
                        "transactionId": 526,
                        "payuTransactionId": "1e541259-5d94-40f8-8065-f8ff9456e6cd",
                        "payuData": {
                            "currency": "COP",
                            "description": "Pesos colombianos",
                            "language": "es",
                            "referenceCode": "SO_123",
                            "value": 120,
                            "taxValue": 1,
                            "taxReturnValue": 1
                        },
                        "buyerData": {
                            "city": "Bogota",
                            "contactPhome": 1234567890,
                            "country": "CO",
                            "email": "email@domain.com",
                            "name": "John Smith",
                            "street": "Some street 123",
                            "documentType": {
                                "type": "CC",
                                "number": 12345678
                            }
                        },
                        "payerData": {
                            "city": "Bogota",
                            "contactPhome": 1234567890,
                            "country": "CO",
                            "email": "email@domain.com",
                            "name": "John Smith",
                            "street": "Some street 123",
                            "documentType": {
                                "type": "CC",
                                "number": 12345678
                            },
                            "personType": "NATURAL"
                        },
                        "deviceData": {
                            "cookie": "no-cookie",
                            "deviceSessionId": {},
                            "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_2) AppleWebKit/537.36 (KHTML,like Gecko) Chrome/41.0.2272.89 Safari/537.36"
                        }
                    }
                }
            }

## Cash payments [/payments/cash?processId=N&plataformId=X&userTransaction=X&transactionId=N]
### Create a payment via cash [POST]
+ Request (application/json)

            {
                "payment": {
                    "cash": {
                        "country": "CO",
                        "paymentMethod": "EFECTY",
                        "expirationDate": "2015-03-19 17:20:00"
                    },
                    "buyer": {
                        "city": "Bogota",
                        "name": "John Smith",
                        "country": "CO",
                        "phone": "1234567890",
                        "street": "Some street 123",
                        "postalCode": "1234",
                        "state": "BO",
                        "document": {
                            "type": "CC",
                            "number": 12345678
                        },
                        "email": "email@domain.com",
                        "personType": "NATURAL"
                    },
                    "payU": {
                        "currency": "COP",
                        "value": 150000,
                        "taxValue": 1,
                        "taxReturnValue": 1,
                        "description": "Compra 1",
                        "language": "es",
                        "referenceCode": "SO_123"
                    },
                    "payer": {
                        "city": "Bogota",
                        "name": "John Smith",
                        "country": "CO",
                        "phone": "1234567890",
                        "street": "Some street 123",
                        "street2": "*",
                        "postalCode": "1234",
                        "personType": "NATURAL",
                        "state": "BO",
                        "document": {
                          "type": "CC",
                          "number": 12345678
                        },
                        "email": "email@domain.com"
                    }
                }
            }

+ Response 200 (application/json)

            {
                "paymentResponse": {
                    "generalResponse": {
                        "generalResponse": {
                            "code": 100,
                            "description": "Transacción efectuada correctamente."
                        }
                    },
                    "payment": {
                        "orderId": 6747205,
                        "platformName": "Pruebas",
                        "paymentNetworkResponseCode": "PENDING_TRANSACTION_CONFIRMATION",
                        "pendingReason": "AWAITING_NOTIFICATION",
                        "state": "PENDING",
                        "submit_dateTime": "2015-03-19T15:46:12.661-05:00",
                        "transactionId": 533,
                        "payuTransactionId": "a43a1497-1744-4e5b-8e65-7ffa872cbc88",
                        "bankURL": "https://stg.gateway.payulatam.com/ppp-web-gateway/voucher.zul?vid=6747205Ya43a149717444e5Ye3363fee49262b2",
                        "payuData": {
                            "currency": "COP",
                            "description": "Compra 1",
                            "language": "es",
                            "referenceCode": "SO_123",
                            "value": 150000,
                            "taxValue": 1,
                            "taxReturnValue": 1
                        },
                        "buyerData": {
                            "city": "Bogota",
                            "contactPhome": 1234567890,
                            "country": "CO",
                            "email": "email@domain.com",
                            "name": "John Smith",
                            "street": "Some street 123",
                            "documentType": {
                                "type": "CC",
                                "number": 12345678
                            }
                        },
                        "payerData": {
                            "city": "Bogota",
                            "contactPhome": 1234567890,
                            "country": "CO",
                            "email": "email@domain.com",
                            "name": "John Smith",
                            "street": "Some street 123",
                            "documentType": {
                                "type": "CC",
                                "number": 12345678
                            },
                            "personType": "NATURAL"
                        },
                        "deviceData": {
                            "cookie": {},
                            "deviceSessionId": {},
                            "userAgent": {}
                        }
                    }
                }
            }

## Update payment status by transaction id [/payments/transaction/status?processId=N&plataformId=X&userTransaction=X&transactionId=N]
### Update payment status via transaction id [PUT]
+ Request (application/json)

        {
            "state": "PENDING"
        }

+ Response 200 (application/json)

        {
            "updatePaymentStatusByTransactionIdResponse": {
                "generalResponse": {},
                "payment": {
                    "orderId": 6747205,
                    "platformName": "Pruebas",
                    "paymentResponseCode": "APPROVED",
                    "state": "APPROVED",
                    "submit_dateTime": "2015-03-19T15:46:09.968-05:00",
                    "payuTransactionId": 533,
                    "bankURL": "https://stg.gateway.payulatam.com/ppp-web-gateway/voucher.zul?vid=6747205Ya43a149717444e5Ye3363fee49262b2",
                    "payuData": {
                        "currency": "COP",
                        "description": "Compra 1",
                        "language": "es",
                        "referenceCode": "SO_123",
                        "value": 150000,
                        "taxValue": {
                            "nil": "true"
                        },
                        "taxReturnValue": {
                            "nil": "true"
                        }
                    },
                    "buyerData": {
                        "city": "Bogota",
                        "contactPhone": 1234567890,
                        "country": "CO",
                        "email": "email@domain.com",
                        "name": "John Smith",
                        "street": "Some street 123",
                        "documentType": {
                            "number": 12345678
                        }
                    },
                    "payerData": {
                        "city": "Bogota",
                        "contactPhone": 1234567890,
                        "country": "CO",
                        "email": "email@domain.com",
                        "name": "John Smith",
                        "street": "Some street 123",
                        "documentType": {
                            "type": "CC",
                            "number": 12345678
                        },
                        "personType": "NATURAL"
                    },
                    "deviceData": {}
                }
            }
        }

