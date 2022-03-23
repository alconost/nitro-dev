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

```shell
curl "api_endpoint_here" \
  -H "Content-Type: application/json" \
  -u apikey: 
```

HTTP Basic authentication. The API key acts as the username. API keys are per-account and can be generated and deleted in the Settings page.

# Account

## Get Account

```shell
curl "https://nitro.alconost.com/api/v1/account" \
  -H "Content-Type: application/json" \
  -u apikey:
```

> The above command returns JSON structured like this:

```json
{
  "id" : 123,
  "balance_overdraft_allowed": false,
  "reserved": 0.24,
  "balance": 174.46
}
```

This endpoint retrieves an account.

### HTTP Request

`GET https://nitro.alconost.com/api/v1/account`


# Orders

## Get All Orders

```shell
curl "https://nitro.alconost.com/api/v1/orders" \
  -H "Content-Type: application/json" \
  -u apikey:
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
    "created_at": "2016-01-29T05:52:17.840197Z"
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

This endpoint retrieves all account orders.

### HTTP Request

`GET https://nitro.alconost.com/api/v1/orders`

### Query Parameters

Parameter | Type | Description
--------- | ---- | -----------
page | integer | Page number (default: 0)
per_page | Orders count (default: 20)


## Get a Specific Order

```shell
curl "https://nitro.alconost.com/api/v1/orders/7" \
  -H "Content-Type: application/json" \
  -u apikey:
```

> The above command returns JSON structured like this:

```json
{
  "id": 7,
  "source_text": "Test",
  "target_text": "Test",
  "status": "DONE",
  "hint": "",
  "snippet": "Test",
  "source_language": "en",
  "target_language": "it",
  "volume": 4,
  "price": 0.05,
  "created_at": "2016-01-29T05:52:17.840197Z",
  "accepted_at": "2016-01-30T012:45:01.223137Z",
  "completed_at": "2016-01-30T13:00:47.312484Z"
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
  -H "Content-Type: application/json" \
  -u apikey: \
  -d '{
      "source_language": "en",
      "target_languages": ["ru", "it"],
      "text": "Text to translate",
      "context" : {
        "comment": {
          "text": "Translation instructions",
          "attachments": [
            { "type": "image/png", "data" : "base64 encoded image" },
            { "type": "image/gif", "data" : "base64 encoded image" }
          ]
        },
        "tone": "GUESS",
        "limit": 25
      }
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
  "volume": 4
}
```
This endpoint sends the text for translation and creates a list of orders.

### HTTP Request

`POST https://nitro.alconost.com/api/v1/translate`

### Attributes

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
source_language | Yes | string | Source language
target_languages | Yes | array | Collection of target languages
text | Yes | string | Text to be translated
hint | | string | Hint for translator
context | | object | Context for translator. Includes comment, tone, limit
context.comment | | object | Comment for translator. Includes text, attachments
context.comment.text | | string | Text of comment
context.comment.attachments | | array | Array of image objects
context.tone | | enum | Choose the tone of translation: FORMAL, INFORMAL. Or let our translators choose the tone themselves by specifying GUESS
context.limit | | integer | Limit of the allowed number of characters

### Attachments

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
type | Yes | string | Image mime type (like image/png). Supported image types are png, jpeg and gif
data | Yes | string | Base64 encoded image

## Delete an Order

```shell
curl -X DELETE "https://nitro.alconost.com/api/v1/orders/6" \
  -H "Content-Type: application/json" \
  -u apikey:
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
  -H "Content-Type: application/json"
```

> The above command returns JSON structured like this:

```json
[
  {"source_language": "en", "target_language": "ms", "rate": 15.4 },
  {"source_language": "en", "target_language": "tl", "rate": 15.4 },
  {"source_language": "en", "target_language": "is", "rate": 20.0 }
]
````

This endpoint retrieves all rates.

### HTTP Request

`GET https://nitro.alconost.com/api/v1/rates`
