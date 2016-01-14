---
title: EoneoPay API Reference

language_tabs:
  - shell: cURL
  - PHP
  - Java
  - Ruby
  - Python
  - Node

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

The EoneoPay API is organized around REST. Our API has predictable, resource-oriented URLs, and uses HTTP response codes to indicate API errors. We use built-in HTTP features, like HTTP authentication and HTTP verbs, which are understood by off-the-shelf HTTP clients. We support cross-origin resource sharing, allowing you to interact securely with our API from a client-side web application (though you should never expose your secret API key in any public website's client-side code). JSON is returned by all API responses, including errors, although our API libraries convert responses to appropriate language-specific objects.

To make the API as explorable as possible, accounts have test mode and live mode API keys. There is no "switch" for changing between modes, just use the appropriate key to perform a live or test transaction. Requests made with test mode credentials never hit the banking networks and incur no cost.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -u your_api_key:
```

```PHP
```

```Java
```

```Ruby
```

```Python
```

```Node
```

Authenticate your account when using the API by including your secret API key in the request. You can manage your API keys in the Dashboard. Your API keys carry many privileges, so be sure to keep them secret! Do not share your secret API keys in publicly accessible areas such GitHub, client-side code, and so forth.

All API requests must be made over HTTPS. Calls made over plain HTTP will fail. API requests without authentication will also fail.

# API Keys 

All calls to the EoneoPay Payment Gateway are authenticated using API Keys.

New API Keys are issued when a [merchant is created](#create-a-merchant). 

API Keys are revocable. An admin key is required to retrieve and revoke API Keys.

## Get API Key details

```shell
curl /apikeys/sk_test_Km2opmRbESoA32r36BlE24xm \
    -u sk_test_QyeTXFXrvKd0I7sGObQGY6mi: \
    -X GET

```

```PHP
```

```Java
```

```Ruby
```

```Python
```

```Node
```

> The above command returns JSON structured like this:

```json
{
    "api_key":"sk_test_Km2opmRbESoA32r36BlE24xm",
    "permissions":"+",
    "status":"1"
}
```

Retrieve all details for a specific API key.

<aside class="warning">An administrator API key is required to manage API keys</aside>

### HTTP Request

`GET /apikeys/<APIKey>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The API key to  revoke

## Revoke an API Key

```shell
curl /apikeys/sk_test_Km2opmRbESoA32r36BlE24xm
    -u sk_test_QyeTXFXrvKd0I7sGObQGY6mi: \
    -X DELETE 
```

```PHP
```

```Java
```

```Ruby
```

```Python
```

```Node
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"API Key revoked"
}
```

Revoke an API Key. Once revoked an API key can no longer be used to make API calls.

<aside class="warning">An administrator API key is required to manage API keys</aside>

### HTTP Request

`DELETE /apikeys/<APIKey>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The API key to retrieve details for

# Merchants 

## Create a Merchant

```shell
curl /merchants \
    -u sk_test_QyeTXFXrvKd0I7sGObQGY6mi: \
    -X POST \
    -d "title=Prof." \
    -d "first_name=Lenora" \
    -d "last_name=Rogahn" \
    -d "email=Buster.Schinner@Hammes.com" \
    -d "business_name=Sawayn-Stroman" \
    -d "business_phone=1-131-325-2208x67174" \
    -d "business_website=http://Rempel.org" \
    -d "abn=32370078770" \
    -d "bank_accounts[0][name]=Mrs. Hertha Brakus" \
    -d "bank_accounts[0][bsb]=495233" \
    -d "bank_accounts[0][number]=765298" \
    -d "credit_cards[0][number]=5307977191019924" \
    -d "credit_cards[0][expiry_month]=06" \
    -d "credit_cards[0][expiry_year]=18" \                    
    -d "credit_cards[0][cvc]=728" \
    -d "credit_cards[0][name]=Katrina O'Kon" \
    -d "credit_cards[0][address_line1]=15772 Broderick Falls" \
    -d "credit_cards[0][address_line2]=" \
    -d "credit_cards[0][address_city]=Erinbury" \
    -d "credit_cards[0][address_postcode]=2195" \
    -d "credit_cards[0][address_state]=NSW" \
    -d "credit_cards[0][address_country]=Australia"
```

```PHP
```

```Java
```

```Ruby
```

```Python
```

```Node
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"Merchant created.",
    "merchant":
    {
        "title":"Prof.",
        "first_name":"Lenora",
        "last_name":"Rogahn",
        "email":"Buster.Schinner@Hammes.com",
        "business_name":"Sawayn-Stroman",
        "business_phone":"1-131-325-2208x67174",
        "business_website":"http:\/\/Rempel.org",
        "abn":32370078770,
        "bank_accounts": [
        {
            "name":"Mrs. Hertha Brakus",
            "bsb":495233,
            "number":765298
        }],
        "credit_cards":[
        {
            "token":"2717742183536883",
            "creditCardInfo":
            {
                "pan":"530797XXXXXXX924",
                "expiryDate":"06\/18",
                "cardType":"5",
                "cardDescription":"Master Card"
            }
        }],
        "id":"mer_ckcBTeNgqstddBe3",
        "secret_key":"sk_llg2kVYIEh2NTf5f2rG49pZH",
        "public_key":"pk_08LxV74zWu2mPFQC8iLc0ATq"
    }
}
```

Create a new merchant.

This call returns the new merchant record, including:

1. The API Keys for this merchant.
2. The merchant unique ID. Use the unique ID to retrieve the merchant.
3. A token and PAN for each credit card. The token and PAN replace the credit card number.

<aside class="warning">An administrator API key is required to manage API keys</aside>

### HTTP Request

`POST /merchants`

## Update a Merchant

```shell
curl /merchants/mer_xtmKq3i0MRMGDg2H \
    -u sk_test_QyeTXFXrvKd0I7sGObQGY6mi: \
    -X PUT \
    -d "email=aGoodwin@hotmail.com"
```

```PHP
```

```Java
```

```Ruby
```

```Python
```

```Node
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"Merchant updated.",
    "merchant":
    {
        "title":"Mr.",
        "first_name":"Jordy",
        "last_name":"Miller",
        "email":"aGoodwin@hotmail.com",
        "business_name":"Kirlin LLC",
        "business_phone":"193.548.2607x9102",
        "business_website":"http:\/\/Yundt.biz",
        "abn":54684559752,
        "bank_accounts":[
        {
            "name":"Abdullah Gutkowski",
            "bsb":454173,
            "number":197814
        }],
        "credit_cards":[
        {
            "token":"2745595004221945",
            "creditCardInfo":
            {
                "pan":"402400XXXXXXX658",
                "expiryDate":"09\/20",
                "cardType":"6",
                "cardDescription":"Visa"
            }
        }],
        "id":"mer_xtmKq3i0MRMGDg2H"
    }
}
```

Update a merchant with new details.

<aside class="warning">An administrator API key is required to manage API keys</aside>

### HTTP Request

`PUT /merchants/<merchant ID>`

### URL Parameters

Parameter | Description
--------- | -----------
merchant ID | The ID of the merchant to update

## Delete a Merchant

```shell
curl /merchants/mer_2zeySm9fP4WKssSX \
    -u sk_test_QyeTXFXrvKd0I7sGObQGY6mi: \
    -X DELETE 
```

```PHP
```

```Java
```

```Ruby
```

```Python
```

```Node
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"Merchant deleted"
}
```

Delete a merchant record.

<aside class="warning">An administrator API key is required to manage API keys</aside>

### HTTP Request

`DELETE /merchants/<merchant ID>`

### URL Parameters

Parameter | Description
--------- | -----------
merchant ID | The ID of the merchant to delete

## Get a Merchant

```shell
curl /merchants/mer_2zeySm9fP4WKssSX \
    -u sk_test_QyeTXFXrvKd0I7sGObQGY6mi: \
    -X GET 
```

```PHP
```

```Java
```

```Ruby
```

```Python
```

```Node
```

> The above command returns JSON structured like this:

```json
{
    "name":"Maida Schaefer",
    "email":"Geovany.Barrows@Hirthe.com",
    "address":"33543 Connelly Prairie\nDouglasbury, MA 58663",
    "credit_cards":
    [
        {
            "token":"3802789002339201",
            "creditCardInfo":
            {
                "pan":"547025XXXXXXX413",
                "expiryDate":"08\/20",
                "cardType":"5",
                "cardDescription":"Master Card"
            }
        }
    ],
    "bank_accounts":
    [
        {
            "name":"Prof. Franco Wunsch II",
            "number":457888,
            "branch":465377
        }
    ],
    "id":"mer_2zeySm9fP4WKssSX"
}
```

Retrieve details for a merchant.

<aside class="warning">An administrator API key is required to manage API keys</aside>

### HTTP Request

`GET /merchants/<merchant ID>`

### URL Parameters

Parameter | Description
--------- | -----------
merchant ID | The ID of the merchant to retrieve

## Get a list of all Merchants

```shell
curl /merchants \
    -u sk_test_QyeTXFXrvKd0I7sGObQGY6mi: \
    -X GET \
    -d "page_key=mer_OjHXobBsSHsGTXvU"
```

```PHP
```

```Java
```

```Ruby
```

```Python
```

```Node
```

> The above command returns JSON structured like this:

```json
{
    "list":[
    {
        "title":"Mr.",
        "first_name":"Jasen",
        "last_name":"Bergstrom",
        "email":"pSawayn@yahoo.com",
        "business_name":"Schiller, Schaden and Pagac",
        "business_phone":"1-567-963-4476x877",
        "business_website":"http:\/\/Runolfsdottir.com",
        "abn":87708222866,
        "bank_accounts":[
        {
            "name":"Mrs. Nikita Harber",
            "bsb":561105,
            "number":696777
        }],
        "credit_cards":[
        {
            "token":"459023068852943",
            "creditCardInfo":
            {
                "pan":"343580XXXXXX868",
                "expiryDate":"11\/17",
                "cardType":"2",
                "cardDescription":"American Express"
            }
        }],
        "id":"mer_mjrPtIYIFUz29IB2"
    },
    {
        "title":"Prof.",
        "first_name":"Ines",
        "last_name":"Gaylord",
        "email":"Cummings.Rodger@gmail.com",
        "business_name":"Glover-Bruen",
        "business_phone":"(233)321-7307x23950",
        "business_website":"http:\/\/Langosh.com",
        "abn":32929909684,"bank_accounts":[
        {
            "name":"Ms. Adah Hoppe Sr.",
            "bsb":925800,
            "number":661430
        }],
        "credit_cards":[
        {
            "token":"8275016079732",
            "creditCardInfo":
            {
                "pan":"448594XXXX381",
                "expiryDate":"12\/17",
                "cardType":"6",
                "cardDescription":"Visa"
            }
        }],
        "id":"mer_t99ZVJsmaSMdFmaw"
    }],
    "page_key":"mer_x8Yrg15AyBqQWk5a"
}
```

Get a paginated list of all merchants.

At most twenty five merchants are returned per call. If more merchants are available the response includes a *page_key* which can be sent in a subsquent request to fetch the next page.

<aside class="warning">An administrator API key is required to manage API keys</aside>

### HTTP Request

`GET /merchants`

# Customers 

## Create a Customer

```shell
curl /customers \
    -u sk_llg2kVYIEh2NTf5f2rG49pZH: \
    -X POST \
    -d "email=iJohnson@yahoo.com
    -d "credit_cards[0][number]=4024007140948844" \
    -d "credit_cards[0][expiry_month]=04" \
    -d "credit_cards[0][expiry_year=17" \
    -d "credit_cards[0][cvc=506" \
    -d "credit_cards[0][name=Luna Stamm" \
    -d "credit_cards[0][address_line1=53326 Goyette Roads" \
    -d "credit_cards[0][address_line2=" \
    -d "credit_cards[0][address_city=Estellville" \
    -d "credit_cards[0][address_postcode=3804" \
    -d "credit_cards[0][address_state=SA" \
    -d "credit_cards[0][address_country=Australia" \
    -d "bank_accounts[0][name]=Immanuel Maggio" \
    -d "bank_accounts[0][bsb]=931958" \
    -d "bank_accounts[0][number]=137367"
```

```PHP
```

```Java
```

```Ruby
```

```Python
```

```Node
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"Customer created.",
    "customer":
    {
        "email":"iJohnson@yahoo.com",
        "credit_cards":[
        {
            "token":"6082824513618512",
            "creditCardInfo":
            {
                "pan":"402400XXXXXXX844",
                "expiryDate":"04\/17",
                "cardType":"6",
                "cardDescription":"Visa"
            }
        }],
        "bank_accounts":[
        {
            "name":"Immanuel Maggio",
            "bsb":931958,
            "number":137367
        }],
        "id":"cus_e44VrNXhj9MFNNfO"
    }
}
```

Create a new customer.

This call returns the new customer record, including:
1. The customer unique ID. Use the unique ID to retrieve the customer
2. A token and PAN for each credit card. The token and PAN replace the credit card number.

### HTTP Request

`POST /customers`

## Update a Customer

```shell
curl /customers/cus_e44VrNXhj9MFNNfO \
    -u sk_llg2kVYIEh2NTf5f2rG49pZH: \
    -X PUT \
    -d "email=Blanda.Sofia@hotmail.com"
```

```PHP
```

```Java
```

```Ruby
```

```Python
```

```Node
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"Customer updated.",
    "customer":
    {
        "email":"Blanda.Sofia@hotmail.com",
        "credit_cards":[
        {
            "token":"6082824513618512",
            "creditCardInfo":
            {
                "pan":"402400XXXXXXX844",
                "expiryDate":"04\/17",
                "cardType":"6",
                "cardDescription":"Visa"
            }
        }],
        "bank_accounts":[
        {
            "name":"Immanuel Maggio",
            "bsb":931958,
            "number":137367
        }],
        "id":"cus_e44VrNXhj9MFNNfO"
    }
}
```

Update a customer with new details.

### HTTP Request

`PUT /customers/<customer ID>`

### URL Parameters

Parameter | Description
--------- | -----------
customer ID | The ID of the customer to retrieve

## Delete a Customer

```shell
curl /customers/cus_P3thMWG1tRvdfING \
    -u sk_llg2kVYIEh2NTf5f2rG49pZH: \
    -X DELETE 
```

```PHP
```

```Java
```

```Ruby
```

```Python
```

```Node
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"Customer deleted"
}
```

Delete a customer record.

### HTTP Request

`DELETE /customers/<customer ID>`

### URL Parameters

Parameter | Description
--------- | -----------
customer ID | The ID of the customer to retrieve

## Get a Customer

```shell
curl /customers/cus_P3thMWG1tRvdfING \
    -u sk_llg2kVYIEh2NTf5f2rG49pZH: \
    -X GET 
```

```PHP
```

```Java
```

```Ruby
```

```Python
```

```Node
```

> The above command returns JSON structured like this:

```json
{
    "name":"Gianni Orn MD",
    "email":"Halie.Stroman@gmail.com",
    "address":"7901 Gavin Extensions\nDurganside, NM 42294",
    "credit_cards":
    [
        {
            "token":"1533969065430",
            "creditCardInfo":
            {
                "pan":"453298XXXX693",
                "expiryDate":"01\/20",
                "cardType":"6",
                "cardDescription":"Visa"
            }
        }
    ],
    "bank_accounts":
    [
        {
            "name":"Alvena Von DDS",
            "number":909844,
            "branch":634292
        }
    ],
    "id":"cus_P3thMWG1tRvdfING"
}
```

Retrieve details for a customer.

### HTTP Request

`GET /customers/<customer ID>`

### URL Parameters

Parameter | Description
--------- | -----------
customer ID | The ID of the customer to retrieve

## Get a list of all Customers

```shell
curl /customers \
    -u sk_llg2kVYIEh2NTf5f2rG49pZH: \
    -X GET \
    -d "page_key=cus_PtMsPVGfgMa0QrXv"
```

```PHP
```

```Java
```

```Ruby
```

```Python
```

```Node
```

> The above command returns JSON structured like this:

```json
{
    "list":[
    {
        "email":"Gino34@Kertzmann.com",
        "credit_cards":[
        {
            "token":"8442679958731",
            "creditCardInfo":
            {
                "pan":"492931XXXX714",
                "expiryDate":"12\/19",
                "cardType":"6",
                "cardDescription":"Visa"
            }
        }],
        "bank_accounts":[
        {
            "name":"Brandyn Swaniawski",
            "bsb":479540,
            "number":120379
        }],
        "id":"cus_5UCb9sCEJmUqB7A9"
    },
    {
        "email":"Champlin.Sandra@Aufderhar.biz",
        "credit_cards":[
        {
            "token":"7240403533051967",
            "creditCardInfo":
            {
                "pan":"453226XXXXXXX792",
                "expiryDate":"07\/21",
                "cardType":"6",
                "cardDescription":"Visa"
            }
        }],
        "bank_accounts":[
        {
            "name":"Ahmad Raynor",
            "bsb":855657,
            "number":469006
        }],
        "id":"cus_BEkJxCyy0ESU1SDR"
    }],
    "page_key":"cus_PtMsPVGfgMa0QrXv"
}
```

Get a paginated list of all customers.

At most twenty five customers will be returned per call. If more customers are available the response includes a *page_key* which can be used to fetch the next page.

### HTTP Request

`GET /customers`

# Payments 

## Create a Payment

```shell
curl /payments \
    -u sk_llg2kVYIEh2NTf5f2rG49pZH: \
    -X POST \
    -d "token=1726094106475018" \
    -d "reference=Vel qui aut tenetur corrupti vero cum itaque." \
    -d "amount=65700" \
    -d "currency=AUD"
```

```PHP
```

```Java
```

```Ruby
```

```Python
```

```Node
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"Payment created.",
    "txnID":"282163",
    "payment":
    {
        "token":"1726094106475018",
        "reference":"Vel qui aut tenetur corrupti vero cum itaque.",
        "amount":65700,
        "currency":"AUD",
        "txnID":"282163"
    }
}
```

Create a new payment.

The token identifies the credit card to be used for this payments. The token is returned when creating a new customer.

The response to a successful payment includes the *txnID* which must be used when processing refunds.

### HTTP Request

`POST /payments`

## Refund a Payment

```shell
curl /payments/282163 \
    -u sk_llg2kVYIEh2NTf5f2rG49pZH: \
    -X DELETE 
```

```PHP
```

```Java
```

```Ruby
```

```Python
```

```Node
```

> The above command returns JSON structured like this:

```json
{
    "code":"00",
    "message":"Payment refunded.",
    "txnID":"282165",
    "refund":
    {
        "amount":65700,
        "currency":"AUD",
        "purchaseOrderNo":"Vel qui aut tenetur corrupti vero cum itaque.",
        "txnID":"282165"
    }
}
```

Refund a payment.

The transaction ID returned by an earlier call to create a payment must be provided

### HTTP Request

`DELETE /payments/<txnID>`

### URL Parameters

Parameter | Description
--------- | -----------
txnID | The ID of the payment transaction to refund

# Fees

## Set general fees

```shell
curl /fees/cc_payment \
    -u sk_test_QyeTXFXrvKd0I7sGObQGY6mi: \
    -X PUT 
    -d "transactionFee=0.3" \
    -d "[cardRates][MasterCard]=1.5" \
    -d "[cardRates][Visa]=1.5" \
    -d "[cardRates][AMEX]=2.9"
```

```PHP
```

```Java
```

```Ruby
```

```Python
```

```Node
```

> The above command returns JSON structured like this:

```json
{"code":0,"message":"Fee created."}
```

Set a general fee structure for a specific payment type.

Payment type can be one of:

1. cc_payment - credit card payments
2. direct_debit - direct debit payments
3. bpay - BPAY payments
4. auspost - AUSPost payments
5. eft - allocated eft
6. cheque - cheque payments

<aside class="warning">An administrator API key is required to manage API keys</aside>

### HTTP Request

`PUT /fees/<payment type>`

### URL Parameters

Parameter | Description
--------- | -----------
payment type | The payment type to set a fee structure for.

## Get fees

```shell
curl /fees/cc_payment \
    -u sk_test_QyeTXFXrvKd0I7sGObQGY6mi: \
    -X GET 
```

```PHP
```

```Java
```

```Ruby
```

```Python
```

```Node
```

> The above command returns JSON structured like this:

```json
{
    "transactionFee":0.3,
    "cardRates":
    {
        "MasterCard":1.5,
        "Visa":1.5,
        "AMEX":2.9
    }
}
```

Get the fee structure for a payment type.

See [Set general fees](#set-general-fees) for a list of valid payment types.

<aside class="warning">An administrator API key is required to manage API keys</aside>

### HTTP Request

`GET /fees/<payment type>`

### URL Parameters

Parameter | Description
--------- | -----------
payment type | The payment type to set a fee structure for.

## Delete general fees

```shell
curl /fees/cc_payment \
    -u sk_test_QyeTXFXrvKd0I7sGObQGY6mi: \
    -X DELETE 
```

```PHP
```

```Java
```

```Ruby
```

```Python
```

```Node
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"Fee deleted."
}
```

Delete a general fee structure for a payment type.

See [Set general fees](#set-general-fees) for a list of valid payment types.

<aside class="warning">An administrator API key is required to manage API keys</aside>

### HTTP Request

`DELETE /fees/<payment type>`

### URL Parameters

Parameter | Description
--------- | -----------
payment type | The payment type to delete a fee structure for.

