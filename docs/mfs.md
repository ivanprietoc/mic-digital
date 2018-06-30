
# MFS App

**Journey**

Journey: Transactional - Mobile
Audience: B2C transactional customers with MFS wallet

**Description**



**Goals and KPIs**
- active users
- transactors

## Features
- Discovery
    - Banner
    - Push notifications
    - Product catalog
- Use & Self-service
    - Buy Pack
        - core balance
        - mfs
    - Loans
        - current debt & credit limit
        - loan balance
        - loan packs
    - Top-up
        - credit card
        - mfs
    - See Balances
    - See Quota
    - Manage subscriptions
    - Internet details
- Care & Recommendation
    - NPS
    - Help
        - chat
        - faq

Banners
Feature products
Product Catalog
Top-up Self/Others
Bill Payments
Remesas Internacionales
Send/Request Money
Puntos Tigo Money
Cambio de Pin
History of transactions
Registration
Authorize transactions
Link/Unlink Bank Account
Recharge Self/Others
Pay Tigo/Non Tigo Bills
Send/Request Money
Cash in with
MoneyGram and Wester Union
Cash in with Bank Acct



## Basic architecture

```mermaid
graph TD

subgraph Channel
    android[Android]
    web[web]
    appbackend[App Backend]
    fapi[API Proxy]
    android---appbackend
    web---appbackend
    appbackend---fapi
end

subgraph Digital Backend
    backend[Apigee]
    fapi---backend

    segment
    payment_gateway
    tigoid
    contentful
end

subgraph Country
    bss[Core BSS - OSB]
    mobile[Mobile]
    bss---mobile
    backend---bss
end

subgraph Mobile Domain
    customer[customer]
    mfs[mfs]
    mobile---customer
end

```

## Implementation Details

### Authentication
- tigo id
    - TigoID Public

### Exposure layer
- apigee


### Engines / Enablers
- evam
    - lifecycle campaigns
    - broadcast
    - upselling (exacaster)
- zendesk

### Marketing tools
- digital turbine
- push notifications
    - pushwoosh
- kannel
- yourls
- attribution tools
    - tune
    - appflyer

### Repositories
- S3

### Other tools
- segment

- new relic
- tableau
    - dashboard tigo shop
    - active users
- analytics
    - mixpanel
    - google analytics
    - facebook analytics

## SOUTH ARCHITECTURE (COUNTRY)

