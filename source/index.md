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

The Eoneo Pay API is RESTful. API URL's intuitively reflect resource names and HTTP response codes indicate API errors. Standard HTTP verbs are used to add (POST), retrieve (GET), update (PUT) and delete (DELETE) resources.

All API accounts have two sets of keys - one set for test mode and one for live mode. Use the test mode keys to make API requests without executing live banking transactions. Use public keys in client side web applications to request credit card and bank account tokens. Use secret keys for all other API requests. Secret keys should never be published in client side code.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -u your_api_key:
```

```PHP
// use EoneoPay\EoneoPay;
EoneoPay::setApiKey('your api key');
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
curl /apikeys/sk_test_pTAETUWZjlsyue0o2pzwii8s \
     -u sk_test_QyeTXFXrvKd0I7sGObQGY6mi: \
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
    "api_key": "sk_test_pTAETUWZjlsyue0o2pzwii8s",
    "api_permissions": [
        "customers",
        "payments",
        "tokens",
        "transfers",
        "balance"
    ],
    "api_status": 1,
    "merchant_id": "mer_w2FaDQdXKNn26Bil",
    "id": "sk_test_pTAETUWZjlsyue0o2pzwii8s"
}
```

Retrieve all details for a specific API key.

<aside class="warning">An administrator API key is required to manage API keys</aside>

### HTTP Request

`GET /apikeys/<APIKey>`

### URL Parameters

Parameter | Description
--------- | -----------
APIKey | The API key to  revoke

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
APIKey | The API key to retrieve details for

# Tokens

## Create a credit card token

```shell
curl /v1/tokens \
     -u pk_test_QCi2W6ca73G03HxQ6vCUWrJF: \
     -X POST \
     -d "card[name]=Prof. Ryan Parisian" \
     -d "card[number]=5213122451942050" \
     -d "card[expiry_month]=12" \
     -d "card[expiry_year]=18" \
     -d "card[cvc]=273" \
     -d "card[address_line1]=6034 Prosacco Fields" \
     -d "card[address_line2]=" \
     -d "card[address_city]=Port Grayceville" \
     -d "card[address_postcode]=4750" \
     -d "card[address_state]=WA" \
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
        "id": "tok_hf5TL8AYsduR0j1s",
        "source_id": "src_0z71AcAGAsLhn5Lh",
        "updated_at": "2016-02-25 04:06:35",
        "created_at": "2016-02-25 04:06:35",
        "version": 1
    }
}
```     
                                                                                                                 
Create a credit card token.
                                                                                                                     
### HTTP Request

`POST /tokens`

## Retrieve a credit card token


```shell
curl /v1/tokens/tok_xfuL5tyVrLe5k20F \
     -u sk_test_Dg3UPZ5IammQbbglwKGQWGyo: \
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
    "created_at": "2016-02-25 05:10:56",
    "source_id": "src_mxiQQmHEfXtll3oI",
    "updated_at": "2016-02-25 05:10:56",
    "version": 1,
    "id": "tok_xfuL5tyVrLe5k20F",
    "source": {
        "updated_at": "2016-02-25 05:10:56",
        "holder_id": "mer_zoIlXkzQnemFIfOS",
        "created_at": "2016-02-25 05:10:56",
        "id": "src_mxiQQmHEfXtll3oI",
        "version": 1,
        "token": "ny6VdPSBXbWV",
        "info": {
            "expiry_month": "08",
            "cvc": 790,
            "address_line2": null,
            "address_line1": "2154 Hirthe Skyway",
            "address_country": "Australia",
            "name": "Roderick Ledner",
            "address_state": "NT",
            "address_postcode": 5610,
            "pan": "51167XXXXXXXX161",
            "expiry_year": 18,
            "address_city": "Port Christaton"
        }
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
curl /v1/tokens \
     -u pk_test_sifZWBjtMU9R2XI9iBIylpf1: \
     -X POST \
     -d "bank_account[name]=Shane Renner" \
     -d "bank_account[number]=762643" \
     -d "bank_account[bsb]=196947"
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
        "id": "tok_iyXaixsK8H5XAYlS",
        "source_id": "src_Z4vETKJuVpEPCeXN",
        "updated_at": "2016-02-25 05:10:56",
        "created_at": "2016-02-25 05:10:56",
        "version": 1
    }
}
```

Create a token for a bank account.

### HTTP Request

`POST /tokens`

## Get a bank account token

```shell
curl /v1/tokens/tok_iyXaixsK8H5XAYlS \
     -u sk_test_Dg3UPZ5IammQbbglwKGQWGyo: \
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
    "created_at": "2016-02-25 05:10:56",
    "source_id": "src_Z4vETKJuVpEPCeXN",
    "updated_at": "2016-02-25 05:10:56",
    "version": 1,
    "id": "tok_iyXaixsK8H5XAYlS",
    "source": {
        "updated_at": "2016-02-25 05:10:56",
        "holder_id": "mer_zoIlXkzQnemFIfOS",
        "created_at": "2016-02-25 05:10:56",
        "id": "src_Z4vETKJuVpEPCeXN",
        "version": 1,
        "token": "nE63VUFUweX4",
        "info": {
            "name": "Shane Renner",
            "bsb": 196947,
            "number": 762643
        }
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

## Create a merchant

```shell
curl /v1/merchants \
     -u sk_test_QyeTXFXrvKd0I7sGObQGY6mi: \
     -X POST \
     -d "title=Dr." \
     -d "first_name=Sadie" \
     -d "last_name=Kris" \
     -d "email=Marvin.Luisa@OReilly.com" \
     -d "business_name=Lockman LLC" \
     -d "business_phone=(767)699-1752x87291" \
     -d "business_website=http://Bergnaum.biz" \
     -d "abn=21332447230" \
     -d "credit_card[name]=Dr. Alfonso Dare DVM" \
     -d "credit_card[number]=5570047709172670" \
     -d "credit_card[expiry_month]=10" \
     -d "credit_card[expiry_year]=19" \
     -d "credit_card[cvc]=902" \
     -d "credit_card[address_line1]=945 Ebba Highway" \
     -d "credit_card[address_line2]=" \
     -d "credit_card[address_city]=Borisbury" \
     -d "credit_card[address_postcode]=6978" \
     -d "credit_card[address_state]=QLD" \
     -d "credit_card[address_country]=Australia" \
     -d "bank_account[name]=Jalyn Schulist" \
     -d "bank_account[number]=645304" \
     -d "bank_account[bsb]=104456" \
     -d "statement_descriptor=Pay Lockman LLC" \
     -d "clearing_account=3"
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
        "title": "Dr.",
        "first_name": "Sadie",
        "last_name": "Kris",
        "email": "Marvin.Luisa@OReilly.com",
        "business_name": "Lockman LLC",
        "business_phone": "(767)699-1752x87291",
        "business_website": "http:\/\/Bergnaum.biz",
        "abn": 21332447230,
        "statement_descriptor": "Pay Lockman LLC",
        "clearing_account": 3,
        "bank_accounts": [
            {
                "name": "Jalyn Schulist",
                "bsb": 104456,
                "number": 645304,
                "id": "src_CYIMRkLIJbebrpSA"
            }
        ],
        "credit_cards": [
            {
                "expiry_month": "10",
                "cvc": 902,
                "address_line2": null,
                "address_line1": "945 Ebba Highway",
                "address_country": "Australia",
                "name": "Dr. Alfonso Dare DVM",
                "address_state": "QLD",
                "address_postcode": 6978,
                "pan": "55700XXXXXXXX670",
                "expiry_year": 19,
                "address_city": "Borisbury",
                "id": "src_Zg1Cb8DuIiUiMGSS"
            }
        ],
        "id": "mer_WTidK388g9zLqHdb",
        "balance": {
            "AUD": 0
        },
        "updated_at": "2016-02-25 05:16:17",
        "created_at": "2016-02-25 05:16:17",
        "version": 1,
        "secret_live_key": "sk_live_SAbtx7HL8AjvxMvI6pe41fQZ",
        "secret_test_key": "sk_test_VYKGdkUD7rLHvnPERHLeqwPr",
        "public_live_key": "pk_live_AGkU9tmiDlAQfUv9qOB3uk2d",
        "public_test_key": "pk_test_XQUIpmXHcUuMvun0daF5jdvv"
    }
}
```

Create a new merchant.

This call returns the new merchant record, including:

1. The API Keys for this merchant.
2. The merchant unique ID. Use the unique ID to retrieve the merchant.
3. A token and PAN for each credit card. The token and PAN replace the credit card number.
4. A token for each bank account.

<aside class="warning">An administrator API key is required to manage API keys</aside>

### HTTP Request

`POST /merchants`

## Update a Merchant

```shell
curl /v1/merchants/mer_WTidK388g9zLqHdb \
     -u sk_test_QyeTXFXrvKd0I7sGObQGY6mi: \
     -X PUT \
     -d "email=rVon@Rosenbaum.biz"
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
    "message": "Merchant updated.",
    "merchant": {
        "clearing_account": 3,
        "business_name": "Lockman LLC",
        "last_name": "Kris",
        "title": "Dr.",
        "abn": 21332447230,
        "version": 2,
        "business_website": "http:\/\/Bergnaum.biz",
        "statement_descriptor": "Pay Lockman LLC",
        "business_phone": "(767)699-1752x87291",
        "balance": {
            "AUD": 0
        },
        "credit_cards": [
            "src_Zg1Cb8DuIiUiMGSS"
        ],
        "bank_accounts": [
            "src_CYIMRkLIJbebrpSA"
        ],
        "first_name": "Sadie",
        "email": "rVon@Rosenbaum.biz",
        "id": "mer_WTidK388g9zLqHdb",
        "updated_at": "2016-02-25 05:16:17",
        "created_at": "2016-02-25 05:16:17"
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
curl /v1/merchants/mer_WTidK388g9zLqHdb \
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
    "message": "Merchant deleted."
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
curl /v1/merchants/mer_WTidK388g9zLqHdb \
     -u sk_test_QyeTXFXrvKd0I7sGObQGY6mi: \
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
    "clearing_account": 3,
    "business_name": "Lockman LLC",
    "last_name": "Kris",
    "title": "Dr.",
    "abn": 21332447230,
    "version": 1,
    "business_website": "http:\/\/Bergnaum.biz",
    "statement_descriptor": "Pay Lockman LLC",
    "business_phone": "(767)699-1752x87291",
    "balance": {
        "AUD": 0
    },
    "credit_cards": [
        {
            "expiry_month": "10",
            "cvc": 902,
            "address_line2": null,
            "address_line1": "945 Ebba Highway",
            "address_country": "Australia",
            "name": "Dr. Alfonso Dare DVM",
            "address_state": "QLD",
            "address_postcode": 6978,
            "pan": "55700XXXXXXXX670",
            "expiry_year": 19,
            "address_city": "Borisbury",
            "id": "src_Zg1Cb8DuIiUiMGSS"
        }
    ],
    "bank_accounts": [
        {
            "name": "Jalyn Schulist",
            "bsb": 104456,
            "number": 645304,
            "id": "src_CYIMRkLIJbebrpSA"
        }
    ],
    "first_name": "Sadie",
    "email": "Marvin.Luisa@OReilly.com",
    "id": "mer_WTidK388g9zLqHdb"
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
curl /v1/customers \
     -u sk_test_PMWDWMDvK5EvMwf2eOYb445w: \
     -X POST \
     -d "email=zKozey@gmail.com" \
     -d "credit_card[name]=Mina Metz IV" \
     -d "credit_card[number]=4485461330960" \
     -d "credit_card[expiry_month]=03" \
     -d "credit_card[expiry_year]=21" \
     -d "credit_card[cvc]=510" \
     -d "credit_card[address_line1]=02486 Darien Meadows" \
     -d "credit_card[address_line2]=" \
     -d "credit_card[address_city]=Kovacekmouth" \
     -d "credit_card[address_postcode]=4256" \
     -d "credit_card[address_state]=SA" \
     -d "credit_card[address_country]=Australia" \
     -d "bank_account[name]=Miss Aryanna Bins" \
     -d "bank_account[number]=992118" \
     -d "bank_account[bsb]=372757"
```

```PHP
//use EoneoPay\Customer;

$customer = new Customer;
$customer->email = 'zKozey@gmail.com';
$customer = $customer->save();

$creditCard = new CreditCard;
$creditCard->number = '4485461330960';
$creditCard->expiry_month = 3;
$creditCard->expiry_year = 21;
$creditCard->name = 'Mina Metz IV';
$creditCard->cvc = '510';
$creditCard->address_line1='02486 Darien Meadows';
$creditCard->address_line2='';
$creditCard->address_city='Kovacekmout';
$creditCard->address_postcode='4256';
$creditCard->address_state='SA';
$creditCard->address_country='Australia';

$customer->addCreditCard($creditCard);

$bankAccount = new BankAccount;
$bankAccount->number = '992118';
$bankAccount->bsb = '372757';
$bankAccount->name = 'Miss Aryanna Bins';

$customer->addBankAccount($bankAccount);

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
        "email": "zKozey@gmail.com",
        "bank_accounts": [
            {
                "name": "Miss Aryanna Bins",
                "bsb": 372757,
                "number": 992118,
                "id": "src_x3HFGRfC6MRcJGuf"
            }
        ],
        "credit_cards": [
            {
                "expiry_month": "03",
                "cvc": 510,
                "address_line2": null,
                "address_line1": "02486 Darien Meadows",
                "address_country": "Australia",
                "name": "Mina Metz IV",
                "address_state": "SA",
                "address_postcode": 4256,
                "pan": "44854XXXXXXXX960",
                "expiry_year": 21,
                "address_city": "Kovacekmouth",
                "id": "src_nLMTTZIbdFkhrVWj"
            }
        ],
        "id": "cus_ci54AkvX11i83W98",
        "merchant_id": "mer_uLo1CZqxeE5OWwne",
        "updated_at": "2016-02-18 04:58:07",
        "created_at": "2016-02-18 04:58:07",
        "version": 1
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
//use EoneoPay\Customer;

$customer->email = 'Blanda.Sofia@hotmail.com';
$customer = $customer->save();
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
//use EoneoPay\Customer;

$customer->delete();
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
//use EoneoPay\Customer;

$customer = Customer::retrieve('cus_P3thMWG1tRvdfING');
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

# Cards (Merchants)
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

# Cards (Customers)

## Add a card

```shell
curl /customers/cus_ZO1gllSfTvQMZdYu/cards \
         -u sk_test_mFWVbfH4JpsA25mpbfZwhbhw: \
         -X POST \
         -d "credit_card[name]=Oran Borer" \
         -d "credit_card[number]=4916454547269724" \
         -d "credit_card[expiry_month]=01" \
         -d "credit_card[expiry_year]=17" \
         -d "credit_card[cvc]=503" \
         -d "credit_card[address_line1]=12898 Ernser Shoal" \
         -d "credit_card[address_line2]=" \
         -d "credit_card[address_city]=Arloberg" \
         -d "credit_card[address_postcode]=6846" \
         -d "credit_card[address_state]=NSW" \
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
    "customer": {
        "credit_cards": [
            {
                "token": "tok_fgt2qhBFos16rtVD",
                "info": {
                    "expiry_month": "10",
                    "cvc": 929,
                    "address_line2": null,
                    "address_line1": "4017 Camden Mews",
                    "address_country": "Australia",
                    "name": "Bette Rau Jr.",
                    "address_state": "NT",
                    "clearingAccount": null,
                    "address_postcode": 4117,
                    "pan": "40240XXXXXXXX448",
                    "expiry_year": 18,
                    "address_city": "West Elvis"
                }
            },
            {
                "token": "tok_MpLZrSXNU3mQp3eS",
                "info": {
                    "name": "Oran Borer",
                    "expiry_month": "01",
                    "expiry_year": 17,
                    "cvc": 503,
                    "address_line1": "12898 Ernser Shoal",
                    "address_line2": "",
                    "address_city": "Arloberg",
                    "address_postcode": 6846,
                    "address_state": "NSW",
                    "address_country": "Australia",
                    "clearingAccount": null,
                    "pan": "49164XXXXXXXX724"
                }
            }
        ],
        "bank_accounts": [
            {
                "token": "tok_T6ICAtj9EA7JLcHm",
                "info": {
                    "name": "Pearl Bahringer",
                    "bsb": 318633,
                    "clearingAccount": null,
                    "number": 919109
                }
            }
        ],
        "email": "leann.bernier@hotmail.com",
        "id": "cus_ZO1gllSfTvQMZdYu",
        "merchant_id": "mer_JqVHiprqD1fxuIgL",
        "updated_at": "2016-01-29 04:01:20",
        "created_at": "2016-01-29 04:01:20",
        "version": 1
    }
}
```

Add a credit card to a customer account.

### HTTP Request

`POST /customers/<customer id>/cards`

### URL Parameters

Parameter | Description
--------- | -----------
customer ID | The ID of the customer to add a card to 

## Delete a card

```shell
curl /customers/cus_tTsMhz5RYPDog9Ua/cards/tok_PisfMAt8ILjcrGuN \
     -u sk_test_MjUMEIEkqVpemreYEyYJMRvT: \
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
    "message": "Credit card deleted.",
    "customer": {
        "credit_cards": [
        {
            "token": "tok_gSz4xDBUYima9Yr0",
            "info": {
                "expiry_month": "09",
                "cvc": 476,
                "address_line2": null,
                "address_line1": "52696 Dawson Vista",
                "address_country": "Australia",
                "name": "Gardner Gaylord",
                "address_state": "SA",
                "clearingAccount": null,
                "address_postcode": 5978,
                "pan": "37771XXXXXXXX886",
                "expiry_year": 17,
                "address_city": "East Monty"
            }
        }
        ],
        "bank_accounts": [
            {
                "token": "tok_Dai6e1jqfY7Wo946",
                "info": {
                    "name": "Miss Litzy Hudson DVM",
                    "bsb": 604526,
                    "clearingAccount": null,
                    "number": 104578
                }
            }
        ],
        "email": "cordie40@pacocha.info",
        "id": "cus_tTsMhz5RYPDog9Ua",
        "merchant_id": "mer_3YnwyFOLKI1YZnja",
        "updated_at": "2016-01-29 05:01:19",
        "version": 1
    }
}
```

Delete a credit card from a customer account.

### HTTP Request

`DELETE /customers/<customer id>/cards/<token>`

### URL Parameters

Parameter | Description
--------- | -----------
customer id | The id of the customer to add a card to 
token | The token for the card to remove

# Bank Accounts (Merchants)

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
bank account token | The token of the bank account to remove

# Bank Accounts (Customers)

## Add a bank account

```shell
curl /customers/cus_ZO1gllSfTvQMZdYu/bankAccounts \
     -u sk_test_mFWVbfH4JpsA25mpbfZwhbhw: \
     -X POST \
     -d "bank_account[name]=Hoyt Botsford" \
     -d "bank_account[number]=559392" \
     -d "bank_account[bsb]=701670"
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
        "customer": {
            "credit_cards": [
            {
                "token": "tok_fgt2qhBFos16rtVD",
                "info": {
                    "expiry_month": "10",
                    "cvc": 929,
                    "address_line2": null,
                    "address_line1": "4017 Camden Mews",
                    "address_country": "Australia",                    
                    "name": "Bette Rau Jr.",                    
                    "address_state": "NT",                    
                    "clearingAccount": null,
                    "address_postcode": 4117,
                    "pan": "40240XXXXXXXX448",
                    "expiry_year": 18,
                    "address_city": "West Elvis"
                }
            },
            {
                "token": "tok_MpLZrSXNU3mQp3eS",
                "info": {
                    "expiry_month": "01",
                    "cvc": 503,
                    "address_line2": null,
                    "address_line1": "12898 Ernser Shoal",
                    "address_country": "Australia",
                    "name": "Oran Borer",
                    "address_state": "NSW",
                    "clearingAccount": null,
                    "address_postcode": 6846,
                    "pan": "49164XXXXXXXX724",
                    "expiry_year": 17,
                    "address_city": "Arloberg"
                }
            }
            ],
                "bank_accounts": [
                {
                    "token": "tok_T6ICAtj9EA7JLcHm",
                    "info": {
                        "name": "Pearl Bahringer",
                        "bsb": 318633,
                        "clearingAccount": null,
                        "number": 919109
                    }
                },
                {
                    "token": "tok_byh3sLy4kwxeCYOo",
                    "info": {
                        "name": "Hoyt Botsford",
                        "number": 559392,
                        "bsb": 701670,
                        "clearingAccount": null
                    }
                }
            ],
                "email": "leann.bernier@hotmail.com",
                "id": "cus_ZO1gllSfTvQMZdYu",
                "merchant_id": "mer_JqVHiprqD1fxuIgL",
                "updated_at": "2016-01-29 04:01:20",
                "created_at": "2016-01-29 04:01:20",
                "version": 1
        }
}
```

<Description>

### HTTP Request

`POST /customers/<customer id>/bankAccounts`

### URL Parameters

Parameter | Description
--------- | -----------
customer id | The ID of the customer to add a bank account to

## Delete a bank account

```shell
curl /customers/cus_ZO1gllSfTvQMZdYu/bankAccounts/tok_byh3sLy4kwxeCYOo \
     -u sk_test_mFWVbfH4JpsA25mpbfZwhbhw: \
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
        "customer": {
            "credit_cards": [
            {
                "token": "tok_fgt2qhBFos16rtVD",
                "info": {
                    "expiry_month": "10",
                    "cvc": 929,
                    "address_line2": null,
                    "address_line1": "4017 Camden Mews",
                    "address_country": "Australia",
                    "name": "Bette Rau Jr.",
                    "address_state": "NT",
                    "clearingAccount": null,
                    "address_postcode": 4117,
                    "pan": "40240XXXXXXXX448",
                    "expiry_year": 18,
                    "address_city": "West Elvis"
                }
            },
            {
                "token": "tok_MpLZrSXNU3mQp3eS",
                "info": {
                    "expiry_month": "01",
                    "cvc": 503,
                    "address_line2": null,
                    "address_line1": "12898 Ernser Shoal",
                    "address_country": "Australia",
                    "name": "Oran Borer",
                    "address_state": "NSW",
                    "clearingAccount": null,
                    "address_postcode": 6846,
                    "pan": "49164XXXXXXXX724",
                    "expiry_year": 17,
                    "address_city": "Arloberg"
                }
            }
            ],
                "bank_accounts": [
                {
                    "token": "tok_T6ICAtj9EA7JLcHm",
                    "info": {
                        "name": "Pearl Bahringer",
                        "bsb": 318633,
                        "clearingAccount": null,
                        "number": 919109
                    }
                }
            ],
                "email": "leann.bernier@hotmail.com",
                "id": "cus_ZO1gllSfTvQMZdYu",
                "merchant_id": "mer_JqVHiprqD1fxuIgL",
                "updated_at": "2016-01-29 04:01:20",
                "created_at": "2016-01-29 04:01:20",
                "version": 1
        }
}
```

Delete a bank account from a customer account.

### HTTP Request

`DELETE /customers/<customer id>/bankAccounts/<bank account token>`

### URL Parameters

Parameter | Description
--------- | -----------
customer id | The ID of the customer to remove a bank account from
bank account token | The token of the bank account to remove

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
curl /v1/fees/cc_payment \
     -u sk_test_QyeTXFXrvKd0I7sGObQGY6mi: \
     -X PUT \
     -d "transaction_fee=0.3" \
     -d "card_rates[MasterCard]=1.5" \
     -d "card_rates[Visa]=1.5" \
     -d "card_rates[AMEX]=2.9"
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

# Plans

## Create a plan

```shell
curl /v1/plans \
     -u sk_test_FV0hGqjo0EcR5oDJg9v94ALM: \
     -X POST \
     -d "name=Quae facilis enim quis impedit ea blanditiis. Et est doloribus laborum. Qui rerum modi soluta illo. Eos dolor delectus velit eius ut pariatur vel." \
     -d "amount=40687" \
     -d "interval=year" \
     -d "intervalCount=3" \
     -d "currency=AUD" \
     -d "fees[0][description]=Sit quibusdam corrupti omnis sit sint. Ut eum quis sint nisi quasi ipsa. At autem accusamus consequatur. Doloremque numquam non nemo aliquid iste. Et et laudantium id qui." \
     -d "fees[0][amount]=2848" \
     -d "fees[0][trigger]=periodical" \
     -d "fees[0][proration]=all"
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
    "message": "Plan created.",
    "plan": {
        "name": "Quae facilis enim quis impedit ea blanditiis. Et est doloribus laborum. Qui rerum modi soluta illo. Eos dolor delectus velit eius ut pariatur vel.",
        "currency": "AUD",
        "amount": 40687,
        "interval": "year",
        "fees": [
            {
                "description": "Sit quibusdam corrupti omnis sit sint. Ut eum quis sint nisi quasi ipsa.\nAt autem accusamus consequatur. Doloremque numquam non nemo aliquid iste. Et et laudantium id qui.",
                "amount": 2848,
                "trigger": "periodical",
                "proration": "all"
            }
        ],
        "interval_count": 1,
        "id": "plan_AcFxxK9m5azQDXr0",
        "merchant_id": "mer_kaspq1kl1LuQhboO",
        "updated_at": "2016-02-29 04:36:34",
        "created_at": "2016-02-29 04:36:34",
        "version": 1
    }
}
```

Create a new subscription plan. Customers must be subscribed to a plan in order to process payments against a plan.

### HTTP Request

`POST /v1/plans`

## Get a Plan

```shell
curl /v1/plans/plan_AcFxxK9m5azQDXr0 \
     -u sk_test_FV0hGqjo0EcR5oDJg9v94ALM: \
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
    "interval_count": 1,
    "amount": 40687,
    "fees": [
        {
            "description": "Sit quibusdam corrupti omnis sit sint. Ut eum quis sint nisi quasi ipsa.\nAt autem accusamus consequatur. Doloremque numquam non nemo aliquid iste. Et et laudantium id qui.",
            "amount": 2848,
            "trigger": "periodical",
            "proration": "all"
        }
    ],
    "name": "Quae facilis enim quis impedit ea blanditiis. Et est doloribus laborum. Qui rerum modi soluta illo. Eos dolor delectus velit eius ut pariatur vel.",
    "currency": "AUD",
    "interval": "year",
    "id": "plan_AcFxxK9m5azQDXr0",
    "merchant_id": "mer_kaspq1kl1LuQhboO"
}
```

<Description>

### HTTP Request

`GET /v1/plans/<plan ID>`

## Update a plan

```shell
curl /v1/plans/plan_AcFxxK9m5azQDXr0 \
     -u sk_test_FV0hGqjo0EcR5oDJg9v94ALM: \
     -X PUT \
     -d "name=Quae facilis enim quis impedit ea blanditiis. Et est doloribus laborum. Qui rerum modi soluta illo. Eos dolor delectus velit eius ut pariatur vel." \
     -d "currency=AUD" \
     -d "amount=81374" \
     -d "interval=year" \
     -d "fees[0][description]=Sit quibusdam corrupti omnis sit sint. Ut eum quis sint nisi quasi ipsa.  At autem accusamus consequatur. Doloremque numquam non nemo aliquid iste. Et et laudantium id qui." \
     -d "fees[0][amount]=2848" \
     -d "fees[0][trigger]=periodical" \
     -d "fees[0][proration]=all" \
     -d "interval_count=1" \
     -d "id=plan_AcFxxK9m5azQDXr0" \
     -d "merchant_id=mer_kaspq1kl1LuQhboO" \
     -d "updated_at=2016-02-29 04:36:34" \
     -d "created_at=2016-02-29 04:36:34" \
     -d "version=1"
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
    "message": "Plan updated.",
    "plan": {
        "interval_count": 1,
        "amount": 81374,
        "fees": [
            {
                "description": "Sit quibusdam corrupti omnis sit sint. Ut eum quis sint nisi quasi ipsa.\nAt autem accusamus consequatur. Doloremque numquam non nemo aliquid iste. Et et laudantium id qui.",
                "amount": 2848,
                "trigger": "periodical",
                "proration": "all"
            }
        ],
        "name": "Quae facilis enim quis impedit ea blanditiis. Et est doloribus laborum. Qui rerum modi soluta illo. Eos dolor delectus velit eius ut pariatur vel.",
        "currency": "AUD",
        "interval": "year",
        "id": "plan_AcFxxK9m5azQDXr0",
        "merchant_id": "mer_kaspq1kl1LuQhboO",
        "version": 2,
        "created_at": "2016-02-29 04:36:34",
        "updated_at": "2016-02-29 04:36:34"
    }
}
```

Update a plan with new details.

### HTTP Request

`PUT /v1/plans/<plan ID>`

## Delete a plan

```shell
curl /v1/plans/plan_R6bTUkP0BrPQtkLf \
     -u sk_live_Zb0kaUsCLwL51YQ60fxd3Lz3: \
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
    "message": "Plan deleted."
}
```

Delete a plan. All subscriptions will be deleted.

### HTTP Request

`DELETE /v1/plans/<plan ID>`

# Subscriptions

## Create a subscription

```shell
curl /v1/customers/cus_w9fPGpw8tJaFtVK8/subscriptions \
     -u sk_test_FV0hGqjo0EcR5oDJg9v94ALM: \
     -X POST \
     -d "plan=plan_AcFxxK9m5azQDXr0" \
     -d "source=src_tY4D1y87aWH1wQHN" \
     -d "start_date=2016-03-01" \
     -d "end_date=2017-03-31"
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
    "message": "Subscription created.",
    "subscription": {
        "id": "sub_bZ3NhZJ0i5Fiihpf",
        "customer_id": "cus_w9fPGpw8tJaFtVK8",
        "plan_id": "plan_AcFxxK9m5azQDXr0",
        "status": "active",
        "source": "src_tY4D1y87aWH1wQHN",
        "start_date": "2016-03-01",
        "end_date": "2017-03-31",
        "updated_at": "2016-02-29 04:36:34",
        "created_at": "2016-02-29 04:36:34",
        "version": 1,
        "plan": {
            "interval_count": 1,
            "amount": 81374,
            "fees": [
                {
                    "description": "Sit quibusdam corrupti omnis sit sint. Ut eum quis sint nisi quasi ipsa.\nAt autem accusamus consequatur. Doloremque numquam non nemo aliquid iste. Et et laudantium id qui.",
                    "amount": 2848,
                    "trigger": "periodical",
                    "proration": "all"
                }
            ],
            "name": "Quae facilis enim quis impedit ea blanditiis. Et est doloribus laborum. Qui rerum modi soluta illo. Eos dolor delectus velit eius ut pariatur vel.",
            "currency": "AUD",
            "interval": "year",
            "id": "plan_AcFxxK9m5azQDXr0",
            "merchant_id": "mer_kaspq1kl1LuQhboO"
        }
    }
}
```

Create a new subscription. The customer is subscribed to the specified plan. Any payments made with the subscription ID as a payment reference will be allocated to this subscription.

### HTTP Request

`POST /v1/customers/<customer ID>/subscriptions`

## Get a subscription

```shell
curl /v1/customers/cus_w9fPGpw8tJaFtVK8/subscriptions/sub_bZ3NhZJ0i5Fiihpf \
     -u sk_test_FV0hGqjo0EcR5oDJg9v94ALM: \
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
    "end_date": "2017-03-31",
    "source": "src_tY4D1y87aWH1wQHN",
    "customer_id": "cus_w9fPGpw8tJaFtVK8",
    "plan_id": "plan_AcFxxK9m5azQDXr0",
    "status": "active",
    "start_date": "2016-03-01",
    "id": "sub_bZ3NhZJ0i5Fiihpf",
    "plan": {
        "interval_count": 1,
        "amount": 81374,
        "fees": [
            {
                "description": "Sit quibusdam corrupti omnis sit sint. Ut eum quis sint nisi quasi ipsa.\nAt autem accusamus consequatur. Doloremque numquam non nemo aliquid iste. Et et laudantium id qui.",
                "amount": 2848,
                "trigger": "periodical",
                "proration": "all"
            }
        ],
        "name": "Quae facilis enim quis impedit ea blanditiis. Et est doloribus laborum. Qui rerum modi soluta illo. Eos dolor delectus velit eius ut pariatur vel.",
        "currency": "AUD",
        "interval": "year",
        "id": "plan_AcFxxK9m5azQDXr0",
        "merchant_id": "mer_kaspq1kl1LuQhboO"
    }
}
```

Get subscription details.

### HTTP Request

`GET /v1/customers/<customer ID>/subscriptions/<subscription ID>

## Cancel a subscription

```shell
curl /v1/customers/cus_w9fPGpw8tJaFtVK8/subscriptions/sub_bZ3NhZJ0i5Fiihpf \
     -u sk_test_FV0hGqjo0EcR5oDJg9v94ALM: \
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
    "message": "api_messages.subscription_cancelled"
}
```

Cancel the specified subscription.

### HTTP Request

`DELETE /v1/customers/<customer ID>/subscriptions/<subscription ID>`
