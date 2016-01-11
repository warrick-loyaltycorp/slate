---
title: EoneoPay API Reference

language_tabs:
  - curl
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

```Ruby
```

```Python
```

```curl
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -u your_api_key:
```

```PHP
```

```Java
```

```Node
```

Authenticate your account when using the API by including your secret API key in the request. You can manage your API keys in the Dashboard. Your API keys carry many privileges, so be sure to keep them secret! Do not share your secret API keys in publicly accessible areas such GitHub, client-side code, and so forth.

All API requests must be made over HTTPS. Calls made over plain HTTP will fail. API requests without authentication will also fail.

# API Keys 

## Create an API Key

```curl
curl -X POST /apikeys
```

```python
```

```shell
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

```curl
curl -X GET /apikeys/<APIKey>
```

```python
```

```shell
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

```curl
curl -X DELETE /apikeys/<APIKey>
```

```python
```

```shell
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

```curl
curl -X POST -d '{"name":"Alexanne Russel","email":"kRuecker@Wintheiser.info","address":"40568 Feil Ferry\nGildafort, MO 50309","credit_cards":[{"number":"6011400661639209","expiry_date":"03\/21","cvv":211}],"bank_accounts":[{"name":"Mckenna Lubowitz","number":653315,"branch":535827}]}' /customers
```

```python
```

```shell
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"Customer created",
    "customer":
    {
        "name":"Alexanne Russel",
        "email":"kRuecker@Wintheiser.info",
        "address":"40568 Feil Ferry\nGildafort, MO 50309",
        "credit_cards":
        [{
            "token":"4293284160636483"
        }],
        "bank_accounts":
        [{
            "name":"Mckenna Lubowitz",
            "number":653315,
            "branch":535827
        }],
        "id":"b4e21d75-4d1c-423e-92f1-9b61bdb0ef8a",
        "internal_id":"a34d6e287751a916b921f769"
    }
}
```

Create a new customer.

### HTTP Request

`POST /customers`

## Update a Customer

```curl
curl -X PUT -d '{"name":"Alexanne Russel","email":"kRuecker@Wintheiser.info","address":"40568 Feil Ferry\nGildafort, MO 50309","credit_cards":[{"number":"6011400661639209","expiry_date":"03\/21","cvv":211}],"bank_accounts":[{"name":"Mckenna Lubowitz","number":653315,"branch":535827}]}' /customers/<customer ID>
```

```python
```

```shell
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"Customer updated",
    "customer":
    {
        "name":"Alexanne Russel",
        "email":"kRuecker@Wintheiser.info",
        "address":"40568 Feil Ferry\nGildafort, MO 50309",
        "credit_cards":
        [{
            "token":"4293284160636483"
        }],
        "bank_accounts":
        [{
            "name":"Mckenna Lubowitz",
            "number":653315,
            "branch":535827
        }],
        "id":"b4e21d75-4d1c-423e-92f1-9b61bdb0ef8a",
        "internal_id":"a34d6e287751a916b921f769"
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

```curl
curl -X DELETE -d /customers/<customer ID>
```

```python
```

```shell
```

> The above command returns JSON structured like this:

```json
{
    "code":0,
    "message":"Customer deleted",
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

```ruby
```

```python
```

```curl
curl -X GET /customers/<customer ID>
```

> The above command returns JSON structured like this:

```json
{
    "name":"Bernhard Zemlak",
    "email":"sDietrich@yahoo.com",
    "address":"000 Little Shore\nBuckridgeside, AR 78146",
    "credit_cards":[{
        "token":"3799936454001853"
    }],
    "bank_accounts":[{
        "name":"David Bartell",
        "number":830480,
        "branch":954278
    }],
    "id":"ae80b1e8-3d6b-4787-bbdc-e65ebdcd6c0c",
    "internal_id":"e62dbebb26aa589ecb70c9b7"
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

```ruby
```

```python
```

```curl
curl -X GET /customers
```

> The above command returns JSON structured like this:

```json
[
    {
        "name":"Johnathan Jerde",
        "email":"Gail.Marks@yahoo.com",
        "address":"31369 Treutel Lakes Suite 665\\nWest Bart, HI 51602-9805",
        "credit_cards":
        [
            {
                "token":"4201345141310"
            }
        ],
        "bank_accounts":
        [
            {
                "name":"Mrs. Jude Cronin",
                "number":449277,
                "branch":495371
            }
        ],
        "id":"789ec273-980d-4521-894e-b4cf45974848",
        "internal_id":"67ee491db9e6fdd41b811eb9"
    },
    {
        "name":"Gerry Mills",
        "email":"Shyann05@hotmail.com",
        "address":"8939 Aron Groves\\nWest Keshaunfurt, MD 50056",
        "credit_cards":
        [
            {
                "token":"6642508956106936"
            }
        ],
        "bank_accounts":
        [
            {
                "name":"Liliane Greenholt",
                "number":784569,
                "branch":832919
            }
        ],
        "id":"5cc27a57-e911-425d-8fd9-8dd94e74b043",
        "internal_id":"73b076c5db5bbfe3d2eaaa02"
    },
]
```

Get a list of all customers.

### HTTP Request

`GET /customers`

# Payments 

## Create a Payment

```curl
curl -X POST -d '{"token":"5083312354487131","reference":"Voluptas in quo dolor commodi repellendus.","amount":946900,"currency":"AUD"}' /payments
```

```python
```

```shell
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

