# Errors

The Nitro API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Something went wrong, please see the response body for details (error code, description)
401 | Unauthorized -- Invalid API key
403 | Forbidden -- The resource requested is hidden for administrators only
404 | Not Found -- The specified resource could not be found
405 | Method Not Allowed -- You tried to access a resource with an invalid method
406 | Not Acceptable -- You requested a format that isn't json
429 | Too Many Requests -- You're requesting too many resources! Slow down!
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.

> In case of 400 (Bad Request) response code, there is an error object returned in the response body. The error object contains the error code, error description and, optionally, additional parameters related to the error. E.g:

```json
{
  "code" : "HUMAN_READABLE_ERROR_CODE",
  "description": "Human readable description of the error",
  "param1": "Error specific additional parameter 1",
  "param2": "Error specific additional parameter 2"
}
```

The 400 error codes are:

Error Code | Meaning
---------- | -------
INSUFFICIENT_FUNDS | There's not enough funds on the account to place an order
WRONG_ORDER_STATUS | The order is not in the QUEUE status (already taken or completed) and you try to delete it
