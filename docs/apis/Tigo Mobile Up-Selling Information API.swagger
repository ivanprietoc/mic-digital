FORMAT: 1A
HOST: https://test.api.tigo.com/v1/tigo/mobile/upselling

# Tigo Mobile Up-Selling Information API
Provides status information of a Tigo Mobile Customer about its Mobile services, Balances and Data Quota  

# Authentication
1. Each Client application MUST register and request its client credentials from Tigo/Millicom.  
2. With your client credentials, an **access_token** needs to be obtained. 
   Please see http://docs.tigooauth20apis.apiary.io on how to obtain access tokens
3. In each request, you need to present the **access_token** in the HTTP **Authorization** header like this:  
   `Authorization: Bearer <access_token>`

# Caching
Quota API uses a caching mechanism to avoid overloading the backend systems which have a nominal 
maximum capacity of 50 request/second. the Caching logic is as follows:

* If **availableQuota** is `0`, then NO caching is done.
* If **availableQuota** is greater than `0` then
    * Derive how many seconds **availableQuota** assuming the user is consuming at a constant 
      rate of 512Kbps or 0.064 Mbytes/sec
    * Derive how many seconds left until **packExpirationDate** or **nextResetDate**
    * Choose the lowest from the 2 times above and populate a cache entry with that Time to live in seconds.

If the client wishes to bypass the caching mechanism (thus clearing and refreshing the cache entry), 
It needs to add the HTTP request Header **bypass-cache** with any value.

# Market availability

This API is avaialable in the following markets:
* Tigo Paraguay
* Tigo Guatemala

# Group Subscriber Balance
# Subscriber Balance [/subscribers/{msisdn}/balance]
Tigo Subscriber's current Main Balance (in local currency) and Type of Customer

**typeClient** values are country specific, as follows:

**Tigo Paraguay:**
- `PREPAGO`
- `POSPAGO`

**Tigo Guatemala:**
- `FACTURA FIJA`
- `FREE`
- `STAFF DE COMCEL`
- `CREDITO`
- `KIT`
- `PREPAGO`
- `HOME`

+ Attributes (object)
  + balance (number, required) - Amount left in Balance (credit limit) in local currency
  + typeClient (enum, required) - Type of Billing Account
  + responseMessage: Operacion exitosa (string) - Expect `Operacion exitosa`
  + transactionCode: 100 (number) - Expect `100`

+ Parameters

    + msisdn (required, string, `595982604505`) ... Mobile number of Tigo Subscriber in international format

## Query Subscriber's Balance [GET]
+ Request

    + Headers
    
            Authorization: Bearer {access_token}

+ Response 200 (application/json)

    + Body
    
            {
            "balance": 2.34,
            "responseMessage": "Operacion exitosa",
            "transactionCode": 100,
            "typeClient": "PREPAGO"
            }
    

# Group Subscriber Mobile Internet Quota
# Subscriber Quota [/subscribers/{msisdn}/quota]
Tigo Subscriber's current Data Plan or Data Package information

The API response returns the following attributes in JSON format:

- **accountType**:  (string) Type of Account.  
Examples:
    - `PRE` Prepaid subscriber
    - `POS` Postpaid subscriber with a Data Plan
    - `POS_NO_PLAN` Postpaid subscriber with NO Data plan
- **clientType**: (string) Type of Customer. A more verbose description of **accountType**.  
Examples:
    - `POSPAGO NO PLAN`
    - `POSPAGO DEFAULT`
    - `PREPAGO DEFAULT`
- **blister**: (string) contains `true` or `false` if this is a Pre-packaged Device sold at a retailer.
- **postPaidPlan**: (JSON object, optional) *Not Always present* information about Subscriber's current 
  Postpaid (monthly billed) Data plan, if any.
- **currentPack**: (JSON object, optional) *Not Always present* information about Subscriber's current 
  Data Package, if any.
- **currentSubscription**: (JSON object, optional) *Not Always present* information about Subscriber's 
  current Data Subscription, if any.
- **currentPass** _new_\*: (JSON object, optional) *Not Always present* information about Subscriber's 
  current Pass that can be purchased on top of Data Plans and Data packages and modify the normal behavior of the Offer.  
Examples: `Unlimited WhatsApp`
- **queuedPacks** _new_\*: (Array of JSON objects, optional) *Not Always present* information about 
  Subscriber's queued Data Packages which are purchased but not yet beign consumed. Maybe more than one.
- **additionalResults** _changed_\*: (JSON object, optional) *Not Always present* additional information 
  attributes, see below.
- **availableQuota** _deprecated in Paraguay_\*: (string) Total Amount of Mbytes or Gbytes left to access 
  Mobile internet services.  
  Examples:  `10,4 MB` `1,3 GB`
  > **IMPORTANT**: In tigo Paraguay, please see **postpaidPlan**, **currentPack**, **currentSubscription**, 
  > **currentPass** and **queuedPacks** to know how many Mbytes/Gbytes are available to the customer in each product.

The **postPaidPlan** JSON object is only present when the User has a Postpaid Data plan active, and has the following attributes:

- **availableQuota**: (string) Amount of Mbytes or Gbytes left in the Data Plan for the current Billing Cycle. This will be reset at **nextResetDate**.  
  Examples:  `10,4 MB` `1,3 GB` *(Note that , -comma- is used as decimal delimiter)*
- **description**: (string) Name of the Postpaid Data Plan.  
  Example: `Navegacion 70mil Gs.`,
- **dpiCode**: (string) Identifier of Plan in the DPI/PCRF system.  
  Example: `HS_VA_650_70MIL`,
- **nextResetDate**: (string) Quota Reset Time (when it is going to refill).  
  Example: `2013-12-21-03:00`,
- **quota**: (string) Granted Quota in MBytes or Gbytes:  
  Example: `1,5 GB` *(Note that , -comma- is used as decimal delimiter)*
- ~~**downLink**~~ _deprecated_\*: Downlink Allowed Speed.  
  Example: `2 Mbps`,
- ~~**dpiQuotaName**~~ _deprecated_\*: Identifier of Quota name in DPI/PCRF system.  
  Example: `1536 MB Quota HSPostpaid`,
- ~~**lowRate**~~ _deprecated_\*: Guaranteed Speed.  
  Example: `0 Mbps`,
- ~~**trafficType**~~ _deprecated_\*: Traffic Type.  
  Example: `L`,
- ~~**uplink**~~ _deprecated_\*: UpLink allowed speed.  
  Example: `2 Mbps`

The **currentPack**, **currentSubscription** and **currentPass** JSON object are only present when the User has an active Data Pack (maybe on top of the Postpaid Data plan). they have the following attributes:

- **description**: (string) Name of the Data package.  
  Example: `10 MB vigencia 24hs.`,
- **quota**: (string) how many Mbytes or Gbytes are granted by this Data Package (not to confuse with **availableQuota**).  
  Example: `10 MB`
- **dpiCode**: Identifier of Plan in the DPI/PCRF system.  
  Example: `HSPOS_CM_1MIL`,
- **expirationDate** _new_: (ISO date) Local date-time When the Data pack is going to expire.  
  Example: `2014-08-09T09:09:45.000-04:00`
- **availableQuota** _new_: (string) Amount of Mbytes or Gbytes left in the Data Pack. This will be expired at **expirationDate**.  
  Examples:  `10,4 MB` `1,3 GB` *(Note that , -comma- is used as decimal delimiter)*
- **purchaseDate** _new_: (ISO date) Local date-time when the Data pack was purchased.  
  Example: `2014-08-07T11:12:30.997-04:00`
- **mundo2** _new_: (string) `true` or `false` if this Data Pack is elegible to "Mundo2" subscribers.
- **priority** _new_: (integer) Consumption priority used to determine in which order Data packs are consumed.
- **duration** _new_: (integer) Validity of the Data Pack or Data pass in seconds.
- **dpiQuotaName**: (string) Identifier of Quota name in DPI/PCRF system.  
  Example: `10 MB Quota TopUp HSPostpaid`.

The **queuedPacks** is a JSON Object or an Array of JSON objects, each represents a Data Package that has been purchased by the Tigo Customer but not yet active for consumption. Once the **currentPack** is exhausted, the next **queuedPack** becomes the **currentPack** based on the highest **priority**. Each **queuedPacks** has the following properties:

- **description**: (string) Descriptive name of the Data Package.  
  Example: `Paquetigo Promocional 20 MB`
- **quota**: (string) Amount of MBytes or Gbytes included with the pack.  
  Example: `20 MB`
- **dpiCode**: (string) Name of the Data Package as configured in the PCRF/DPI.  
  Example: `PAQUETIGO 20MB 24HORAS`
- **expirationDate** _new_: (ISO date, optional) *Not Always present* Local date-time When the Data pack is going to expire.  
  Example: `2014-08-09T09:09:45.000-04:00`
- **availableQuota**: (string) remaining amount of Mbytes or GBytes in Data package.  
  Example: `20 MB`
- **purchaseDate**: (ISO date string) local date-time when the Data Pack was purchased.  
  Example: `2014-07-11T08:33:00.000-04:00`
- **duration**: (Integer) duration in seconds of the Data package validity.  
  Example: `86400`
- **mundo2**: (String) true/false flag to indicate if this Data pack is part of the "Mundo2" subscription.  
  Example: `true`
- **priority**: (Integer) Data Pack consuption priority. Highest priority are first to be consumed.  
  Example: `10`


The **additionalResults** JSON object may have an Array of **parameter**, however if there is only 1 **parameter** is a single JSON object.

Each **parameter** have the following attributes:

- **parameterName**: (string) for possible values see below
- **parameterType**: Not used
- **parameterValue**: (string) for possible values see below

~~Useful information in **additionalResults**~~ _deprecated_\*:

<table>
    <tr>
        <th>Scenario</th>
        <th>parameterName</th>
        <th>parameterValue</th>
    </tr>
    <tr>
        <td>If <em>currentPack</em> is present</td>
        <td><em>packExpirationDate</em></td>
        <td>will contain Date & time when the Package will expire in format "dd/mm/yyyy HH:SS" Example: <em>27/12/2013 21:57</em></td>
    </tr>
    <tr>
        <td>If Subscriber has Postpaid Billing</td>
        <td><em>handsetPostPaidNoPlan</em></td>
        <td><em>true</em> if This subscriber has NO data Plan, otherwise <em>false</em></td>
    </tr>
</table>

+ Parameters

    + msisdn (required, string, `595982604505`) ... Mobile number of Tigo Subscriber in international format
    
+ Model (application/json)
    
    JSON representation of the Tigo Subscriber's Quota

    + Body

            {
                "accountType": "POS", 
                "blister": false, 
                "clientType": "POSPAGO DEFAULT", 
                "postPaidPlan": {
                    "availableQuota": "16 GB", 
                    "description": "Plan de Datos 16 GB", 
                    "dpiCode": "PLAN_16384MB_POS_FW", 
                    "quota": "16 GB"
                }
                "currentPack": {
                    "description": "Paquetigo Promocional 100 MB",
                    "quota": "100 MB",
                    "dpiCode": "PAQUETIGO 100MB 24HORAS",
                    "expirationDate": "2014-08-09T09:09:45.000-04:00",
                    "availableQuota": "18,75 MB",
                    "purchaseDate": "2014-08-07T11:12:30.997-04:00",
                    "mundo2": "true",
                    "priority": 10
                },
                "queuedPacks": [
                    {
                        "availableQuota": "100 MB", 
                        "description": "Paquetigo Promocional 100 MB", 
                        "dpiCode": "PAQUETIGO 100MB 24HORAS", 
                        "mundo2": "true", 
                        "priority": 10, 
                        "purchaseDate": "2014-08-07T11:12:30.997-04:00", 
                        "quota": "100 MB"
                    }, 
                    {
                        "availableQuota": "500 MB", 
                        "description": "Paquetigo Promocional 500 MB", 
                        "dpiCode": "PAQUETIGO 500MB 24HORAS", 
                        "mundo2": "false", 
                        "priority": 9, 
                        "purchaseDate": "2014-08-07T11:13:29.028-04:00", 
                        "quota": "500 MB"
                    }, 
                    {
                        "availableQuota": "300 MB", 
                        "description": "Paquetigo Promocional 300 MB", 
                        "dpiCode": "PAQUETIGO 300MB 24HORAS", 
                        "duration": 86400, 
                        "mundo2": "false", 
                        "priority": 8, 
                        "purchaseDate": "2014-08-08T14:19:18.562-04:00", 
                        "quota": "300 MB"
                    }
                ]
            }

## Query Subscriber's Quota [GET]
+ Request

    + Headers
    
            apikey: cAGOBtZREWM2SRXmP3JQZ8uhBDJQzA7Y

+ Response 200

    [Subscriber Quota][]

# Group Subscriber Balance Collection
# Subscriber Balances Collection [/subscribers/{msisdn}/balances]
Tigo Subscriber's list of Balances and their current value.  
Returns a JSON object with attribute **balances** which contains an array of **balance** JSON objects.  
Each **balance** JSON Object has the following attributes:

- **wallet**: (string) Name of the wallet or balance. Example: `CORE BALANCE`
- **expirationDate**: (date time in ISO format) Date and Time when the Balance will be reset to 0 (zero). Example: `2017-01-14T20:59:59`
- **balanceAmount**: (float) current available Amount of **unit**s in the balance. Example: `6.8585`
- **description**: (string) Description of the balance/wallet use. Example: `Saldo Principal`
- **unit**: (string) Units in which **balanceAmount** is represented (may be a currency or non-monetary, such as "segundos"). Example: `segundos`

The meaning and use of the Balances in each Tigo Market are different. Below is the known balances at each market.

## Tigo Paraguay Balances Description

<table>
    <tr>
        <th width="20%">Wallet Name</th>
        <th width="20%">Units</th>
        <th width="60%">Use and Product compatibility</th>
    </tr>
    <tr>
        <td>CORE BALANCE</td>
        <td>Guaraníes (Currency)</td>
        <td>Available for all purposes: 
        Calls (On Net, Xnet, Fixed Net, Internationales, Special Numbers, etc.), SMS (OnNet, XNet, Premium, etc.), MMS, Other (Ej.: Purchase Paquetigos, Loan Collection, Transfers, etc)</td>
    </tr>
    <tr>
        <td>PROMO LLAMADAS</td>
        <td>Guaraníes (Currency)</td>
        <td>Balance Available only for: 
        OnNet Calls & SMS For regular Commercial Plans
        Calls (On Net, Xnet, Fixed Net, Internationales) for Staff Plans higher that 19.90 USD
        </td>
    </tr>
    <tr>
        <td>PROMO_SALDO2</td>
        <td>Guaraníes (Currency)</td>
        <td>Promotional Balance only availabe for OnNet Calls</td>
    </tr>
    <tr>
        <td>PAQUETE GPRS</td>
        <td>Octet (bytes)</td>
        <td>Promotional Balance used for: GPRS (Not in use, currently)</td>
    </tr>
    <tr>
        <td>PROMO_SMS2</td>
        <td>SMS</td>
        <td>Promotional Available only for: SMS OnNet</td>
    </tr>
    <tr>
        <td>PAQUETE LLAMADA</td>
        <td>Seconds</td>
        <td>Promotional Available only for: OnNet Calls</td>
    </tr>
    <tr>
        <td>PLANES_SMS</td>
        <td>SMS</td>
        <td>Balance Available only for: OnNet & Xnet SMS 
            Corporate SMS
        </td>
    </tr>
    <tr>
        <td>PROMO_SMS</td>
        <td>SMS</td>
        <td>Promotional Balance Available only for: SMS OnNet</td>
    </tr>
    <tr>
        <td>PAQUETE LLAMADA3</td>
        <td>Seconds</td>
        <td>Promotional Balance Available only for: OnNet Calls</td>
    </tr>
    <tr>
        <td>PAQUETE_SMS</td>
        <td>SMS</td>
        <td>
        Promotional Balance Available only for: OnNet + Xnet SMS (Claro, Vox y Personal)
        </td>
    </tr>
    <tr>
        <td>PAQUETE_SALDO2</td>
        <td>Seconds</td>
        <td>
        Balance Available only For: Calls (On Net, Xnet, Fixed Net)
        </td>
    </tr>
    <tr>
        <td>PROMO_SMS3</td>
        <td>SMS</td>
        <td>
        Promotional Balance only available for Calls to Argentina or SMS Packs to Argentina
        </td>
    </tr>
    <tr>
        <td>PROMO_SALDO3</td>
        <td>Guaraníes (Currency)</td>
        <td>
        Promotional Balance only Available for: OnNet Calls 
        OnNet SMS 
        Also Known as "Devolvato" Balance
        </td>
    </tr>
    <tr>
        <td>EXCEDENTE</td>
        <td>Guaraníes (Currency)</td>
        <td>
            Wallet Created for Convergent Plans
            Available for All activities:
            Calls (On Net, Xnet, Fixed Net, Internacionales, Special Number, etc.)
            SMS (OnNet, XNet, Premium, etc.), 
            GPRS (Camel Phase 3, OSA),
            MMS,
            Others (Ej.: Paquetigos, Loan Collection, Transfers, etc)
        </td>
    </tr>
    <tr>
        <td>PROMO_SMS4</td>
        <td>SMS</td>
        <td>Promotional Balance only Available for: OnNet SMS</td>
    </tr>
    <tr>
        <td>PAQUETE LLAMADA2</td>
        <td>Seconds</td>
        <td>Promotional Balance only Available for: OnNet + Xnet Call</td>
    </tr>
    <tr>
        <td>VA_MINUTOS</td>
        <td>Seconds</td>
        <td>Promotional Balance only Available for: OnNet Call</td>
    </tr>
    <tr>
        <td>MINSALVA</td>
        <td>Seconds</td>
        <td>Promotional Balance only Available for: OnNet + Xnet + Fixed Net Call
</td>
    </tr>
    <tr>
        <td>VA_GPRS</td>
        <td>Octet (bytes)</td>
        <td>Not in use, used to be for Data Packages in APNs INTERNET and WAP</td>
    </tr>
    <tr>
        <td>MIN_PLAN</td>
        <td>Seconds</td>
        <td>For convergence plans for OnNet + Xnet + Fixed Net</td>
    </tr>
    <tr>
        <td>PROMO_SMS5</td>
        <td>SMS</td>
        <td>Promotional Balance only Available for: SMS OnNet + Xnet</td>
    </tr>
    <tr>
        <td>PROMO_SMS6</td>
        <td>SMS</td>
        <td>
        Promotional Balance only Available for: SMS OnNet
        </td>
    </tr>
    <tr>
        <td>DPI</td>
        <td>Mbytes</td>
        <td>
        This balance is the actual Mbytes left in the DPI Quota for a Subscriber. 
        This information should match the <code>/subscriber/{msisdn}/quota</code> API response. 
        Note that this special wallet does not return an <code>expirationDate</code>
        </td>
    </tr>
</table>

## Tigo Guatemala Balances Description

<table>
    <tr>
        <th width="20%">Wallet Name</th>
        <th width="20%">Units</th>
        <th width="60%">Use and Product compatibility</th>
    </tr>
    <tr>
        <td>CORE BALANCE</td>
        <td>Quetzales (Currency)</td>
        <td>Main Balance, Available for all purposes
        </td>
    </tr>
    <tr>
        <td>FREE SECONDS BALANCE</td>
        <td>Seconds</td>
        <td>Balance Available only for: 
        OnNet Calls
        </td>
    </tr>
    <tr>
        <td>PROMOTIONAL BALANCE 1</td>
        <td>Quetzales (Currency)</td>
        <td>Promotional Balance only availabe for Local Calls (On-Net and Other Networks)</td>
    </tr>
    <tr>
        <td>PROMOTIONAL BALANCE 2</td>
        <td>Quetzales (Currency)</td>
        <td>Monthly credit for Postpaid with fixed billing, used only for Local Calls, International Calls and SMS</td>
    </tr>
    <tr>
        <td>SMS BALANCE</td>
        <td>SMS</td>
        <td>SMS Packages Available only for: Local SMS (On-Net and Other Networks)</td>
    </tr>
    <tr>
        <td>DATA BALANCE</td>
        <td>Bytes</td>
        <td>DEPRECATED use /quota API instead</td>
    </tr>
    <tr>
        <td>WELCOMEPACK</td>
        <td>Quetzales (Currency)</td>
        <td>Promotional Balance only availabe for Local Calls (On-Net and Other Networks)</td>
    </tr>
    <tr>
        <td>FREE SECONDS BALANCE 2</td>
        <td>Seconds</td>
        <td>?</td>
    </tr>
    <tr>
        <td>Free Seconds balance 3</td>
        <td>Seconds</td>
        <td>?</td>
    </tr>
    <tr>
        <td>FREE SECONDS BALANCE 4</td>
        <td>Seconds</td>
        <td>?</td>
    </tr>
    <tr>
        <td>SMS BALANCE 2</td>
        <td>SMS</td>
        <td>
        SMS to ANY destination, including Local and International
        </td>
    </tr>
    <tr>
        <td>SMS BALANCE 3</td>
        <td>SMS</td>
        <td>
        SMS To Local (ON-net and Other Networks)
        </td>
    </tr>
    <tr>
        <td>MMS BALANCE INT</td>
        <td>MMS</td>
        <td>
        MMS
        </td>
    </tr>
    <tr>
        <td>SMS BALANCE 4</td>
        <td>SMS</td>
        <td>
        SMS to Tigo (On-Net)
        </td>
    </tr>
    <tr>
        <td>Free Second Balance 5</td>
        <td>Seconds</td>
        <td>
            ?
        </td>
    </tr>
</table>


+ Parameters

    + msisdn (required, string, `595986749778`) ... Mobile number of Tigo Subscriber in international format.

+ Model (application/json)
    
    JSON representation of the Tigo Subscriber's Balance

    + Body
    
            {
                "balances": [
                    {
                        "wallet": "CORE BALANCE",
                        "expirationDate": "2017-01-14T20:59:59",
                        "balanceAmount": 6.8585,
                        "description": "Saldo principal",
                        "unit": "Gs."
                    },
                    {
                        "wallet": "PROMO LLAMADAS",
                        "expirationDate": "2017-01-13T21:50:11",
                        "balanceAmount": 0,
                        "description": "Saldo promocional",
                        "unit": "Gs."
                    },
                    {
                        "wallet": "PROMO_SALDO2",
                        "expirationDate": "0001-12-31T22:00:00",
                        "balanceAmount": 0,
                        "description": "Saldo promocional",
                        "unit": "Gs."
                    },
                    {
                        "wallet": "PAQUETE_GPRS",
                        "expirationDate": "0001-12-31T22:00:00",
                        "balanceAmount": 0,
                        "description": "Saldo PAQUETIGO de Internet",
                        "unit": "MB"
                    },
                    {
                        "wallet": "PROMO_SMS2",
                        "expirationDate": "0001-12-31T22:00:00",
                        "balanceAmount": 0,
                        "description": "Saldo PAQUETIGO de mensajes",
                        "unit": "unidades"
                    },
                    {
                        "wallet": "PAQUETE LLAMADA",
                        "expirationDate": "0001-12-31T22:00:00",
                        "balanceAmount": 0,
                        "description": "Saldo PAQUETIGO de llamadas",
                        "unit": "segundos "
                    },
                    {
                        "wallet": "PLANES_SMS",
                        "expirationDate": "0001-12-31T22:00:00",
                        "balanceAmount": 0,
                        "description": "Saldo para plan de mensajes",
                        "unit": "unidades"
                    },
                    {
                        "wallet": "PROMO_SMS",
                        "expirationDate": "0001-12-31T22:00:00",
                        "balanceAmount": 0,
                        "description": "Saldo para mensajes dentro de la red",
                        "unit": "unidades"
                    },
                    {
                        "wallet": "PAQUETE LLAMADA3",
                        "expirationDate": "0001-12-31T22:00:00",
                        "balanceAmount": 0,
                        "description": "Saldo PAQUETIGO de llamadas",
                        "unit": "segundos "
                    },
                    {
                        "wallet": "PAQUETE_SMS",
                        "expirationDate": "0001-12-31T22:00:00",
                        "balanceAmount": 0,
                        "description": "Saldo para mensajes",
                        "unit": "unidades"
                    },
                    {
                        "wallet": "PAQUETE_SALDO2",
                        "expirationDate": "0001-12-31T22:00:00",
                        "balanceAmount": 0,
                        "description": "Saldo para todas las operadoras",
                        "unit": "Gs."
                    },
                    {
                        "wallet": "PROMO_SMS3",
                        "expirationDate": "0001-12-31T22:00:00",
                        "balanceAmount": 0,
                        "description": "Saldo para mensajes dentro de la red",
                        "unit": "unidades"
                    },
                    {
                        "wallet": "PROMO_SALDO3",
                        "expirationDate": "0001-12-31T22:00:00",
                        "balanceAmount": 0,
                        "description": "Saldo Por Compra De Telefono",
                        "unit": "Gs."
                    },
                    {
                        "wallet": "PROMO_SMS4",
                        "expirationDate": "0001-12-31T22:00:00",
                        "balanceAmount": 0,
                        "description": "Saldo para mensajes dentro de la red",
                        "unit": "unidades"
                    },
                    {
                        "wallet": "PAQUETE LLAMADA2",
                        "expirationDate": "0001-12-31T22:00:00",
                        "balanceAmount": 0,
                        "description": "Saldo PAQUETIGO de llamadas",
                        "unit": "segundos "
                    },
                    {
                        "wallet": "VA_MINUTOS",
                        "expirationDate": "0001-12-31T22:00:00",
                        "balanceAmount": 0,
                        "description": "Saldo Billetera Corporativa",
                        "unit": "segundos"
                    },
                    {
                        "wallet": "MINSALVA",
                        "expirationDate": "0001-12-31T22:00:00",
                        "balanceAmount": 0,
                        "description": "Saldo de emergencia para minutos",
                        "unit": "segundos"
                    },
                    {
                        "wallet": "VA_GPRS",
                        "expirationDate": "0001-12-31T22:00:00",
                        "balanceAmount": 0,
                        "description": "Saldo PLAN internet",
                        "unit": "MB"
                    },
                    {
                        "wallet": "PROMO_SMS5",
                        "expirationDate": "0001-12-31T22:00:00",
                        "balanceAmount": 0,
                        "description": "Saldo para mensajes dentro de la red",
                        "unit": "unidades"
                    },
                    {
                        "wallet": "PROMO_SMS6",
                        "expirationDate": "0001-12-31T22:00:00",
                        "balanceAmount": 0,
                        "description": "Saldo para mensajes dentro de la red",
                        "unit": "unidades"
                    },
                    {
                        "wallet": "DPI",
                        "balanceAmount": 0,
                        "description": "Billetera de navegacion",
                        "unit": "MB"
                    }
                ]
            }

## Query Subscriber's Balances Collection [GET]
+ Request

    + Headers
    
            Authorization: Bearer {access_token}

+ Response 200

    [Subscriber Balances Collection][]

