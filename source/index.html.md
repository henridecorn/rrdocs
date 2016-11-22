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

# Create an applicant

> HTTP request example

```ruby
POST https://www.rickrut.com/api/v1/applicants?api_key=b95cad3e4825ba123995a87b594444dc7a9150f7
```

> Request body

```json
{
  "email": "john.smith@gmail.com",
  "opening": "software-engineer",
  "first_name": "John",
  "last_name": "Smith"
}
```

> Response: 201 OK

```json
{
  "data": {
    "id": "31415",
    "type": "applicants",
    "attributes": {
      "email": "john.smith@gmail.com",
      "opening-id": 47,
      "status": "REMINDED",
      "skill-score": null,
      "adequation-score": null,
      "first-name": "John",
      "last-name": "Smith",
      "code": "IKWOOFKE",
      "recruiter-score": 0,
      "source": "API",
      "step": 0,
      "cv": "/cvs/original/missing.png",
      "video-uuid": null,
      "audio-introduction": "/audio_introductions/original/missing.png",
      "text-introduction": null,
      "slug": "de-corn-henri-9b1fef96-f3cf-43c3-9c2d-809c73693a17",
      "created-at": "2016-11-18T13:02:04Z",
      "updated-at": "2016-11-21T14:49:05Z",
      "finished-at": null
    },
    "relationships": {
      "quizz-answers": {
        "data": []
      },
      "poll-answers": {
        "data": []
      },
      "case-answers": {
        "data":[]
      }
    }
  }
}
```

This API endpoint enables you to register a new applicant to one of your openings.

Parameter | Required | Description
--------- | -------- | -----------
**email** | True | The applicant's email.
**opening** | True | The name of the opening.
**first_name** | False | The applicant's first_name.
**last_name** | False | The applicant's last_name.
**api_key** | True | Your secret API key. You can generate it in your dashboard.


# Get an applicant

> HTTP request example

```ruby
GET https://www.rickrut.com/api/v1/applicants/31415?api_key=b95cad3e4825ba123995a87b594444dc7a9150f7
```

> Response: 200 OK

```json
{
  "data": {
    "id": "329",
    "type": "applicants",
    "attributes": {
      "email": "john.smith@gmail.com",
      "opening-id": 45,
      "status": "SCORED",
      "skill-score": "15.0",
      "adequation-score": "100.0",
      "first-name": "John",
      "last-name": "Smith",
      "code": "ATZDVQDH",
      "recruiter-score": 0,
      "source": "API",
      "step": 6,
      "cv": "/cvs/original/missing.png",
      "video-uuid": null,
      "audio-introduction": "/audio_introductions/original/missing.png",
      "text-introduction": null,
      "slug": "de-corn-henri-2016-10-27-09-02-49-utc",
      "created-at": "2016-10-27T09:02:49Z",
      "updated-at": "2016-10-27T09:03:35Z",
      "finished-at": null
    },
    "relationships": {
      "quizz-answers": {
        "data": [
          {
            "id": "150",
            "type": "quizz-answers"
          }
        ]
      },
      "poll-answers": {
        "data": []
      },
      "case-answers": {
        "data": [
          {
            "id":"212",
            "type":"case-answers"
          }
        ]
      }
    }
  },
  "included": [
    {
      "id": "150",
      "type": "quizz-answers",
      "attributes": {
        "quizz": 28,
        "value":"Oui"
      }
    },
    {
      "id": "212",
      "type": "case-answers",
      "attributes": {
        "value": null,
        "audio-file": "/system/case_answers/audio_files/000/000/212/original/audio_recording_1477558998009.mp3?1477558998",
        "duration": 8,
        "gibberish": true
      }
    }
  ]
}
```

Retrieves all the fields of an applicant, including his/her answers and scores.

Parameter | Required | Description
--------- | -------- | -----------
**id** | True | Identifier of the applicant.
**api_key** | True | Your secret API key. You can generate it in your dashboard.





