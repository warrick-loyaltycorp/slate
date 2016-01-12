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

## Create an API Key

```shell
curl /apikeys \
    -u sk_test_QyeTXFXrvKd0I7sGObQGY6mi: \
    -X POST
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
    "test_secret_key": "sk_test_6qzkzasVKBYirSHtTHJASrmL",
    "test_public_key": "pk_test_zgo5VQTGem75o0PDcphyqtSx"
}
```

Create a new API Key.

<aside class="warning">An administrator API key is required to manage API keys</aside>

### HTTP Request

`POST /apikeys`

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

