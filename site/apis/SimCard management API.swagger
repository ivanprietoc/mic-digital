swagger: '2.0'
info:
  description: SimCard management API
  version: 2.0.0
  title: SimCard management API
  contact:
    name: Ivan Florentin
    email: ivan.florentin@edge.com.py
    url: 'https://edge.com.py'
host: test.api.tigo.com
basePath: /v2/tigo/b2b/hn/crm
tags:
  - name: ticket
    description: SimCard Management
    externalDocs:
      description: TC-368
      url: 'https://jira.tigo.com.hn/browse/TC-368'
schemes:
  - https
consumes:
  - application/json
produces:
  - application/json
securityDefinitions:
  Bearer:
    type: oauth2
    authorizationUrl: >-
      https://test.api.tigo.com/oauth/client_credential/accesstoken?grant_type=client_credentials
    flow: implicit
    scopes:
      'read:contracts': read contracts
paths:
  '/clients/rtn/{rtn}/simcards':
    get:
      tags:
        - clients
        - SimCard
      description: Get client info
      summary: Get information about a line and a symCard associated to it
      operationId: getSimCardInfo
      consumes:
        - application/json
      produces:
        - application/json
      parameters:
        - name: rtn
          in: path
          type: number
          description: Client RTN
          required: true
        - name: Authorization
          in: header
          required: true
          type: string
          description: Access token
      responses:
        '200':
          description: Successful operation
          schema:
            $ref: '#/definitions/SimCardType'
        '404':
          description: Line not found
          schema:
            $ref: '#/definitions/errorBody'
  '/clients/{idType}/{clientId}/simcards':
    put:
      tags:
        - SimCard
      summary: Update line with a new Simvard
      description: Update a simCard
      operationId: updateSimCard
      parameters:
        - name: idType
          type: string
          in: path
          required: true
          description: Client rtn id
        - name: clientId
          type: string
          in: path
          description: SimCard id
          required: true
        - in: body
          name: details
          description: SimCard change details
          required: true
          schema:
            $ref: '#/definitions/SimCardChange'
      security:
        - Bearer: []
      responses:
        '200':
          description: Operation successful
        '404':
          description: Not Found.
          schema:
            $ref: '#/definitions/errorBody'
        default:
          description: Unhandled resource
          schema:
            $ref: '#/definitions/errorBody'
definitions:
  ClientType:
    type: object
    properties:
      id:
        type: string
        description: Client Id
      idType:
        type: string
        description: Identifier type
  SimCardChange:
    description: SimCard change request message
    type: object
    properties:
      clientId:
        $ref: '#/definitions/ClientType'
        description: Client id
      accountIntegration:
        type: string
        description: Integration Id provided by CRM
      newSim:
        $ref: '#/definitions/SimCardType'
        description: The new simCard details
      oldSim:
        $ref: '#/definitions/SimCardType'
        description: The simCard to be changed
      transactionUser:
        type: string
        description: Employee login name
      vendor:
        $ref: '#/definitions/ClientType'
        description: Seller information
      additionalParameters:
        type: array
        description: aditional parameters
  SimCardType:
    type: object
    properties:
      imsi:
        type: string
        description: Platform SimCard id number
      iccid:
        type: string
        description: SimCard serial number
      pin1:
        type: string
        description: PIN1 Security code
      pin2:
        type: string
        description: PIN2 Security code
      puk1:
        type: string
        description: Pin unlock key for pin1
      puk2:
        type: string
        description: Pin unlock key for pin2
      simCardType:
        type: string
        description: 'SimCard type (microSim, nanoSim, etc)'
      status:
        type: string
        description: SimCard Status
      simCardPrice:
        type: number
        format: double
        minimum: 0
        description: SimCard Price
  errorBody:
    properties:
      error:
        required:
          - statusCode
          - message
        type: object
        properties:
          statusCode:
            type: string
            description: Http Status Code
            example: '401'
          code:
            type: string
            description: Same as the http status code
            example: '401'
          message:
            type: string
            description: General message for the error
            example: Not Authorized
          developerMessage:
            type: string
            description: More precise info about the error
            example: Access token was not provided or is invalid
