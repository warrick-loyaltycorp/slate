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

To use your API key, pass it to the stripe module. The Node.js library then will automatically send this key in each request.

All API requests must be made over HTTPS. Calls made over plain HTTP will fail. API requests without authentication will also fail.

# Errors

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

<aside class="warning">If you're not using an administrator API key, note that some kittens will return 403 Forbidden if they are hidden for admins only.</aside>

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

### URL Parameters

Parameter | Description
--------- | -----------
ID | The API key to retrieve details for

## Get a Customer

```ruby
```

```python
```

```curl
curl -X POST -d '' /customers
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

### HTTP Request

`GET /apikeys/<APIKey>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The API key to retrieve details for

