---
title: RickRut's API Reference


search: false
---

# Introduction

> API endpoint

```ruby
GET https://www.rickrut.com/api/v1/
```

Welcome to the RickRut API! You can use our simple JSON API to access candidate management endpoints, which can let you register candidates and retrieve information on them.

You can view code examples in the dark area to the right.

# Structure

> Successful response

```json
{
  "data": {
    ...
  },
  "meta": {
    ... 
  }
}
```

> Error response

```json
{
  "errors": {
    ...
  }
}
```

Our API is designed to be as simple to use as possible. We always use the same basic structure:

* `data` contains the data you requested.
* `meta` provides information regarding your request.
* `errors` shows errors with insights regarding what made the request fail. Learn more about the [errors responses](#errors).



# Authentication

> [Log in](https://www.rickrut.com/users/sign_in) to get your API secret key



Authentication is made with a key you will have to add to every call you make to our API. This parameter is always required. We'll return an error if the key is either missing or invalid.

Your API key is what identifies your account, so make sure to keep it secret! You can at anytime generate or delete API keys on your dashboard.


# Errors

> Error example

```json
{
  "errors" : [
    {
      "id" : "wrong_params",
      "code" : 400,
      "details" : "You are missing the API key"
    }
  ]
}
```

RickRut's API uses conventional HTTP response codes to indicate the success or failure of an API request.

In case of an error, we'll return an array of errors containing information regarding what happened.


Error Code | Meaning
---------- | -------
200 - OK | The request was successful.
201 - Created | The request was successful and the resource was created.
204 - No content | The request was successful and no additional content was sent.
400 - Bad request | Your request was not valid.
401 - Unauthorized | No valid API key was provided.
404 - Not found | The requested resource does not exist.
422 - Unprocessable entity | Your request is valid but the creation of the resource failed. Check the errors.
429 - Too many requests | You have reached your usage limit. Upgrade your plan if necessary.
5XX - Server Errors | Something went wrong on RickRut's end.

