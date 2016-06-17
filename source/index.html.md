---
title: Nitro API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='mailto:nitro@alconost.com'>Contact Us</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Alconost Nitro API! You can use our API to access Nitro API endpoints.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "Authorization: Basic {TOKEN}"
```

> Make sure to replace `{TOKEN}` with your token.

Nitro expects the token to be included in all API requests to the server in a Basic authentication header that looks like the following:

`Authorization: Basic {TOKEN}`

<aside class="notice">
You must replace <code>{TOKEN}</code> with your personal token. Personal token is `email:password` Base64 encoded.
</aside>

# User

## Get User

```shell
curl "http://api.nitro.alconost.com/v1/user" \
  -H "Authorization: {TOKEN}"
```

> The above command returns JSON structured like this:

```json
{
  "id" : 123,
  "email": "test@alconost.com",
  "full_name": "Nitro",
  "balance_overdraft_allowed": false,
  "reserved": 0.24,
  "balance": 174.46
}
```

This endpoint retrieves a user.

### HTTP Request

`GET http://api.nitro.alconost.com/v1/user`


# Orders

## Get All Orders

```shell
curl "http://api.nitro.alconost.com/v1/orders" \
  -H "Authorization: {TOKEN}"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 6,
    "status": "QUEUE",
    "snippet": "Test",
    "source_language": "en",
    "target_language": "ru",
    "created_at": "2016-01-29T05:52:17.840197Z",
    "accepted_at": "0001-01-01T00:00:00Z",
    "completed_at": "0001-01-01T00:00:00Z"
  },
  {
    "id": 7,
    "status": "DONE",
    "snippet": "Test",
    "source_language": "en",
    "target_language": "it",
    "created_at": "2016-01-29T05:52:17.840197Z",
    "accepted_at": "2016-01-30T012:45:01.223137Z",
    "completed_at": "2016-01-30T13:00:47.312484Z"
  }
]
```

This endpoint retrieves all user orders.

### HTTP Request

`GET http://api.nitro.alconost.com/v1/orders`

### Query Parameters

Parameter | Type | Description
--------- | ---- | -----------
page | integer | Page number (default: 0)
per_page | Orders count (default: 20)


## Get a Specific Order

```shell
curl "http://api.nitro.alconost.com/v1/orders/6" \
  -H "Authorization: {TOKEN}"
```

> The above command returns JSON structured like this:

```json
{
  "id": 6,
  "source_text": "Test",
  "status": "QUEUE",
  "hint": "",
  "snippet": "Test",
  "source_language": "en",
  "target_language": "ru",
  "volume": 4,
  "price": 0.04,
  "created_at": "2016-01-29T05:52:17.840197Z",
  "accepted_at": "0001-01-01T00:00:00Z",
  "completed_at": "0001-01-01T00:00:00Z",
  "quality": "EXCELLENT"
}
```

This endpoint retrieves a specific order.

### HTTP Request

`GET http://api.nitro.alconost.com/v1/orders/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the order to retrieve

## Create an Order

```shell
curl -X POST "http://api.nitro.alconost.com/v1/orders" \
  -H "Authorization: {TOKEN}" \
  -d source_language="en" \
  -d target_languages=["ru", "it"] \
  -d text="Test" \
  -d quality="EXCELLENT"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 6,
    "source_text": "Test",
    "status": "QUEUE",
    "hint": "",
    "snippet": "Test",
    "source_language": "en",
    "target_language": "ru",
    "volume": 4,
    "price": 0.04,
    "created_at": "2016-01-29T05:52:17.840197Z",
    "accepted_at": "0001-01-01T00:00:00Z",
    "completed_at": "0001-01-01T00:00:00Z",
    "quality": "EXCELLENT"
  },
  {
    "id": 7,
    "source_text": "Test",
    "status": "QUEUE",
    "hint": "",
    "snippet": "Test",
    "source_language": "en",
    "target_language": "it",
    "volume": 4,
    "price": 0.04,
    "created_at": "2016-01-29T05:52:17.840197Z",
    "accepted_at": "0001-01-01T00:00:00Z",
    "completed_at": "0001-01-01T00:00:00Z",
    "quality": "EXCELLENT"
  }
]
```

This endpoint creates a new order.

### HTTP Request

`POST http://api.nitro.alconost.com/v1/orders`

### Attributes

Parameter | Type | Description
--------- | ---- | -----------
source_language | string | Source language
target_languages | array | Collection of target languages
text | string | Text to be translated
quality | enum | Translation quality (at this moment EXCELENT quality supported only)

## Cancel an Order

```shell
curl -X PUT "http://api.nitro.alconost.com/v1/orders/6/cancel" \
  -H "Authorization: {TOKEN}"
```

> The above command returns 204 No Content:

This endpoint cancels a specific order.

### HTTP Request

`PUT http://api.nitro.alconost.com/v1/orders/<ID>/cancel`

### URL Parameters

Parameter | Type | Description
--------- | ---- | -----------
ID | integer | The ID of the order to be cancelled

<aside class="notice">
You can cancel order with QUEUE status only.
</aside>


# Rates

## Get Rates

```shell
curl "http://api.nitro.alconost.com/v1/rates" \
  -H "Authorization: {TOKEN}"
```

> The above command returns JSON structured like this:

```json
[
  {"sourceLanguage":"en", "targetLanguage":"ms", "rate":15.4, "quality":"EXCELLENT"},
  {"sourceLanguage":"en", "targetLanguage":"tl", "rate":15.4, "quality":"EXCELLENT"},
  {"sourceLanguage":"en", "targetLanguage":"is", "rate":20.0, "quality":"EXCELLENT"}
]
````

This endpoint retrieves all rates.

### HTTP Request

`GET http://api.nitro.alconost.com/v1/rates`


# Transactions

## Get All Transactions

```shell
curl "http://api.nitro.alconost.com/v1/transactions" \
  -H "Authorization: {TOKEN}"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 53742,
    "time": "2016-03-30T15:52:27.29Z",
    "amount": 5,
    "balance": 10,
    "reason": "ADD_WITHDRAW_FUNDS"
  },
  {
    "id": 53716,
    "time": "2016-03-23T16:22:18.791Z",
    "amount": 5,
    "balance": 5,
    "reason": "ADD_WITHDRAW_FUNDS"
  }
]
```

This endpoint retrieves all user transactions. At this moment the `reason` property is enum and can be equals `ADD_WITHDRAW_FUNDS` or `CUSTOMER_FEE`.

### HTTP Request

`GET http://api.nitro.alconost.com/v1/transactions`

### Query Parameters

Parameter | Type | Description
--------- | ---- | -----------
page | integer | Page number (default: 0)
per_page | Transactions count (default: 20)