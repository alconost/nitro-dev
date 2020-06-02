---
title: Nitro API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='mailto:nitro@alconost.com'>Contact Us</a>

includes:
  - errors

search: false
---

# Introduction  

Welcome to the Alconost Nitro API! You can use our API to access Nitro API endpoints.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "Authorization: Basic <base64("email:password")>" \
  -H "Content-Type: application/json" 
```

Nitro expects credentials to be included in all API requests to the server in authentication header that looks like the following:

`Authorization: Basic <base64("email:password")>`

# User

## Get User

```shell
curl "https://nitro.alconost.com/api/v1/user" \
  -H "Authorization: Basic ZW1haWw6cGFzc3dvcmQ="\
  -H "Content-Type: application/json" 
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

`GET https://nitro.alconost.com/api/v1/user`


# Orders

## Get All Orders

```shell
curl "https://nitro.alconost.com/api/v1/orders" \
  -H "Authorization: Basic ZW1haWw6cGFzc3dvcmQ=" \
  -H "Content-Type: application/json" 

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

`GET https://nitro.alconost.com/api/v1/orders`

### Query Parameters

Parameter | Type | Description
--------- | ---- | -----------
page | integer | Page number (default: 0)
per_page | Orders count (default: 20)


## Get a Specific Order

```shell
curl "https://nitro.alconost.com/api/v1/orders/6" \
  -H "Authorization: Basic c3Jpbml2YXNtMjAxMEBnbWFpbC5jb206dGVzdEBrcHQ="\
  -H "Content-Type: application/json" 

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

`GET https://nitro.alconost.com/api/v1/orders/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the order to retrieve

## Translate

```shell
curl "https://nitro.alconost.com/api/v1/translate" \
  -H "Authorization: Basic c3Jpbml2YXNtMjAxMEBnbWFpbC5jb206dGVzdEBrcHQ="\
  -H "Content-Type:application/json" \
  -d '{
      "source_language": "en",
      "target_languages": ["ru", "it"],
      "text": "Text to translate"
      }'
```
> The above command returns JSON structured like this:

```json
{
  "orders": [
    {
      "id": 6,
      "source_language": "en",
      "target_language": "ru",
      "price": 0.04,
      "created_at": "2016-01-29T05:52:17.840197Z"
    },
    {
      "id": 7,
      "source_language": "en",
      "target_language": "it",
      "price": 0.05,
      "created_at": "2016-01-29T05:52:17.840197Z"
    }
  ],
  "text": "Text to translate",
  "hint": "Hint for translator",
  "volume": 4
}
```
This endpoint sends the text for translation and creates a list of orders.

### HTTP Request

`POST https://nitro.alconost.com/api/v1/translate`

### Attributes

Parameter | Type | Description
--------- | ---- | -----------
source_language | string | Source language
target_languages | array | Collection of target languages
text | string | Text to be translated
hint | string | Hint for translator
quality | enum | Translation quality (at this moment EXCELLENT quality supported only)

## Delete an Order

```shell
curl "https://nitro.alconost.com/api/v1/orders/6" \
  -H "Authorization: Basic ZW1haWw6cGFzc3dvcmQ="\
  -H "Content-Type: application/json" 

```

> The above command returns 204 No Content:

This endpoint deletes a specific order.

### HTTP Request

`DELETE https://nitro.alconost.com/api/v1/orders/<ID>`

### URL Parameters

Parameter | Type | Description
--------- | ---- | -----------
ID | integer | The ID of the order to be deleted

<aside class="notice">
You can delete orders with QUEUE status only.
</aside>


# Rates

## Get Rates

```shell
curl "https://nitro.alconost.com/api/v1/rates" \
  -H "Authorization: Basic ZW1haWw6cGFzc3dvcmQ=}"\
  -H "Content-Type: application/json" 

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

`GET https://nitro.alconost.com/api/v1/rates`
