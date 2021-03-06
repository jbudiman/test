---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: Yes
---

# Introduction

Welcome to Bitcoin World partner integration API. 

This API documentation page was created with [Slate](https://github.com/lord/slate). Feel free to edit it and use it as a base for your own API's documentation.


# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: FooBar"
```

> Make sure to replace `FooBar` with your API key.

Bitcoin.World uses API keys to allow access to the API. You can register a new Bitcoin.World API key at our [developer portal](http://example.com/developers).

Bitcoin.World expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: FooBar`

<aside class="notice">
You must replace <code>FooBar</code> with your personal API key.
</aside>

# Accounts
The Api endpoints to manage accounts. 
## Get Account

```shell
curl "https://api.bitcoin.world/accounts"
  -H "Authorization: foobar"
```

> The above command returns JSON structured like this:
`GET https://api.bitcoin.world/accounts/id/<ACCOUNT_ID>`

```json
{
  "id": 1001,
  "status": "OK",
  "kyc": {
    "status": "incomplete",
    "reason": "missing document"
  }
}
```

This endpoint retrieves a customer's account details.

### HTTP Request
`GET http://api.bitcoin.world/accounts/<ACCOUNT_ID>` 
### Parameters
    _TBD_
## Create Account
This endpoint registers an account for a customer. The account registration requires a bare minimum of an email address 
and a mobile phone to create. 

On successful registration, an account id will be provided for the customer.

You maybe able to update customer details by adding KYC details. Adding KYC detail for the customer will allow them
to access greater tier benefits such as being able to purchase with more payments and with higher daily limit.
### HTTP Request
    POST http://api.bitcoin.world/accounts/
### Query Parameters
Parameter | Required | Description
--------- | -------- | -----------
mobile_phone    | Yes  | mobile numbers of type *string*. International format `61412708135`
email           | Yes  | email address of type *string*. 

# Rates
This endpoint returns the exchange rates.
### HTTP Request
`GET http://api.bitcoin.world/rates/`
# Orders
The Api endpoints to manage order creation.
## Get Orders
Returns the order status by `order_id`. 
The `order_id` can be obtained after order has been created with the *Create Orders* API endpoint below.
### HTTP Request
`GET http://api.bitcoin.world/orders/<ORDER_ID>`
### Query Parameters
Parameter | Required | Description
--------- | -------- | -----------
order_id  | Yes     | The order id returned by `create orders` endpoint
## Create Orders
This endpoint creates an order. 
When order is created, customer should be redirected to bitcoin.world url checkout page the url is indicated in the response.
The response will also contain an `order_id`, that can be used to check the order status.
### HTTP Request
`GET http://api.bitcoin.world/orders`
### Query Parameters
Parameter | Required | Description
--------- | -------- | -----------
coin_amount                 | Yes  | the cryptocurrency amount of type *float* up to *8* decimal points. e.g 0.12345678 
coin_code                   | Yes  | the cryptocurrency code of type *string*. e.g. 'BTC'. Code must be offered in the rates API
fiat_amount                 | Yes  | the fiat currency amount of type *float* up to *2* decimal points.
fiat_code                   | Yes  | the fiat currency code of type *string* e.g. 'AUD'. Code must be offered in the rates API
wallet_address              | Yes  | Wallet address of type *string*. We would prefer you to do the validation on your side.
account_id                  | Yes  | @internal Discuss with the team if this is necessary. The account_id the order belongs to
*rate_id                    | No | @internal Discuss with the team if this is necessary
callback_url_on_success     | Yes  |
callback_url_on_failure     | Yes  |

<aside class="success">
This API endpoint requires an authentication header
</aside>



# Customers
The Api endpoints registers the customers KYC _(This can probably be combined with Accounts api)_
## Register Customer KYC
```shell
curl "http://api.bitcoinworld.com/customers"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
[
  {}
]
```
### HTTP Request
`POST http://example.com/api/customers`
### Query Parameters
Parameter | Required | Description
--------- | ------- | -----------
account_id          | Yes  | The account ID
given_name          | Yes  | The first name of the customer
middle_name         | No | The middle name of the customer, if any.
surname             | Yes  | The family name of the customer
flat_number         | No | The address flat number
street_number       | Yes  | The address street number
street_name         | Yes  | The address street name
street_type         | Yes  | The address street type
suburb              | Yes  | The address suburb
state               | Yes  | The address state
post_code           | Yes  | The address post code
country             | Yes  | The country of residence
dob                 | Yes  | The date of birth in *YYYY-MM-DD* format of type *string*
document_ids        | Yes  | The document identification number of type *string*
document_type       | No | The identification document of type *string*. e.g. *passport* 
document_file_urls  | Yes  | The document link image or pdf file(s) that is accessible by us.

You can add multiple file urls `document_file_urls` by adding JSON collection like below:

```json
  { 
    "files": [ 
      "https://example.com/id_front.jpg",
      "https://example.com/id_back.jpg"
      ]
  }
```

<aside class="success">
Must attach authentication header
</aside>




