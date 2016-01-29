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

# Tokens

## Create a credit card token

```shell
    curl /tokens \ 
        -u pk_test_cTNdimnqAb625Kjl7JQFbj4c: \
        -X POST \
        -d "card[name]=Dr. Nichole Casper V" \
        -d "card[number]=341694306848167" \
        -d "card[expiry_month]=07" \
        -d "card[expiry_year]=18" \
        -d "card[cvc]=609" \
        -d "card[address_line1]=934 Bechtelar Knolls" \
        -d "card[address_line2]=" \
        -d "card[address_city]=Willmsport" \
        -d "card[address_postcode]=5357" \
        -d "card[address_state]=ACT" \
        -d "card[address_country]=Australia"
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
    "code": 0, 
    "message": "Token created.",
    "token": {
        "token": "tok_6KilthplNtDCnajd",
        "info": {
            "name": "Dr. Nichole Casper V",
            "expiry_month": "07",
            "expiry_year": 18,
            "cvc": 609,
            "address_line1": "934 Bechtelar Knolls",
            "address_line2": "",
            "address_city": "Willmsport",
            "address_postcode": 5357,
            "address_state": "ACT",
            "address_country": "Australia",
            "pan": "34169XXXXXXXX167"
        }
    }   
}
```     
                                                                                                                 
Create a credit card token.
                                                                                                                     
### HTTP Request

`POST /tokens`

## Retrieve a credit card token


```shell
curl /tokens/tok_6KilthplNtDCnajd \
     -u sk_test_YzvwgQwl1BO4xE3hV57S1QsE: \
     -X GET \
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
    "token": "tok_6KilthplNtDCnajd",
    "info": {
        "expiry_month": "07",
        "cvc": 609,
        "address_line2": null,
        "address_line1": "934 Bechtelar Knolls",
        "address_country": "Australia",
        "name": "Dr. Nichole Casper V",
        "address_state": "ACT",
        "address_postcode": 5357,
        "pan": "34169XXXXXXXX167",
        "expiry_year": 18,
        "address_city": "Willmsport"
    }
}
```

Retrieve a credit card token.

### HTTP Request

`GET /tokens/<token ID>`

### URL Parameters

Parameter | Description
--------- | -----------
token ID | The ID of the token to retrieve

## Create a bank account token

```shell
curl /tokens \
     -u pk_test_Lg6j5tD4CezAMc4nOcm3Hxmr: \
     -X POST \
     -d "bank_account[name]=Jimmy Grimes V" \
     -d "bank_account[number]=628279" \
     -d "bank_account[bsb]=343178"
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
    "code": 0,
    "message": "Token created.",
    "token": {
        "token": "tok_DPvhAj8CiZJGEmy4",
            "info": {
                "name": "Jimmy Grimes V",
                "number": 628279,
                "bsb": 343178
            }
        }
    }
```

Create a token for a bank account.

### HTTP Request

`POST /tokens`

## Get a bank account token

```shell
curl /tokens/tok_DPvhAj8CiZJGEmy4 \
     -u sk_test_4kOEEQXZxNRS6VLtg63wLdRT: \
     -X GET \
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
    "token": "tok_DPvhAj8CiZJGEmy4",
    "info": {
        "name": "Jimmy Grimes V",
        "bsb": 343178,
        "number": 628279
    }
}
```

Get a bank account token.

### HTTP Request

`GET /tokens/<token ID>`

### URL Parameters

Parameter | Description
--------- | -----------
token ID | The ID of the token to retrieve

# Merchants 

```shell
curl /merchants \
     -u sk_QyeTXFXrvKd0I7sGObQGY6mi: \
     -X POST \
     -d "title=Prof." \
     -d "first_name=Ryleigh" \
     -d "last_name=Hayes" \
     -d "email=vance.champlin@hane.net" \
     -d "business_name=Braun, Kulas and Heaney" \
     -d "business_phone=249-839-5908" \
     -d "business_website=http://lang.com" \
     -d "abn=18307279381" \
     -d "credit_card[name]=Madalyn Harris" \
     -d "credit_card[number]=5144316381526579" \
     -d "credit_card[expiry_month]=12" \
     -d "credit_card[expiry_year]=18" \
     -d "credit_card[cvc]=788" \
     -d "credit_card[address_line1]=53289 Dickens Crest" \
     -d "credit_card[address_line2]=" \
     -d "credit_card[address_city]=New Cletusberg" \
     -d "credit_card[address_postcode]=3924" \
     -d "credit_card[address_state]=NSW" \
     -d "credit_card[address_country]=Australia" \
     -d "bank_account[name]=Prof. Margie Schuster DDS" \
     -d "bank_account[number]=299481" \
     -d "bank_account[bsb]=692501"
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
    "code": 0,
    "message": "Merchant created.",
    "merchant": {
        "title": "Prof.",
        "first_name": "Ryleigh",
        "last_name": "Hayes",
        "email": "vance.champlin@hane.net",
        "business_name": "Braun, Kulas and Heaney",
        "business_phone": "249-839-5908",
        "business_website": "http:\/\/lang.com",
        "abn": 18307279381,        
        "bank_accounts": [            
            {
                "name": "Prof. Margie Schuster DDS",
                "number": 299481,
                "bsb": 692501
            }
        ],
        "credit_cards": [
            {
                "token": "tok_s02GmYwLhGfgwBDI",
                "creditCardInfo": {
                    "pan": "514431XXXXXXX579",
                    "expiryDate": "12\/18",
                    "cardType": "5",
                    "cardDescription": "Master Card"
                }
            }
        ],
        "id": "mer_3KDrwOWxVk9QQetd",
        "secret_key": "sk_UbT2kNVBV5zd47jjKMpaq4eX",
        "public_key": "pk_asVs4nMBxiLe5T9AO5y9Vh3Y"
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

##<Route name>

```shell
curl /customers \
     -u sk_jPnwDoXglGtnJ5KmBT8iAFeT: \
     -X POST \
     -d "email=kristina.krajcik@gmail.com" \
     -d "credit_card[name]=Lamont Farrell" \
     -d "credit_card[number]=5522860686208732" \
     -d "credit_card[expiry_month]=02" \
     -d "credit_card[expiry_year]=17" \
     -d "credit_card[cvc]=818" \
     -d "credit_card[address_line1]=5735 Adelia Orchard" \     
     -d "credit_card[address_line2]=" \
     -d "credit_card[address_city]=East Chanelle" \
     -d "credit_card[address_postcode]=6309" \
     -d "credit_card[address_state]=NT" \
     -d "credit_card[address_country]=Australia" \
     -d "bank_account[name]=Rhoda Waelchi" \
     -d "bank_account[number]=302083" \
     -d "bank_account[bsb]=105964"
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
    "code": 0,
    "message": "Customer created.",
    "customer": {
        "email": "kristina.krajcik@gmail.com",
        "bank_accounts": [
            {
                "name": "Rhoda Waelchi",
                "number": 302083,
                "bsb": 105964
            }
        ],
        "credit_cards": [
            {
                "token": "tok_gUrrYIWKq2xtZlQD",
                "creditCardInfo": {
                    "pan": "552286XXXXXXX732",
                    "expiryDate": "02\/17",
                    "cardType": "5",
                    "cardDescription": "Master Card"
                }
            }
        ],
        "id": "cus_MuSMXuHnWRL7qN3b",
        "merchant_id": "sk_jPnwDoXglGtnJ5KmBT8iAFeT"
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

# Cards
## Add a card

```shell
curl /merchants/mer_kXwC0TX1m7yh1lBE/cards \
     -u sk_QyeTXFXrvKd0I7sGObQGY6mi: \
     -X POST \
     -d "credit_card[name]=Ms. Eloisa Satterfield Sr." \
     -d "credit_card[number]=5188908314542199" \
     -d "credit_card[expiry_month]=10" \
     -d "credit_card[expiry_year]=17" \
     -d "credit_card[cvc]=680" \
     -d "credit_card[address_line1]=19312 Collins Viaduct" \
     -d "credit_card[address_line2]=" \
     -d "credit_card[address_city]=Lake Aubreyfort" \
     -d "credit_card[address_postcode]=6426" \
     -d "credit_card[address_state]=QLD" \
     -d "credit_card[address_country]=Australia"
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
    "code": 0,
    "message": "Credit card created.",
    "merchant": {
        "business_name": "Sawayn-Gutmann",
        "business_phone": "435-371-5159",
        "credit_cards": [
            {
                "creditCardInfo": {
                    "expiryDate": "09\/18",
                    "cardType": "6",
                    "pan": "448545XXXX677",
                    "cardDescription": "Visa"
                },
                "token": "tok_2eyJrNjqUw4YwS9u"
            },
            {
                "token": "tok_H7bb4RBV3mbmb560",
                "creditCardInfo": {
                    "pan": "518890XXXXXXX199",
                    "expiryDate": "10\/17",
                    "cardType": "5",
                    "cardDescription": "Master Card"
                }
            }
        ],
        "last_name": "Schmidt",
        "bank_accounts": [
            {
                "name": "Demarco Jerde",
                "bsb": 154166,
                "number": 672749
            }
        ],
        "title": "Prof.",
        "abn": 44491048695,
        "first_name": "Jackson",
        "email": "zheller@yahoo.com",
        "business_website": "http:\/\/hauck.com",
        "id": "mer_kXwC0TX1m7yh1lBE"
    }
}
```

Add a card to this account

### HTTP Request

`POST /merchants/<merchant ID>/cards`

### URL Parameters

Parameter | Description
--------- | -----------
merchant ID | The ID of the merchant to add a card to 

## Remove a card from an account

```shell
curl /merchants/mer_kXwC0TX1m7yh1lBE/cards/tok_H7bb4RBV3mbmb560 \
     -u sk_QyeTXFXrvKd0I7sGObQGY6mi: \
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
        "code": 0,
        "message": "Credit card deleted.",
        "merchant": {
            "business_name": "Sawayn-Gutmann",
            "business_phone": "435-371-5159",
            "credit_cards": [
                {
                    "creditCardInfo": {
                        "expiryDate": "09\/18",
                        "cardType": "6",
                        "pan": "448545XXXX677",
                        "cardDescription": "Visa"
                    },
                    "token": "tok_2eyJrNjqUw4YwS9u"
                }
            ],
            "last_name": "Schmidt",
            "bank_accounts": [
                {
                    "name": "Demarco Jerde",
                    "bsb": 154166,
                    "number": 672749
                }
            ],
            "title": "Prof.",
            "abn": 44491048695,
            "first_name": "Jackson",
            "email": "zheller@yahoo.com",
            "business_website": "http:\/\/hauck.com",
            "id": "mer_kXwC0TX1m7yh1lBE"
        }
    }
```

Remove a card from an account.

### HTTP Request

`DELETE /merchants/<merchant ID>/cards/<token>`

### URL Parameters

Parameter | Description
--------- | -----------
merchant ID | The ID of the merchant to add a card to 
token | The token for the card to remove

# Bank Accounts

## Add a bank account

```shell
curl /merchants/mer_vttc1znlfHvbRKww/bankAccounts \
     -u sk_test_QyeTXFXrvKd0I7sGObQGY6mi: \
     -X POST \
     -d "bank_account[name]=Coleman Marks" \
     -d "bank_account[number]=347933" \
     -d "bank_account[bsb]=587061"
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
    "code": 0,
    "message": "Bank account created.",
    "merchant": {
        "business_name": "Stoltenberg PLC",
        "last_name": "Windler",
        "title": "Miss",
        "abn": 77471188579,
        "version": 4,
        "business_website": "http:\/\/halvorson.biz",
        "statement_descriptor": "Pay Stoltenberg PLC",
        "business_phone": "218-788-1937",
        "balance": {
            "AUD": 0
        },
        "credit_cards": [
            {
                "token": "tok_MaLv1xcgAhxocNtY",
                "info": {
                    "expiry_month": "03",
                    "cvc": 492,
                    "address_line2": null,
                    "address_line1": "28308 Aurelia Corner",
                    "address_country": "Australia",
                    "name": "Prof. Mckenzie Klocko",
                    "address_state": "TAS",
                    "address_postcode": 6016,
                    "pan": "49293XXXXXXXX217",
                    "expiry_year": 19,
                    "address_city": "Lake Dawn"
                }
            },
            {
                "token": "tok_YY4xwAsNkp9gWvAh",
                "info": {
                    "expiry_month": "08",
                    "cvc": 760,
                    "address_line2": null,
                    "address_line1": "371 Bernhard Mountains",
                    "address_country": "Australia",
                    "name": "Prof. Kenton Smitham V",
                    "address_state": "WA",
                    "address_postcode": 3606,
                    "pan": "44341XXXXXXXX886",
                    "expiry_year": 21,
                    "address_city": "West Reyes"
                }
            }
        ],
        "bank_accounts": [
            {
                "token": "tok_2QYecX57qWC1y9BE",
                "info": {
                    "name": "Devon Sporer",
                    "bsb": 601023,
                    "number": 928740
                }
            },
            {
                "token": "tok_YuWCnw5qokoT2QMR",
                "info": {
                    "name": "Coleman Marks",
                    "number": 347933,
                    "bsb": 587061
                }
            }
        ],
        "first_name": "Trystan",
        "email": "casimir47@rowe.com",
        "id": "mer_vttc1znlfHvbRKww",
        "updated_at": "2016-01-27 05:01:27",
        "created_at": "2016-01-27 05:01:27"
    }
}
```

Add a bank account to a merchant or customer account

### HTTP Request

`POST /merchants/<merchant id>/bankAccounts`

### URL Parameters

Parameter | Description
--------- | -----------
merchant id | The ID of the merchant to add a bank account to


## Delete a bank account

```shell
curl /merchants/mer_vttc1znlfHvbRKww/bankAccounts/tok_YuWCnw5qokoT2QMR \
     -u sk_test_QyeTXFXrvKd0I7sGObQGY6mi: \
     -X DELETE \
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
    "code": 0,
    "message": "Bank account deleted.",
    "merchant": {
        "business_name": "Stoltenberg PLC",
        "last_name": "Windler",
        "title": "Miss",
        "abn": 77471188579,
        "version": 5,
        "business_website": "http:\/\/halvorson.biz",
        "statement_descriptor": "Pay Stoltenberg PLC",
        "business_phone": "218-788-1937",
        "balance": {
            "AUD": 0
        },
        "credit_cards": [
            {
                "token": "tok_MaLv1xcgAhxocNtY",
                "info": {
                    "expiry_month": "03",
                    "cvc": 492,
                    "address_line2": null,
                    "address_line1": "28308 Aurelia Corner",
                    "address_country": "Australia",
                    "name": "Prof. Mckenzie Klocko",
                    "address_state": "TAS",
                    "address_postcode": 6016,
                    "pan": "49293XXXXXXXX217",
                    "expiry_year": 19,
                    "address_city": "Lake Dawn"
                }
            },
            {
                "token": "tok_YY4xwAsNkp9gWvAh",
                "info": {
                    "expiry_month": "08",
                    "cvc": 760,
                    "address_line2": null,
                    "address_line1": "371 Bernhard Mountains",
                    "address_country": "Australia",
                    "name": "Prof. Kenton Smitham V",
                    "address_state": "WA",
                    "address_postcode": 3606,
                    "pan": "44341XXXXXXXX886",
                    "expiry_year": 21,
                    "address_city": "West Reyes"
                }
            }
        ],
        "bank_accounts": [
            {
                "token": "tok_2QYecX57qWC1y9BE",
                "info": {
                    "name": "Devon Sporer",
                    "bsb": 601023,
                    "number": 928740
                }
            }
        ],
        "first_name": "Trystan",
        "email": "casimir47@rowe.com",
        "id": "mer_vttc1znlfHvbRKww",
        "updated_at": "2016-01-27 05:01:27",
        "created_at": "2016-01-27 05:01:27"
    }
}
```

Delete a bank account.

### HTTP Request

`DELETE /merchants/<merchant id>/bankAccounts/<bank account token>`

### URL Parameters

Parameter | Description
--------- | -----------
merchant id | The ID of the merchant to remove a bank account from
bank account token | The token of the bak account to remove

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

# Transfers

## Create a transfer

```shell
curl /transfers \
     -u sk_test_lFWxyN7FVnLWYh7sYDarBVRL: \
     -X POST \
     -d "amount=2439" \
     -d "currency=AUD" \
     -d "destination=tok_l8F0xt4lzUPWlzzG" \
     -d "description=Omnis aliquid necessitatibus itaque aut eum corrupti."
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
    "code": 0,
    "message": "transfer created.",
    "transfer": {
        "amount": 2439,
        "currency": "AUD",
        "description": "Omnis aliquid necessitatibus itaque aut eum corrupti.",
        "destination": "tok_l8F0xt4lzUPWlzzG",
        "id": "tfr_JYEzwbKqSdF0Z1kY",
        "merchant_id": "mer_8pyqskBUJasZGPDQ",
        "status": 0
    }
}
```

Create a new transfer.

### HTTP Request

`POST /transfers`

## Get transfer details

```shell
curl /transfers/tfr_JYEzwbKqSdF0Z1kY \
     -u sk_test_lFWxyN7FVnLWYh7sYDarBVRL: \
     -X GET \

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
    "amount": 2439,
    "destination": "tok_l8F0xt4lzUPWlzzG",
    "description": "Omnis aliquid necessitatibus itaque aut eum corrupti.",
    "currency": "AUD",
    "status": 0,
    "id": "tfr_JYEzwbKqSdF0Z1kY",
    "merchant_id": "mer_8pyqskBUJasZGPDQ"
}
```

Get transfer details.

A transfer is processed through several states:

Status | Description
------ | -----------
0      | Created - the transfer is newly created and has not yet been processed
1      | Queued - the transfer has been submitted for processing
2      | Pending - the payment processing institution has acknowledge receipt of the transfer request
3      | Failed - The transfer has failed. More information is provided in *status_reason*
4      | Completed - The payment institution has accepted the trasfer for processing
5      | Disbursed - The payment has been disbursed
6      | Returned - The payment has been reversed. A reason code is provided in *status_reason*.

For returns the status reason contains one of the following codes:

Code | Description
---- | -----------
1    | Invalid BSB number 
2    | Payment stopped 
3    | Account closed 
4    | Customer deceased 
5    | No account or incorrect account number 
6    | Refer to customer 
8    | Invalid User ID Number 
9    | Technically invalid

When the status changes the *statusDate* is updated.

### HTTP Request

`GET /transfers/<transfer ID>`

### URL Parameters

Parameter | Description
--------- | -----------
transfer ID | The ID of the transfer to retrieve

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

Type             | Desccription
----             | ------------
cc_payment       | A credit card payment
cc_refund        | A credit card refund
bpay             | A BPAY payment
bpay_correction  | A BPAY correction
bpay_reversal    | A BPAY reversal

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

# Balances

## Get current balance

```shell
curl /balance \
     -u sk_test_JH6Hc4vNAXOlS2IKQHQij85n: \
     -X GET \
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
    "AUD": 32672
}
```

Get current balance.

### HTTP Request

`GET /balance`

## Get balance history

```shell
curl /balance/history \
     -u sk_test_JH6Hc4vNAXOlS2IKQHQij85n: \
     -X GET \
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
    "list": [
        {
            "created_at": "2016-01-22 01:01:07",
            "merchant_id": "mer_ZEv95JWyBXC3yQpL",
            "type": "cc_payment",
            "version": 1,
            "txn_id": "txn_2EDan22JAwm4vkRH",
            "updated_at": "2016-01-22 01:01:07",
        }
    ]
}
```

Get the list of transactions that have contributed to a balance.

### HTTP Request

`GET /balance/history?from=<from date>&to=<to date>&customer=<customer id>&token=<token>&currency=<currency>&type=<type>`

### URL Parameters

<aside class="info">All parameters are optional. If no parameters are provided all transactions are returned.</aside>

Parameter   | Description
---------   | -----------
from date   | The earlest date to include in the report
to date     | The latest date to include in the report
customer id | Show only transactions for the given customer
token       | Show only transactions for the given token (credit card or bank account)
currency    | Show only transactions for the given currenct code, e.g. AUD
type        | Show only transactions of the given type

Type can be any of the following:

Type             | Desccription
----             | ------------
cc_payment       | A credit card payment
cc_refund        | A credit card refund
bpay             | A BPAY payment
bpay_correction  | A BPAY correction
bpay_reversal    | A BPAY reversal

