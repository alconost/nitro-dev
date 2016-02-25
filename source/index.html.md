---
title: API Reference

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
  -H "Authorization: {API_KEY}"
```

> Make sure to replace `{API_KEY}` with your API key.

Nitro expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: {API_KEY}`

<aside class="notice">
You must replace <code>{API_KEY}</code> with your personal API key.
</aside>

# Orders

## Get All Orders

```shell
curl "http://api.nitro.alconost.com/v1/orders" \
  -H "Authorization: {API_KEY}"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 6,
    "status": "QUEUE",
    "name": "Test",
    "source_language": "en",
    "target_language": "ru",
    "created_at": "2016-01-29T05:52:17.840197Z",
    "accepted_at": "0001-01-01T00:00:00Z",
    "completed_at": "0001-01-01T00:00:00Z"
  },
  {
    "id": 7,
    "status": "DONE",
    "name": "Test",
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

## Get a Specific Order

```shell
curl "http://api.nitro.alconost.com/v1/orders/6" \
  -H "Authorization: {API_KEY}"
```

> The above command returns JSON structured like this:

```json
{
  "id": 6,
  "source_text": "Test",
  "status": "QUEUE",
  "name": "Test",
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
  -H "Authorization: {API_KEY}" \
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
    "name": "Test",
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
    "name": "Test",
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
curl -X POST "http://api.nitro.alconost.com/v1/orders/6/cancel" \
  -H "Authorization: {API_KEY}"
```

> The above command returns 204 No Content:

This endpoint cancels a specific order.

### HTTP Request

`GET http://api.nitro.alconost.com/v1/orders/<ID>/cancel`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the order to be cancelled

<aside class="notice">
You can cancel order with QUEUE status only.
</aside>