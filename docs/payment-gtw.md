# Payment Gateway

## Journey

Enabler - Mobile + Home
audience: developers

## Description

Allow payments with Credit / Debit Cards
Fulfillment

## Goals and KPIs
- Credit Card Payments (#)
- Debit Card Payments (#)
- Tokenized Card (#)
- Accounts Paid


## Features
Payments
- Pay on Demand (no fulfilment)
- Pay + fulfillment
- Tokenization
- Pre Authorizations
- Use of html helpers
- Autopay

Fulfillment
- Pay Tigo Bills
- Top-up Tigo (recharge)
- Pay On Demand

Management
- Transactions and reconciliation Reports

## Basic architecture

```mermaid
graph TD

subgraph Presentation
    clientApp[Client Application]
    trxReports[Transactions and Reconciliation]
end

subgraph Digital Backend
    paygtw[Payment Gateway]
    backend[Apigee]
    clientApp-->paygtw
    paygtw-->backend
    trxReports-->paygtw
end

subgraph Country
    bss[Core BSS - OSB]
    mobile[Mobile]
    fixed[Fixed]
    backend-->bss
    bss-->fixed
    bss-->mobile
end
subgraph Mobile Domain
    fulfillment[fulfillment]
    cbs[invoices]
    mobile-->cbs
    mobile-->fulfillment
end

subgraph fixed Domain
    cbsFixed[invoices]
    fixed-->cbsFixed

end

```



## Implementation Details


