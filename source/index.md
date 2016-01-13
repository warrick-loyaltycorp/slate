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
    -d merchant='{"name":"Dr. Keyshawn Cruickshank IV","email":"Elmer25@Kuhn.biz","address":"0060 Jaylan Pine Apt. 094\nEast Lori, NV 71135","credit_cards":[{"number":"5142451063431350","expiry_date":"12\/17","cvv":856}],"bank_accounts":[{"name":"Louvenia Morar","number":212192,"branch":616398}]}'
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
    "message":"Merchant created",
    "merchant":
    {
        "name":"Dr. Keyshawn Cruickshank IV",
        "email":"Elmer25@Kuhn.biz",
        "address":"0060 Jaylan Pine Apt. 094\nEast Lori, NV 71135",
        "credit_cards":
        [
            {
                "token":"4817230923470352",
                "creditCardInfo":
                {
                    "pan":"514245XXXXXXX350",
                    "expiryDate":"12\/17",
                    "cardType":"5",
                    "cardDescription":"Master Card"
                }
            }
        ],
        "bank_accounts":
        [
            {
                "name":"Louvenia Morar",
                "number":212192,
                "branch":616398
            }
        ],
        "id":"mer_TICtkVBH2HMhaaS5",
        "secret_key":"sk_UHEtfvVqwiAUQeaEnqzFrMT5",
        "public_key":"pk_4PNIUIwbMOrQvF91oVPFIQFR"
    }
}
```

Create a new merchant.

This call returns the new merchant record, including:

1. The API Keys for this merchant.
2. The merchant unique ID. Use the unique ID to retrieve the merchant.
3. A token and PAN for each credit card. The token and PAN replace the credit card number.

### HTTP Request

`POST /merchants`

## Update a Merchant

```shell
curl /merchants/cus_P3thMWG1tRvdfING \
    -u sk_test_QyeTXFXrvKd0I7sGObQGY6mi: \
    -X PUT \
    -d merchant='{"name":"Maida Schaefer","email":"sMorar@yahoo.com","address":"33543 Connelly Prairie\nDouglasbury, MA 58663","credit_cards":[{"token":"3802789002339201","creditCardInfo":{"pan":"547025XXXXXXX413","expiryDate":"08\/20","cardType":"5","cardDescription":"Master Card"}}],"bank_accounts":[{"name":"Prof. Franco Wunsch II","number":457888,"branch":465377}],"id":"mer_2zeySm9fP4WKssSX","secret_key":"sk_cOJPAMZGPmJgkjUpwX3Kspz4","public_key":"pk_ydrJTGR600yCBgM89QUy3rSY"}' 
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
    "message":"Merchant updated",
    "merchant":
    {
        "name":"Maida Schaefer",
        "email":"sMorar@yahoo.com",
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
        "id":"mer_2zeySm9fP4WKssSX",
        "secret_key":"sk_cOJPAMZGPmJgkjUpwX3Kspz4",
        "public_key":"pk_ydrJTGR600yCBgM89QUy3rSY"
    }
}
```

Update a merchant with new details.

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
[
    {
        "name":"Dr. Keyshawn Cruickshank IV",
        "email":"Elmer25@Kuhn.biz",
        "address":"0060 Jaylan Pine Apt. 094\nEast Lori, NV 71135",
        "credit_cards":
        [
            {
                "token":"4817230923470352",
                "creditCardInfo":
                {
                    "pan":"514245XXXXXXX350",
                    "expiryDate":"12\/17",
                    "cardType":"5",
                    "cardDescription":"Master Card"
                }
            }
        ],
        "bank_accounts":
        [
            {
                "name":"Louvenia Morar",
                "number":212192,
                "branch":616398
            }
        ],
        "id":"mer_TICtkVBH2HMhaaS5"
    },
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
]
```

Get a list of all merchants.

### HTTP Request

`GET /merchants`

# Customers 

## Create a Customer

```shell
curl /customers \
    -u sk_test_QyeTXFXrvKd0I7sGObQGY6mi: \
    -X POST \
    -d customer='{"name":"Skyla Bins Sr.","email":"Holly82@hotmail.com","address":"94034 Mireya Knolls Suite 124\nEast Liliana, OR 93969","credit_cards":[{"number":"5559039016093199","expiry_date":"05\/19","cvv":602}],"bank_accounts":[{"name":"Dorothea Walker","number":128818,"branch":632605}]}'
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
    "message":"Customer created",
    "customer":
    {
        "name":"Skyla Bins Sr.",
        "email":"Holly82@hotmail.com",
        "address":"94034 Mireya Knolls Suite 124\nEast Liliana, OR 93969",
        "credit_cards":
        [
            {
                "token":"8846051300564567",
                "creditCardInfo":
                {
                    "pan":"555903XXXXXXX199",
                    "expiryDate":"05\/19",
                    "cardType":"5",
                    "cardDescription":"Master Card"
                }
            }
        ],
        "bank_accounts":
        [
            {
                "name":"Dorothea Walker",
                "number":128818,
                "branch":632605
            }
        ],
        "id":"cus_u4enomYPXItBeEP2"
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
curl /customers/cus_P3thMWG1tRvdfING \
    -u sk_test_QyeTXFXrvKd0I7sGObQGY6mi: \
    -X PUT \
    -d customer='{"name":"Gianni Orn MD","email":"Shayna.Yundt@gmail.com","address":"7901 Gavin Extensions\nDurganside, NM 42294","credit_cards":[{"token":"1533969065430","creditCardInfo":{"pan":"453298XXXX693","expiryDate":"01\/20","cardType":"6","cardDescription":"Visa"}}],"bank_accounts":[{"name":"Alvena Von DDS","number":909844,"branch":634292}]}' 
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
    "message":"Customer updated",
    "customer":
    {
        "name":"Gianni Orn MD",
        "email":"Shayna.Yundt@gmail.com",
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
[
    {
        "name":"Ms. Kayli Donnelly",
        "email":"Brenda.Leuschke@yahoo.com",
        "address":"561 Marcelo Field\nWest Guadalupe, UT 44365-1757",
        "credit_cards":
        [
            {
                "token":"8554872018151104",
                "creditCardInfo":
                {
                    "pan":"492933XXXXXXX138",
                    "expiryDate":"06\/16",
                    "cardType":"6",
                    "cardDescription":"Visa"
                }
            }
        ],
        "bank_accounts":
        [
            {
                "name":"Prof. Wilmer Champlin MD",
                "number":119490,
                "branch":987275
            }
        ],
        "id":"cus_89d0d316f6786debcc30adabbe675b05"
    },
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
]
```

Get a list of all customers.

### HTTP Request

`GET /customers`

# Payments 

## Create a Payment

```shell
curl /payments \
    -u sk_test_QyeTXFXrvKd0I7sGObQGY6mi: \
    -X POST 
    -d payment='{"token":"1479093065260287","reference":"Officia similique quaerat et eaque quo.","amount":74200,"currency":"AUD"}' 
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
    "message":"Payment created",
    "txnID":"273040",
    "payment":{
        "token":"1479093065260287",
        "reference":"Officia similique quaerat et eaque quo.",
        "amount":74200,
        "currency":"AUD",
        "txnID":"273040"
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
curl /payments/273040 \
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
    "message":"Payment refunded",
    "txnID":"273042",
    "refund":
    {
        "amount":74200,
        "currency":"AUD",
        "purchaseOrderNo":"Officia similique quaerat et eaque quo.",
        "txnID":"273042"
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
    -d fee='{"transactionFee":0.3,"cardRates":{"MasterCard":1.5,"Visa":1.5,"AMEX":2.9}}' \
    -X PUT 
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

### HTTP Request

`PUT /fees/<payment type>`

### URL Parameters

Parameter | Description
--------- | -----------
payment type | The payment type to set a fee structure for.

## Set fees for a specific merchant

```shell
curl /fees/cc_payment/mer_Jz1jhip325eRwhWy \
    -u sk_test_QyeTXFXrvKd0I7sGObQGY6mi: \
    -d fee='{"transactionFee":0.4,"cardRates":{"MasterCard":1.8,"Visa":1.9,"AMEX":3.2}}' \
    -X PUT 
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

Set a fee structure for a specific payment type and merchant.

The merchant fee structure overrides the general fee structure.

See [Set general fees](#set-general-fees) for a list of valid payment types.

### HTTP Request

`PUT /fees/<payment type>/<merchant id>`

### URL Parameters

Parameter | Description
--------- | -----------
payment type | The payment type to set a fee structure for.
merchant id | The merchant to set a fee structure for.

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

### HTTP Request

`GET /fees/<payment type>`

### URL Parameters

Parameter | Description
--------- | -----------
payment type | The payment type to set a fee structure for.

## Get merchant fees

```shell
curl /fees/cc_payment/mer_Jz1jhip325eRwhWy \
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

Get the fee structure for a payment type and merchant.

See [Set general fees](#set-general-fees) for a list of valid payment types.

### HTTP Request

`GET /fees/<payment type>/<merchant id>`

### URL Parameters

Parameter | Description
--------- | -----------
payment type | The payment type to set a fee structure for.
merchant id | The merchant to set a fee structure for.

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

### HTTP Request

`DELETE /fees/<payment type>`

### URL Parameters

Parameter | Description
--------- | -----------
payment type | The payment type to delete a fee structure for.

## Delete merchant fees

```shell
curl /fees/cc_payment/mer_Jz1jhip325eRwhWy \
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

Delete the fee structure for a payment type and merchant.

See [Set general fees](#set-general-fees) for a list of valid payment types.

### HTTP Request

`DELETE /fees/<payment type>/<merchant id>`

### URL Parameters

Parameter | Description
--------- | -----------
payment type | The payment type to delete a fee structure for.
merchant id | The merchant to delete a fee structure for.
