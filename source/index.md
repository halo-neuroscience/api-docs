---
title: API Reference

language_tabs:
  - shell
  - ruby
  - python

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Halo Neuroscience API.  This is a WIP and currently only available to internal clients (iOS, admin).

# Authentication

Application authentication has not been implemented it.

For user requests after sign in (have link here), the Authorization header should include the user ID, followed by a colon,
followed by the access token which is returned as a response to user sign in.  For example:

`Authorization: 1:-gjzZa8aHs7M7wjyE8xU`

<aside class="notice">
The user ID and access token are returned upon user sign in.
</aside>

# Users

## Create A User

> This is the response from creating a user

```json
{
  "id": 1,
  "email": "example@haloneuro.com",
  "access_token": "-gjzZa8aHs7M7wjyE8xU"
}
```

### HTTP Request

`POST https://api.haloneuro.com/v1/users`

### Body Parameters

Parameter | Default | Description
--------- | ------- | -----------
email | NA | user email
password | NA | account password

# Sessions

## Create a Session (Login)

> This is the response from logging in

```json
{
  "id": 1,
  "email": "example@haloneuro.com",
  "access_token": "-gjzZa8aHs7M7wjyE8xU"
}
```

### HTTP Request

`POST https://api.haloneuro.com/v1/login`

### Body Parameters

Parameter | Default | Description
--------- | ------- | -----------
email | NA | user email
password | NA | account password


## Delete a Session (Logout)

Coming Soon

# Waveforms

## Get All Waveforms

```shell
curl "https://api.haloneuro.com/v1/waveforms"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Waveform 1",
    "description": "This is a description of waveform 1",
    "data": "AAAAAD0AHQAACvh/AQAAA....",
    "bytesize": 382,
    "created_at": "2015-06-10T12:05:23.800Z"
  },
  {
    "id": 2,
    "name": "Waveform 2",
    "description": "This is a description of waveform 2",
    "data": "AEAf2cBALV6AQDqmAEADJo....",
    "bytesize": 20054,
    "created_at": "2015-06-11T16:02:38.800Z"
  }
]
```

This endpoint retrieves all waveforms.

### HTTP Request

`GET https://api.haloneuro.com/v1/waveforms`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
NA | NA | NA
NA | NA | NA

<aside class="notice">
Binary data is base64 encoded so can be escaped and placed into string element for JSON.
Typical waveform file is about 20KB, base64 expands size to about 27KB.
</aside>

## Get a Specific Waveform

```shell
curl "https://api.haloneuro.com/v1/waveforms/2"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Waveform 2",
  "description": "This is a description of waveform 2",
  "data": "AEAf2cBALV6AQDqmAEADJo....",
  "bytesize": 20054,
  "created_at": "2015-06-11T16:02:38.800Z"
}
```

This endpoint retrieves a specific waveform.

### HTTP Request

`GET https://api.haloneuro.com/v1/waveforms/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the waveform to retrieve

<aside class="notice">
Binary data is base64 encoded so can be escaped and placed into string element for JSON.
Typical waveform file is about 20KB, base64 expands size to about 27KB.
</aside>

## Create A Waveform

> This is the response from creating a waveform

```json
{
  "id": 2,
  "name": "Waveform 2",
  "description": "This is a description of waveform 2",
  "data": "AEAf2cBALV6AQDqmAEADJo....",
  "bytesize": 20054,
  "created_at": "2015-06-11T16:02:38.800Z"
}
```

### HTTP Request

`POST https://api.haloneuro.com/v1/waveforms`

### Body Parameters

Parameter | Default | Description
--------- | ------- | -----------
name | NA | waveform name
description | NA | waveform description
data | NA | waveform file

<aside class="notice">
File along with name and description should be sent as part of multipart/form-data POST.
Support for uploading as base64 encoded JSON coming soon.
</aside>
