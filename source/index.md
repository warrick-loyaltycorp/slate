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
curl "api_endpoint_here"
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
curl -X POST /apikeys
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
curl -X GET /apikeys/<APIKey>
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
    "api_key":"pk_test_zgo5VQTGem75o0PDcphyqtSx",
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
curl -X DELETE /apikeys/<APIKey>
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

`GET /apikeys/<APIKey>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The API key to retrieve details for

# Customers 

## Create a Customer

```shell
curl -X POST -d '{"name":"Gianni Orn MD","email":"Halie.Stroman@gmail.com","address":"7901 Gavin Extensions\nDurganside, NM 42294","credit_cards":[{"token":"1533969065430","creditCardInfo":{"pan":"453298XXXX693","expiryDate":"01\/20","cardType":"6","cardDescription":"Visa"}}],"bank_accounts":[{"name":"Alvena Von DDS","number":909844,"branch":634292}]}' /customers
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
}
```

Create a new customer.

The new customer record, including the unique ID,  is returned in the response.

### HTTP Request

`POST /customers`

## Update a Customer

```shell
curl -X PUT -d '{"name":"Gianni Orn MD","email":"Shayna.Yundt@gmail.com","address":"7901 Gavin Extensions\nDurganside, NM 42294","credit_cards":[{"token":"1533969065430","creditCardInfo":{"pan":"453298XXXX693","expiryDate":"01\/20","cardType":"6","cardDescription":"Visa"}}],"bank_accounts":[{"name":"Alvena Von DDS","number":909844,"branch":634292}]}' /customers/cus_P3thMWG1tRvdfING
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
curl -X DELETE /customers/cus_P3thMWG1tRvdfING
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
curl -X GET /customers/cus_P3thMWG1tRvdfING
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
curl -X GET /customers
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
curl -X POST -d '{"token":"5083312354487131","reference":"Voluptas in quo dolor commodi repellendus.","amount":946900,"currency":"AUD"}' /payments
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
    "payment":
    {
        "token":"5083312354487131",
        "reference":"Voluptas in quo dolor commodi repellendus.",
        "amount":946900,
        "currency":"AUD"
    }
}
```

Create a new payment.

The token identifies the credit card to be used for this payments. The token is returned when creating a new customer.

### HTTP Request

`POST /payments`

