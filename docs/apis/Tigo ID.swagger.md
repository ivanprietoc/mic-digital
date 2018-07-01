FORMAT: 1A
HOST: https://mic-test.apigee.net/

# Tigo ID 
# Group Introduction
*Tigo ID* is Tigo's federated identity solution, based on the industry standard 
[OpenID Connect 1.0](http://openid.net/specs/openid-connect-core-1_0.html),
allowing Tigo Customers to create and maintain their digital identity in a single 
place, and enabling our partner's and own applications identify (authenticate) and 
get Authorization from Tigo Customers.  

## Benefits to Tigo Customers
Tigo ID offers the following the possibilities to our **Customers**:

* **Sign in with a Mobile number**:  
  Tigo ID will take care of identifying the mobile phone number using one time password over SMS 
  or Header Enrichment when the Mobile User-agent is connected to the Tigo Mobile Network.  
  This is useful for applications that only require identifying the mobile subscriber number of the user.

* **Sign in with email**:  
  a user will be able to create an account and log in using his prefered email provider.  
  An email with a validation code will be sent to the user's account in order to verify the user's email address.

* **Sign in with a social network ( Facebook, Twitter, Google, LinkedIn, Yahoo, Microsoft )**:  
  This will allow the user to sign up with his prefered social network, making it easier 
  for customers to sign-up, without filling our forms and remembering yet another password.

* **Authorize and consent the sharing of their Identity with Applications**:  
  Tigo Customers will be aware of what information and to whom they share their identity with.
  Additionally, Tigo Customers can review Applications they have granted acesss of their identity 
  and revoke access to specific applications if needed.

* **Authenticate, create and validate a Tigo Money account**:
  Tigo Customers can authenticate, and authorize the viewing of their mobile money wallets.
  

## Benefits to Tigo Applications and Partner's
Tigo ID offers the following possibilities for our Own and Partner's **Applications**:

* Identify the User's Mobile Number and its corresponding Tigo Customer number
* Identify the User's Email address
* Identify the User's Profile information, such as: Name, Gender, Birthday, Photo, etc.
* Obtain a valid OAuth 2.0 `access_token` to access other Tigo APIs.
* Obtain consent from the User to access his Identity information and any other information exposed in other Tigo APIs.
* Auto-merge User identities, based on the email address.
* Auto-merge User Social Network identites ("Hyper-profile"), based on [Gigya's Social Login](http://developers.gigya.com/010_Developer_Guide/10_UM360/030_Social_Login) best practices.
* Auto-link (more than one) User's Mobile Number to User's profile.
* Takes care of Password Recovery, Email verification and MSISDN verification.

------------------------------------------------------------------------------------------------------------------

Tigo ID is based on the **OpenID Connect** industry standard [Spec](http://openid.net/connect/), 
and implements two main flows:

* Authorization Code Flow [Spec](http://openid.net/specs/openid-connect-basic-1_0.html)
* Implicit Flow [Spec](http://openid.net/specs/openid-connect-implicit-1_0.html)

At the end of the flow you should have access to an [id_token](http://openid.net/specs/openid-connect-core-1_0.html#IDToken) 
and *optionally* a valid OAuth 2.0 Bearer [access_token](http://tools.ietf.org/html/rfc6749#section-1.4).  
The `id_token` SHOULD be validated as explained in the [specs](http://openid.net/specs/openid-connect-implicit-1_0.html#IDTokenValidation)

# Group Onboarding 
Onboarding is the process of setting up the application to be able to use Tigo ID.
This will show the process of onboarding an application and getting ready for integrating with the flows.

## Tigo ID API Setup

Within the Apigee organization there **MUST** be an "Tigo Identity Product" deployed in API Products.  
This API Product must contain the **Allowed OAuth Scopes** that will be supported by the Tigo ID API.  
This API Product needs to be created only once, and includes the following built-in `scope`s:

* `openid` used to identify this API is compliant with the OpenID Connect 1.0 spec.
* `profile` used to request the User's personal information such as: name, birthday, photo.
* `email` used to request the User's email address.
* `mobileid` used to request the User's mobile phone number and Tigo Customer Number.
* `phone` same as `mobileid`.
* `homeid` used to request the User's Tigo Home (Residential CableTV, Internet and fixed telephony) Customer Number.
* `mfsid` Requests access to the user’s MFS wallet ID. Must be combined with the mobileid scope.
* `mfsid.account.read ` Requests access to the read the MFS wallet balance and information. Must be combined with the mfsid scope.
* `mfsid.account.tx ` Requests to transfer an amount from the user’s wallet. Must be combined with the mfsid scope and requires that the value to transfer be set in the  account.tx property of the mfs_params parameter



Additional `scope`s can be defined, but won't affect the Tigo ID behavior, except for generating an `access_token` valid for all
the requested `scope`s.  
Additional `scope`s SHOULD also be localized, so the user understands what permissions are beign granted to the Application (Consent).  
In order to localize additional `scope`s, a custom variable named `scopes_ui_localization` can be configured in the API Product.  
`scopes_ui_localization` must contain a serialized JSON as follows:

        {
            "email": {
                "en": "your email address", 
                "es": "Su direcci\u00f3n de correo electronico"
            }, 
            "mobileid": {
                "en": "Your Mobile Phone number", 
                "es": "Tu numero de telefono movil"
            }, 
            "phone": {
                "en": "Your Mobile Phone number", 
                "es": "Tu numero de telefono movil"
            }, 
            "profile": {
                "en": "Your Profile Information: name, gender, birthday.", 
                "es": "Su informaci\u00f3n personal: Nombre, edad y cumplea\u00f1os."
            }, 
            "sms": {
                "en": "Send SMS to your mobile", 
                "es": "Enviarle Mensajes Cortos a su Movil"
            }
        }


## Developer onboarding

Before an Application can access the Tigo ID APIs or any other Tigo APIs, the Developer of the application needs 
to be registered in our Apigee platform. For this the Apigee admin interfaces allows to create a **Developer** record
which must have all Primary Point of Contact information for the Application Developer.


Once the developer has been created, we can register and associate a **Developer App**.

## Application onboarding

The **Developer App** must be registered and associated with a developer, 
so it can be granted access to Tigo ID APIs and any other Tigo API.  
After creating the Application record and granting access to specific API products, 
the **Client credentials** of the Application are assigned: 
- `client_id`
- `client_secret`  

These credentials are the ones that are going to identify the app within the Tigo ID flows.  

----

In order to use the Tigo ID APIs, the Application MUST provide a valid `redirect_uri`,
this will serve as a **Callback URL** where Tigo ID will notify the outcome of any authentication flow.  
This `redirec_uri` MUST exactly match the parameters sent by the Application to the **Authorization Endpoint**.  
Only one callback URL can be configured per Application, however, If an application needs to have more than one
Callback URL, then another Application record can be created.  
As a bare minimum, if the aplication wishes to use Tigo ID to identify its users, then the aplication MUST
have the **Tigo Identity Product** API product associated.  

----

Optionally, the following additional **Custom Attributes** can be defined in the **Developer App** record, 
which will affect the Tigo ID behavior as follows:
- `app_logo_url`: a valid URL where the Application Icon is published, a valid HTTPS URI is prefered. 
  If present, Tigo ID will use this image/logo in the Consent User Interface. So the end user identifies 
  your Application visually.
- `preapproved_consent`: **true/false**, indicates if this Application has a pre-approved consent, 
  so the Consent User Interface will never be displayed to users of this Application.  
  This feature is reserved to Tigo's own applications and strategic Partners.
- `expiresIn`: a time in milliseconds to set the validity of the access_token. If not set the default value is one hour (3600 seconds, or 3600000 milliseconds). Although this is set in milliseconds in the configuration, the time returned with the access token is still set in seconds.


## Registration Flow

Users are created after verifing their email accounts via code input or clicking on the verification link sent to their email addresses, this registration flow can be simplified by setting the `registration_flow_simplified` flag (see the flags section below).

Simplified flow will ommit the verification steps and create the user account straight forward and leaving them unverified until user verifies them clicking an link sent to their email addresses.

## Style
Tigo ID use [Materialize css](http://materializecss.com/) which is a design language developed by Google that synthesizes the principles of good design along with innovation and technology.
The design is a concept, a philosophy, a design language with guidelines focused on the design used in the user interface of Android, but also for the web and on the platform, it is a cleaner design in which they predominate the animations and transitions of response, the filling and the effects of the truth stories such as lighting and shadows.

# Group Guidelines

This section provides simple guidelines that developers *MUST* follow. Failure to do so could result in some broken behavior, and /or security issues.

## Implicit flow

Implicit flow is only recommended for a single page app. In any case, the use of implicit flow should be approved by the Millicom team. When possible it is better to use code flow for public clients with PKCE.

## Smartphone applications

* Whenever possible, use standard compliant SDKs for instance:
    * Android: https://github.com/openid/AppAuth-Android
    * IOS: https://github.com/openid/AppAuth-iOS
* Never ever EVER store client_secret within a smartphone application.
* Implementation *MUST* never use embedded webviews as these pose some issues:
    * security implications : credentials could be intercepted
    * user experience : sandboxed cookie jar doe snot share session with the default browser on the device, so user might have to relog in, even if he already has logged in on browser, or on other conforming app.
* In order to provide more security and better user experience (sharing sessions), Smartphone applications *MUST* implement Tigo ID integration using:
    * [Custom tabs](http://developer.android.com/tools/support-library/features.html#custom-tabs) on android 
    * [SFSafariViewController](https://developer.apple.com/library/ios/documentation/SafariServices/Reference/SFSafariViewController_Ref/)
    * if required implementation is not available due to access or version, app should revert to using default external browser on device.
--
## Group Account Chooser
The account chooser it’s a helper for the user, to remove the burden of inputs, it will also allow us to get more emails and numbers associated together.
The email and mobile accounts will be displayed in a single view depending on the requested scope.

## Basic operation

The operation of the account chooser is given by the presence of the TIGO_ACCOUNTS cookie, if it does not exist it will be created at the end of the successful authentication process.
The TIGO_ACCOUNTS cookie refers to an object in the database, the contents of this object are the accounts that the user has used to authenticate (with the same user-agent), thus providing the account selector,
a simplified way for the user to access their different stories. The account selector will store both mobile number and email accounts.
Once TigoId is invoked with the present cookie, TigoId proceeds to show the user a list of accounts that the user could use to authenticate without having to re-enter the email or msisdn.
The last account used by the user appears as the first option in the list of accounts to be selected, if this is selected, it proceeds to autologin (no password or OTP is needed).
If you select another account, which is not the last used, TigoId proceeds to require the user's password, or OTP is sent in case of mobile line to re-identify the user.
## Flow according to requested scope

For when profile is requested, and mobile Flow is invoked only when enrichment is not possible, either not present, or flags are stating to not execute in one of many ways we have now.
## Profile Flow

If profile history cookie not present, display email input field. If not get all email, name, gravatar from history, build view and display account selector screen.
## Mobile flow

If prompt = none, then the flow should try header enrichment directly without showing account chooser if hint is sent, and that option is available, the flow should continue as if it had been “clicked” if email is selected, then the mobile account associated to that email should be used, if none are available, then one should be prompted to be added, if a few are available then chooser should be displayed.
If number selected needs revalidation, then OTP/vs HE rules apply.
Omit he also still a valid flag for this, if it is sent to true then the HE will be bypassed.
If mobile or profile history cookie not present display msisdn input field, if present get all mobile number, email, name, gravatar, build view and display account selector screen.

Image AC-Mobile, AC-profile, Account chooser profile and account chooser mobile.

# Group API Usage
Once the preliminary setup is done, The Application developer can use the Tigo ID APIs 
to obtain the identity of a Tigo Customer and optionally an `access_token` to access 
other Tigo APIs on his/her behalf.  

At this point, the Application Developer must have:
- a `client_id`: unique identifier of the Application. Considered *public* information.
- a `client_secret`: a password assigned to the Application. Considered *secret* information.
- a `redirect_uri`: this is a URI implemented by the Application, where the final result of  the authentication flows will receive the Tigo Customer identity information or an error.
    - If implementing Web Applications, this should be a valid web URI, such as: `https://myapp.domain/tigoid/callback`
    - if implementing a Native Application, this should be a registered protocol handler for the App, such as: `x-myapp://tigoid/callback`

# Public clients
Tigo ID supports both Confidential and Public clients as defined in [RFC 6749 S 2.1](https://tools.ietf.org/html/rfc6749#section-2.1)
The only restriction imposed on a public client is that it *MUST* use [PKCE](https://tools.ietf.org/html/rfc7636) with S256 in order to be able to complete the code flow. Implicit Flow is not recommended under any circumstance. Although currently supported, there is no guarantee that it will be supported or maintained in the future.

## PKCE
PKCE is defined in the [RFC 7636](https://tools.ietf.org/html/rfc7636). Tigo ID supports `code_challenge_method`s `S256` and `plain` (default). Public clients may only use `S256`.
When PKCE is used, developer can request the `access_token` from the token endpoint without using the client_secret.

---
Depending on the type of application, the Developer can use the Tigo ID API in 2 ways:

## Authorization Code flow
In this flow, the Application is assumed to have a Server side (backend) component and a User Interface (frontend) component, such as the case of a Web Application implemented using PHP in the Web Server or a Native App that uses it's own Backend Server via APIs.  

A public client may also use the code flow provided it uses PKCE with S256 method.

The steps to authenticate a Tigo Customers using this flow are as follows:

1. Application frontend opens Browser or embedded WebView (User-Agent) poiting to the **Authorization Endpoint** URI.
2. User interacts with Tigo ID user interfaces to Login or Register (if new user).
3. (Only the first time) User grants authorization (consent) to Application, this is asked only once per different Application, User & Scope.
4. Tigo ID will redirect User-Agent to the Application's `redirect_uri`
5. Application must read the **query parameters** sent in the `redirect_uri` and process the response, which will contain:
    - an authorization `code` if authentication was succesfull.
    - an `error` if not.
6. Application backend must receive the `code` and call the Tigo ID **Token Endpoint** including the `code`, `client_id` and `client_secret`, in exchange it will receive a `id_token` and `access_token` back.
7. the `id_token` should be verified as authentic and will contain the Tigo User's identity. 
8. If requested, the `access_token` will allow the Application to access the **UserInfo endpoint** and other Tigo APIs on behalf of the user.
9. Self service apps may access to **enhanced details** of the User if configured (self_care_access).

## Implicit Flow
In this flow, the Application is assumed to be running exclusively in the User-agent (browser) or in the User's device (App) **without** coordination with a backend server, such as the case of a "Single Page Application" in HTML+Javascript or Native App without a Backend server.
It is important to note, that in this case, the Application's Code (even if obfuscated) is accesible to end-users, so it cannot store the `client_secret` or any other secret information in the application's code, for this reason, the `client_secret` is not used.

NOTE: it is recommended that these applications use public client implementation using PKCE. `implicit` flow is considered less safe and there is no guarantee we will keep it updated.

The steps to authenticate a Tigo Customers using this flow are as follows:

1. Application frontend opens Browser or embedded WebView (User-Agent) poiting to the **Authorization Endpoint** URI.
2. User interacts with Tigo ID user interfaces to Login or Register (if new user).
3. (Only the first time) User grants authorization (consent) to Application, this is asked only once per different Application, User & Scope.
4. Tigo ID will redirect User-Agent to the Application's `redirect_uri`
5. Application must read the **fragment** parameters in the `redirect_uri` and process the response, which will cotain:
    - the `id_token` and (if requested) the `access_token`, if authentication was succesfull.
    - an `error` if not.
6. the `id_token` should be verified as authentic and will contain the Tigo User's identity. 
7. If requested, the `access_token` will allow the Application to access the **UserInfo endpoint** and other Tigo APIs on behalf of the user. 

## Tigo ID `id_token`s

The primary goal of all the authentication flows is to obtain the User's Identity in a secure and _verifiable_ way.  
In Open ID Connect, the way to obtain this user identity is through the `id_token`.  
The `id_token` is a string representation of the User's Identity Claims, encoded in 
a [JSON Web Token](https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-27), that can be encrypted and signed.  
Tigo ID only supports signed `id_token`s using the **HS256** algorithm and the Application's `client_secret` as signing key.
Tigo ID DOES NOT support encrypted `id_token`, since this level of security is supplied by the use of TLS/SSL in HTTPS.
Inside an `id_token` you'll find the following "Claims" about the user's identity:

To be completed:

|Claim name|Content|Example|present when using scopes:|
|:--------:|:------|:------|:-------------------------|
|sub|unique user identifier. If user has registerd a profile, email or social network before, this will be a UUID. otherwise a MSISDN|`12312313313`|*always*|
|iss|unique Identity Provider identifier. This will always be Tigo ID's base URL|`https://id.tigo.com/openid`|*always*|
|aud||||
|iat||||
|exp||||
|auth_time||||
|at_hash||||
|nonce||||
|name||||
|email||||
|email_verified||||
|phone||||
|phone_verified||||
|tigo_customerId||||
|tigo_contractNumber||||
|mfsid|mfs account identifier|595123123123|mfsid mfsid.account.read mfsid.account.write|


## Security considerations

- All endpoints MUST be accessed over TLS/SSL exclusively. 
  - With the only exception when the requested `scope` contains `phone` or `mobileid`, 
    to be able to detect the MSISDN headers injected by the Tigo Network, Tigo ID will 
    do a temporary redirect to a clear HTTP URL, just to detect and extract the headers, 
    before continuing the rest of the flow using TLS/SSL.
- When calling the **Authorization endpoint** URL from a Native Application, prefer opening the URL in the Device's 
  Native Browser instead of using an embedded WebView. For the following reasons:
  - the Application opening the embedded WebView can intercept User's interactions, including user's passwords.
  - usually, the embedded WebView has a private (clean) cookie store, so if User has previously signed-in to a 
    Social Network or another Application that uses Tigo ID, the Embedded WebView is not aware of those sessions, so it
    will request the user to sign-in again.
- Treat `client_secret` as an Application password that needs to be stored securely in a Server (backend).  
  *NEVER* include this in a Native App's code or in the Client side code (Client side Javascript), 
  even when using obfuscation techniques.  
  In general, an application user should never have access to the `client_secret` even if encrypted or obfuscated in the Application Code.  
  You should be prepared to change the `client_secret` if it gets compromised, and this SHOULD NOT require a new version of your Application Code
  to be downloaded or distributed by all your users.
- Always verify the `state` parameter in your **Callback URL** to check if it is the same you sent in the **Authorization Endpoint** request.
- Always verify the `id_token` according to [Open ID Connect 1.0 recommendations](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation)
  - Tigo `id_token`s are signed using the **HS256** algorithm and the `client_secret` is used as the signing key.
- Beware of the `access_token` expiration time (parameter `expires_in`), to renew it, your application will need to go through the **Authorization Endpoint** to get another valid `access_token`.

## Flags

It should be noted that all the flags are configurators for each of the applications in their respective TigoID database, so for example there are no applications that send a flag of type preset_country flag, rather what is done is an attribute configuration at the level of the database.

|Flag|Description|
|:--:|:----------|
|social_login|Enable social buttons to import the account from facebook or google where the possible parameters are: social_login_on (default) or social_login_off.|
|mobileid_account|In previous versions, this flag forced the visualization of screens to add a line or to select a line: mobileid_account_add or mobileid_account_select are the options. It is possible that in the new version of TigoID, these flags are deprecated.|
|homeid_account|It has a description similar to mobileid_account.|
|tigo_claims|The options are: tigo_claims_optional (default), tigo_claims_enforced, tigo_claims_none. Once the user validates his line, TigoID consults the service (GetClientAccountGeneralInfo) which gets the contract and client numbers where this response will be added to the JWT, now if this service responds with error or the user does not exist this flag manages the corresponding response and load the empty fields. In the event that the service responds with error TigoID will return the authentication process with error and will not make the respective call, loading the JWT with the empty fields.|
|omit_he|Avoid the flow where it is necessary to validate a line with your header information, this process is done via http, which is why this flag is used to vacate that functionality. Example: omit_he_true.|
|preset_country|Its functionality allows the forms to add a line or household plan that has a pre-selected country. example: preset_country_gt, preset_country_co, preset_country_py.|
|registration_flow|Allows the application to require that users have valid email accounts because the user creation process requires that a code sent to the email be entered.|
|api_version|It allows to define the information that TigoID responds in the id_token v2.|
|rememberMe|Deprecated flag that marked the field "remember me" in the tigoid forms.|

## Enhanced details
Enhanced details returns a user model which is the full representation of a user record.

For an app to have enhanced details it must have the `self_care_access` attribute. For JWT to have enhanced details i must have been generated with the scope profile.

For the app to access the phoneList and homeList attributes the app has to request a auth flow with the phone and homeid scopes respectively.

i.e: 

scope: openid phone  (invalid scope for enhanced details)
scope: openid homeid profile (valid scope for enhanced details with access to full homeid list)


## Group Authorization Endpoint
## Authorization Code Flow [/oauth/v2/authorize?response_type=code{&redirect_uri,client_id,scope,state,nonce,prompt,display,login_hint}]

This is the first endpoint The Client Application must call to initiate a Tigo ID authentication flow.  
This endpoint must be called within a User-Agent (Browser) since it may require User interaction.

### Succesful Response
At the end of the flow, your Application will receive a callback to your registered `redirect_uri`, 
in the *query string* the following parameters will be URL-encoded:

|Parameter name|Description|Example/Values|
|:-------------|:----------|:-------------|
|code |Authorization Code, a random string that SHOULD be used by your Application Backed server in the **Token endpoint** to get the `id_token` and `access_token`| `s6r3ge5w`|
|state|the same `state` parameter sent in the request, Use to verify this callback is correlated to your request and not a malicious redirect| |

> **IMPORTANT**:
> the `code` has a short expiration time of about 60 seconds, 
> so your Application Backend Server must exchage it at the **Token Endpoint** 
> as soon as possible.

At this point, if your Application is able to get a `id_token` and verify the user's identity, 
you should reply back to the User to grant access to your application and start a new session.

### Error Response
If during the flow, for any reason the User is not able to authenticate, or rejects Consent, 
your Application will receive a callback to your registered `redirect_uri`, 
in the *query string* the following parameters will be URL-encoded:

|Parameter name|Description|Example/Values|
|:-------------|:----------|:-------------|
|error|Error code according to [OAuth 2.0](http://tools.ietf.org/html/rfc6749#section-4.1.2.1) and [OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html#AuthError)|`access_denied`|
|error_description|Human description of the error cause|`User cancelled login`|
|state|the same `state` parameter sent in the request, Use to verify this callback is correlated to your request and not a malicious redirect| |

### GET

+ Parameters

    + redirect_uri (required,string,`https://www.domain.tld/tigoid/callback`) ... URL encoded String that must match *exactly* the URL added in the onboarding process. The users User-Agent will be redirected to the  `redirect_uri` once the authentication/authorization flow has concluded (either sucessfully or not).
    + client_id (required,string,`cAGOBtZREWM2SRXmP3JQZ8uhBDJQzA7Y`) ... Client identifier to identify the application that is requesting the authentication flow. If the application ID is not valid the call will fail.
    + scope (required,string ,`openid profile email phone homeid`) ... space separated scopes requested in the current call. this will prompt the user with the consent part of the flow. Minimally for an openID connect flow the `scope` openid must be requested, else it will not be considered a valid openid connect flow.
        + Values
            + `openid`
            + `openid profile`
            + `openid email`
            + `openid phone`
            + `openid mobileid`
            + `openid profile email`
            + `openid profile email phone`
            + `openid profile email mobileid`
            + `openid profile email phone homeid`
    + response_type (required,string,`code`) ... Type of response requested. Always use `code` to initiate an Authentication Code flow.
    + state (required,string,`tigoid-authenticated`) ...  any string that will be sent back to your application at the `redirect_uri`, so you can correlate to the authorization request.
    + nonce (optional,string,`4ac27273-0cab-70fa-8d55-787964ace0d6`) ... randomly generated string with sufficient entropy to prevent Replay Attacks. This will be inside the `id_token` so it can be verified.
    + prompt (optional,string,`login`) ... Forces Tigo ID to ask (or not ask) for login or consent to end user.
        + Values
            + `none`
            + `login`
            + `consent`
    + display = `page` (optional,string,`popup`) ... Tells Tigo ID in what type of User-Agent the pages should be rendered in.
        + Values
            + `page`
            + `popup`
            + `touch`
            + `wap`
    + login_hint (optional,string,`user@example.com`) ... Tells Tigo ID to try authenticate a known user
      identified by the supplied email address or a MSISDN. If Tigo ID cannot identify the requested user, 
      it will will return an `error` to the Application's `redirect_uri`.
    + auth_flow (optional,string,`redirect`) ... Tells Tigo ID to set gigya auth flow parameters to 'redirect' instead of default pop up behavior.
    + flags: `social_login_on`(string, optional) - Tells Tigo ID to modify default settings. Toogle social login on/off, define tigo claims for other operators, ommit header enrichment, define registration flow.
        + Members
            + `social_login_on`
            + `social_login_off`
            + `tigo_claims_mandatory`
            + `tigo_claims_optional`
            + `tigo_claims_none`
            + `omit_he_on`
            + `omit_he_off`
            + `registration_flow_simplified`
            + `mobileid_account_add`
            + `mobileid_account_select`
            + `homeid_account_add`
            + `homeid_account_select`
            + `preset_country_*`
            
    + code_challenge (optional, string) ... Signs the Authorize request so that code verifier is requiered in the token endpoint.

    + tigo_claims (optional, string, `mandatory`) ... Tells Tigo ID what Lookup callout behavior should have over OTP flow.
        + Values
            + `mandatory`
            + `optional (default)`
            + `none`
    
 
+ Request Succesful Request

+ Response 302
  Succesful outcome.  
  This response will cause a redirect in a normal User-Agent (Browser), so your `redirect_uri` will be called.

    + Headers

            Location: {redirect_uri}?code={code}&state={state}

+ Request Error during Login or Consent

+ Response 302
  Error during authentication or consent.  
  This response will cause a redirect in a normal User-Agent (Browser), so your `redirect_uri` will be called.  
  Possible Error Codes according to OAuth 2.0 [Spec](http://tools.ietf.org/html/rfc6749#section-4.1.2.1)

    + Headers

            Location: {redirect_uri}?error={error_code}&error_description={error_description}&state={state}

+ Request Invalid Request

+ Response 400 (application/json)
  Error when sending an Invalid Request

    + Body

            {"error" : "bad_request", "error_description" : "invalid redirect uri"}

## Implicit Flow [/oauth/v2/authorize{?response_type,redirect_uri,client_id,scope,state,nonce,prompt,display,login_hint}]

This is the first endpoint The Client Application must call to initiate a Tigo ID authentication flow.
This endpoint must be called within a User-Agent (Browser) since it may require User interaction.  
At the end of this flow, your Application will receive a callback to your registered `redirect_uri`, and in the _fragment_
component, the `id_token` and `access_token` will be encoded and ready to be extracted and verified.

### GET

+ Parameters

    + redirect_uri (required,string,`https://www.domain.tld/tigoid/callback`) ... URL encoded String that must match *exactly* the URL added in the onboarding process. The users User-Agent will be redirected to the  `redirect_uri` once the authentication/authorization flow has concluded (either sucessfully or not).
    + client_id (required,string,`cAGOBtZREWM2SRXmP3JQZ8uhBDJQzA7Y`) ... Client identifier to identify the application that is requesting the authentication flow. If the application ID is not valid the call will fail.
    + scope (required,string ,`openid profile email mobileid`) ... space separated scopes requested in the current call. this will prompt the user with the consent part of the flow. Minimally for an openID connect flow the `scope` openid must be requested, else it will not be considered a valid openid connect flow.
        + Values
            + `openid`
            + `openid profile`
            + `openid email`
            + `openid phone`
            + `openid mobileid`
            + `openid profile email`
            + `openid profile email phone`
            + `openid profile email mobileid`
            + `openid mobileid mfsid mfsid.account.read mfsid.account.write`
    + response_type (required,string,`id_token token`) ... Type of response requested. To initiate a Implicit flow, specify any combination of `id_token` and `token`.
        + Values
            + `id_token`
            + `token`
            + `id_token token`
    + state (required,string,`tigoid-authenticated`) ...  any string that will be sent back to your application at the `redirect_uri`, so you can correlate to the authorization request.
    + nonce (required,string,`4ac27273-0cab-70fa-8d55-787964ace0d6`) ... randomly generated string with sufficient entropy to prevent Replay Attacks. This will be inside the `id_token` so it can be verified.
    + prompt (optional,string,`login`) ... Forces Tigo ID to ask (or not ask) for login or consent to end user.
        + Values
            + `none`
            + `login`
            + `consent`
    + display = `page` (optional,string,`popup`) ... Tells Tigo ID in what type of User-Agent the pages should be rendered in.
        + Values
            + `page`
            + `popup`
            + `touch`
            + `wap`
    + login_hint (optional,string,`user@example.com`) ... Tells Tigo ID to try authenticate a known user
      identified by the supplied email address or a MSISDN. If Tigo ID cannot identify the requested user, 
      it will will return an `error` to the Application's `redirect_uri`.

+ Request Succesful Request


+ Response 302
  Succesful outcome.  
  This response will cause a redirect in a normal User-Agent (Browser), so your `redirect_uri` will be called.

    + Headers

            Location: {redirect_uri}#access_token={access_token}&token_type=bearer&id_token={id_token}&expires_in={expires_in}&state={state}

+ Request Error during Login or Consent


+ Response 302
  Error during authentication or consent.  
  This response will cause a redirect in a normal User-Agent (Browser), so your `redirect_uri` will be called.  
  Possible Error Codes according to OAuth 2.0 [Spec](http://tools.ietf.org/html/rfc6749#section-4.1.2.1)

    + Headers

            Location: {redirect_uri}?error={error_code}&error_description={error_description}&state={state}

+ Request Invalid Request

+ Response 400 (application/json)
  Error when sending an Invalid Request

    + Body

            {"error" : "bad_request", "error_description" : "invalid redirect uri"}

## Group Token Endpoint
## Obtain access_token [/oauth/v2/accesstoken]
The Token endpoint allows the Application to get an `id_token` and `access_token` in exchange from a valid Authorization `code`
obtained after completing a successful **Authorization Code Flow**.

### POST

+ Request (application/x-www-form-urlencoded)

    + Headers

            Authorization: Basic Base64({client_id}:{client_secret})

    + Body

            grant_type=authorization_code&code={code}&redirect_uri={redirect_uri}&code_verifier={code_verifier}

+ Response 200 (application/json)

        {
            "access_token": "6dgcyB7Z30w5XCAOSa75oRT4N2zO",
            "token_type": "Bearer",
            "refresh_token": "1hJ6YGvK9epTDCJBQImY0NAJFg2B4HjJ",
            "expires_in": "3599",
            "id_token": "eyJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbWljLXRlc3QuYXBpZ2VlLm5ldCIsImF1ZCI6Imh6YWxTWkpXZUc2V0tjM0NXVFQzTWl5bGNyQXFzTHFIIiwic3ViIjoiMzNjMDgyNmEtNDgyZC0xMWU0LWI1MzQtNzNjZDVmYTVkNzRkIiwiaWF0IjoxNDEyMTM3Mjg3LCJleHAiOjE0MTIxMzczNDcsImF1dGhfdGltZSI6MTQxMjEzNzI4NywibmFtZSI6IlJvYmVydG8iLCJlbWFpbCI6InJjbmF2YXNAZ21haWwuY29tIiwiZW1haWxfdmVyaWZpZWQiOiJ0cnVlIiwicGhvbmUiOiI1MDM3ODgzMjAxMCIsInBob25lX3ZlcmlmaWVkIjoidHJ1ZSIsInRpZ29fY3VzdG9tZXJJZCI6IiIsInRpZ29fY29udHJhY3ROdW1iZXIiOiIiLCJhdF9oYXNoIjoiSm1YNjY4czF2cm1ZajNvckV6YmJoQVx1MDAzZFx1MDAzZCIsIm5vbmNlIjoiODM0NzEwZGMtMmFiNC1lOGQ5LTVmNjgtNTQzZDU1NzU3Njk5In0.qnknWdJy1MLh53Hq1PSWSttyOOEqOhvRN0CTrnEUsPg"
        }

## Group User Information Endpoint
## Get User Information [/oauth/v2/getdetails]
Once your flow has been concluded you should have an `access_token` and an `id_token`. 
The `id_token` gives you some information about the user, but may be not include all "Claims" (User Identity attributes).  
To get all requested "Claims" of the user, you can query the **UserInfo** endpoint, 
Authenticating using OAuth 2.0 Bearer Tokens: just include a valid `access_token` obtained on the **Authorization Endpoints**

### GET


+ Request Succesful Request

    + Headers

            Authorization: Bearer {access_token}
    
+ Response 200 (application/json)

        {
            "birthdate": "1974-7-21", 
            "email": "rcnavas@gmail.com", 
            "email_verified": "true", 
            "family_name": "Navas", 
            "gender": "male", 
            "given_name": "Roberto", 
            "name": "Roberto", 
            "phone_number": "50378832010", 
            "phone_number_verified": "true", 
            "picture": "https://graph.facebook.com/1212097504/picture?type=large", 
            "sub": "33c0826a-482d-11e4-b534-73cd5fa5d74d", 
            "updated_at": 1412137262771
        }


## Group Session management
## Token revocation endpoint [/oauth/v2/revoke]
When your user logs out of the app, you can consume an endpoint to revoke the token, it is in good practice as the user's action shows that he does not wish to maintain the session.
Using this endpoint you can revoke the `refresh_token` or the `access_token`.
This method receives two parameters within its body.

### POST 

+ Parameters

    + token (required,string,`asdasdasdqdasdasd`) ... The actual token to be revoked.
    + token_type_hint (required,string ,`access_token`) ... The type of token to be revoked. If `refresh_token` is specified, then only the refresh token is revoked. If `access_token` is specified then both the `access_token` and its associated `refresh_token` are revoked.
        + Values
            + `access_token`
            + `refresh_token`

+ Request (application/x-www-form-urlencoded)

    + Headers

            Accept: application/json

    + Body

            token_type_hint={token_type_hint}&token={token}

+ Response 200 (application/json)

        {
            "message": "Access Token Revoked"
        }

## Token validation endpoint [/oauth/v2/idtoken/validate]
Validate a token generated with TigoID. Verify token checks for a valid signature and if token hasn't expired yet.

### POST 

+ Parameters

    + id_token (required,string,`asdasdasdqdasdasd`) ... The actual token to be validated.
    
+ Request (application/x-www-form-urlencoded)

    + Headers

            apikey: someapikey

    + Body

            id_token={id_token}

+ Response 200 (application/json)

        {
            "isValid": true
        }


##Logout options [/openid/logout]

New logout options in Tigo ID 

### Normal [GET]
This will respond with the login page for tigo id after having deleted the active session.

+ Response 200 (application/html)
    <html></html>

### JSON  [GET]

This will return the payload as JSON. NOT WORKING CURRENTLY

+ Request (application/json)

    + Headers

            Accept: application/json


+ Response 200 (application/json)



### Redirect [GET]

Will logout and redirect to {post_logout_redirect_uri}. id_token_hint is currently mandatory but will be made optional.
When logging out the access token should be invalidated, and the `post_logout_redirect_uri` MUST invalidate the useragent session if it is still active.

+ Parameters
    + post_logout_redirect_uri
    + id_token_hint 
    + state
    
+ Response 302 ()
    + Headers
        Location: redirect_uri

        
# Group Social login considerations

If working from an embedded browser, you can add to the authorization flow a parameter called `auth_flow` and set the vaue to 'redirect' in order to get the gigya social flow to NOT use popups.


# Refresh Token Endpoint

## Obtain refresh_token [/oauth/v2/accesstoken]
The Refresh token endpoint allows the Application to get a new `id_token` and `access_token` in exchange from a valid `refresh_token`.

### POST

+ Request (application/x-www-form-urlencoded)

    + Headers

            Authorization: Basic Base64({client_id}:{client_secret})

    + Body

            grant_type=refresh_token&refresh_token={refresh_token}&redirect_uri={redirect_uri}

+ Response 200 (application/json)

        {
            "access_token": "6dgcyB7Z30w5XCAOSa75oRT4N2zO",
            "token_type": "Bearer",
            "refresh_token": "1hJ6YGvK9epTDCJBQImY0NAJFg2B4HjJ",
            "expires_in": "3599",
            "id_token": "eyJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbWljLXRlc3QuYXBpZ2VlLm5ldCIsImF1ZCI6Imh6YWxTWkpXZUc2V0tjM0NXVFQzTWl5bGNyQXFzTHFIIiwic3ViIjoiMzNjMDgyNmEtNDgyZC0xMWU0LWI1MzQtNzNjZDVmYTVkNzRkIiwiaWF0IjoxNDEyMTM3Mjg3LCJleHAiOjE0MTIxMzczNDcsImF1dGhfdGltZSI6MTQxMjEzNzI4NywibmFtZSI6IlJvYmVydG8iLCJlbWFpbCI6InJjbmF2YXNAZ21haWwuY29tIiwiZW1haWxfdmVyaWZpZWQiOiJ0cnVlIiwicGhvbmUiOiI1MDM3ODgzMjAxMCIsInBob25lX3ZlcmlmaWVkIjoidHJ1ZSIsInRpZ29fY3VzdG9tZXJJZCI6IiIsInRpZ29fY29udHJhY3ROdW1iZXIiOiIiLCJhdF9oYXNoIjoiSm1YNjY4czF2cm1ZajNvckV6YmJoQVx1MDAzZFx1MDAzZCIsIm5vbmNlIjoiODM0NzEwZGMtMmFiNC1lOGQ5LTVmNjgtNTQzZDU1NzU3Njk5In0.qnknWdJy1MLh53Hq1PSWSttyOOEqOhvRN0CTrnEUsPg"
        }

# Group MFSID considerations

The use of MFSID is only accessible if federated from Tigo ID, this means tha the only requirement to use mfsid is using tigo id.
You only need to include the proper scopes. You will be issued a token the same way as with tigo id, this token contains the context required to call the MFS APIS.

MFSID is a separate Api from Tigo ID, although it is very similar to the difference that it can not verify emails or phone number, limiting only to see the MSISDN and the corresponding pin to communicate with the backend of each country.MFSID presents a screen where the user is requested to enter the pin to verify its authenticity. If everything is in order, it loads the views where it shows the options to perform, such as making a transfer from one number to another, this in turn generates a token which allows the call to the backend of MFS services where the operation that validates that the client has already accepted the operation is executed.

# Trusted apps

Apps that are within the MFS security domain can have special access given to them so that they may present a native UI to request the PIN.
This mechanism enables the apps to upgrade their token from lower scope ( which MUST do the federated login as described above) with the mfsid read scope.

# Token escalate

A level of Tigo ID API is recognized by the scope of the "mfsid" prefix where the msisdn is required, Tigo ID takes the cell phone number and verifies it by sea through the header or by sending the time password code with the information, with this information Tigo ID has been redirected to the MFSID server where the screens with an appearance very similar to that of TigoID are displayed, these screens can be made with the corresponding authorization address once the operation is completed it is redirected to TigoID and Notifies about the final status of the transaction.
 
## Escalate access_token [/tigoid/v2/money/escalate]
The escalate token endpoint allows the Application to upgrade the `access_token` to more scopes without having to do a reauth flow. It has to present the native UI for a pin entry and then use that entry to calculate a HMAC signature

* The APP obtains its access token.
* The APP uses its access token for basic operations. At some point, the APP may need additional one-time consents like for example: Transfer X amount of money.
* Non trusted APPs require a new access token each time, and each time specify the amount of money to transfer.
* Trusted APPs may ask the user for its PIN once per session and use it to request additional consents directly to MFS by providing a request signed with the pin.


### POST

+ Request (application/json )

    + Headers

            Authorization: Bearer oldbearertoken

    + Body

        {
            request:{
                "scope": "", // requested new scope 
                "mfsid": "", // mfsid targeted
                "mfs_params":{// params required by the new scope, if any
            },
            "timestamp": 0,// UTC timestamp, in milliseconds since UNIX Epoch
            "signature": "" // signature of request
        }

+ Response 200 (application/json)

        {
            "access_token": "6dgcyB7Z30w5XCAOSa75oRT4N2zO",
            "token_type": "Bearer",
            "refresh_token": "1hJ6YGvK9epTDCJBQImY0NAJFg2B4HjJ",
            "expires_in": "3599",
            "id_token": "eyJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbWljLXRlc3QuYXBpZ2VlLm5ldCIsImF1ZCI6Imh6YWxTWkpXZUc2V0tjM0NXVFQzTWl5bGNyQXFzTHFIIiwic3ViIjoiMzNjMDgyNmEtNDgyZC0xMWU0LWI1MzQtNzNjZDVmYTVkNzRkIiwiaWF0IjoxNDEyMTM3Mjg3LCJleHAiOjE0MTIxMzczNDcsImF1dGhfdGltZSI6MTQxMjEzNzI4NywibmFtZSI6IlJvYmVydG8iLCJlbWFpbCI6InJjbmF2YXNAZ21haWwuY29tIiwiZW1haWxfdmVyaWZpZWQiOiJ0cnVlIiwicGhvbmUiOiI1MDM3ODgzMjAxMCIsInBob25lX3ZlcmlmaWVkIjoidHJ1ZSIsInRpZ29fY3VzdG9tZXJJZCI6IiIsInRpZ29fY29udHJhY3ROdW1iZXIiOiIiLCJhdF9oYXNoIjoiSm1YNjY4czF2cm1ZajNvckV6YmJoQVx1MDAzZFx1MDAzZCIsIm5vbmNlIjoiODM0NzEwZGMtMmFiNC1lOGQ5LTVmNjgtNTQzZDU1NzU3Njk5In0.qnknWdJy1MLh53Hq1PSWSttyOOEqOhvRN0CTrnEUsPg"
        }
