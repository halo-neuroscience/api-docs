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

For client requests that are not user specific, the Authorization header should include "Token", followed by the client key.  For example:

`Authorization: Token 43cdfc04d99680dcc9828bd44ff41`

For user requests after sign in (have link here), the Authorization header should include "Bearer", followed by the user ID, followed by a colon,
followed by the access token which is returned as a response to user sign in.  For example:

`Authorization: Bearer 1:-gjzZa8aHs7M7wjyE8xU`

<aside class="notice">
The user ID and access token are returned upon user sign in.
</aside>

# Users

## Create A User

> This is the response from creating a user

```json
{
  "id": 1,
  "name": "John Doe",
  "email": "example@haloneuro.com",
  "access_token": "-gjzZa8aHs7M7wjyE8xU"
}
```

### HTTP Request

`POST https://api.haloneuro.com/v1/users`

### Body Parameters

Parameter | Default | Description
--------- | ------- | -----------
name | NA | user name
email | NA | user email
password | NA | account password

# Sessions

## Create a Session (Login)

> This is the response from logging in

```json
{
  "id": 1,
  "name": "John Doe",
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
    "byte_size": 382,
    "duration_in_seconds": 600,
    "impedance_waveform": "AABQABAA...",
    "clip_config": {
      "left": true,
      "center": true,
      "right": true,
      "description": "All clips should be installed"
    },
    "visual_profile": {
      "stim_type_image_url": {
        "1x": "https://halo-api-images.s3.amazonaws.com/waveforms/1/training_1x/original.png?12345",
        "2x": "https://halo-api-images.s3.amazonaws.com/waveforms/1/training_2x/original.png?12345",
        "3x": "https://halo-api-images.s3.amazonaws.com/waveforms/1/training_3x/original.png?12345"
      },
      "remote_bg_image_url": {
        "1x": "https://halo-api-images.s3.amazonaws.com/waveforms/1/remote_1x/original.png?12345",
        "2x": "https://halo-api-images.s3.amazonaws.com/waveforms/1/remote_2x/original.png?12345",
        "3x": "https://halo-api-images.s3.amazonaws.com/waveforms/1/remote_3x/original.png?12345"
      },
      "gradient_start_hex": "#AA9FFF",
      "gradient_end_hex": "#FF7399"
    },
    "level_multiplier": {
      "1": "0x45",
      "2": "0x5a",
      "3": "0x69",
      "4": "0x76",
      "5": "0x80",
      "6": "0x87",
      "7": "0x8e",
      "8": "0x94",
      "9": "0x9b",
      "10": "0xa0"
    },
    "created_at": "2015-06-10T12:05:23.800Z"
  },
  {
    "id": 2,
    "name": "Waveform 2",
    "description": "This is a description of waveform 2",
    "data": "AEAf2cBALV6AQDqmAEADJo....",
    "byte_size": 20054,
    "duration_in_seconds": 600,
    "impedance_waveform": "AABQABAA...",
    "clip_config": {
      "left": true,
      "center": false,
      "right": true,
      "description": "Left and Right clips should be installed"
    },
    "visual_profile": {
      "stim_type_image_url": {
        "1x": "https://halo-api-images.s3.amazonaws.com/waveforms/2/training_1x/original.png?12345",
        "2x": "https://halo-api-images.s3.amazonaws.com/waveforms/2/training_2x/original.png?12345",
        "3x": "https://halo-api-images.s3.amazonaws.com/waveforms/2/training_3x/original.png?12345"
      },
      "remote_bg_image_url": {
        "1x": "https://halo-api-images.s3.amazonaws.com/waveforms/2/remote_1x/original.png?12345",
        "2x": "https://halo-api-images.s3.amazonaws.com/waveforms/2/remote_2x/original.png?12345",
        "3x": "https://halo-api-images.s3.amazonaws.com/waveforms/2/remote_3x/original.png?12345"
      },
      "gradient_start_hex": "#AA9FFF",
      "gradient_end_hex": "#FF7399"
    },
    "level_multiplier": {
      "1": "0x45",
      "2": "0x5a",
      "3": "0x69",
      "4": "0x76",
      "5": "0x80",
      "6": "0x87",
      "7": "0x8e",
      "8": "0x94",
      "9": "0x9b",
      "10": "0xa0"
    },
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
  "byte_size": 20054,
  "duration_in_seconds": 600,
  "impedance_waveform": "AABQABAA...",
  "clip_config": {
    "left": true,
    "center": false,
    "right": true,
    "description": "Left and Right clips should be installed"
  },
  "visual_profile": {
    "stim_type_image_url": {
      "1x": "https://halo-api-images.s3.amazonaws.com/waveforms/2/training_1x/original.png?12345",
      "2x": "https://halo-api-images.s3.amazonaws.com/waveforms/2/training_2x/original.png?12345",
      "3x": "https://halo-api-images.s3.amazonaws.com/waveforms/2/training_3x/original.png?12345"
    },
    "remote_bg_image_url": {
      "1x": "https://halo-api-images.s3.amazonaws.com/waveforms/2/remote_1x/original.png?12345",
      "2x": "https://halo-api-images.s3.amazonaws.com/waveforms/2/remote_2x/original.png?12345",
      "3x": "https://halo-api-images.s3.amazonaws.com/waveforms/2/remote_3x/original.png?12345"
    },
    "gradient_start_hex": "#AA9FFF",
    "gradient_end_hex": "#FF7399"
  },
  "level_multiplier": {
    "1": "0x45",
    "2": "0x5a",
    "3": "0x69",
    "4": "0x76",
    "5": "0x80",
    "6": "0x87",
    "7": "0x8e",
    "8": "0x94",
    "9": "0x9b",
    "10": "0xa0"
  },
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
  "byte_size": 20054,
  "duration_in_seconds": 600,
  "impedance_waveform": "AABQABAA...",
  "clip_config": {
    "left": true,
    "center": false,
    "right": true,
    "description": "Left and Right clips should be installed"
  },
  "visual_profile": {
    "stim_type_image_url": {
      "1x": "https://halo-api-images.s3.amazonaws.com/waveforms/2/training_1x/original.png?12345",
      "2x": "https://halo-api-images.s3.amazonaws.com/waveforms/2/training_2x/original.png?12345",
      "3x": "https://halo-api-images.s3.amazonaws.com/waveforms/2/training_3x/original.png?12345"
    },
    "remote_bg_image_url": {
      "1x": "https://halo-api-images.s3.amazonaws.com/waveforms/2/remote_1x/original.png?12345",
      "2x": "https://halo-api-images.s3.amazonaws.com/waveforms/2/remote_2x/original.png?12345",
      "3x": "https://halo-api-images.s3.amazonaws.com/waveforms/2/remote_3x/original.png?12345"
    },
    "gradient_start_hex": "#AA9FFF",
    "gradient_end_hex": "#FF7399"
  },
  "level_multiplier": {
    "1": "0x45",
    "2": "0x5a",
    "3": "0x69",
    "4": "0x76",
    "5": "0x80",
    "6": "0x87",
    "7": "0x8e",
    "8": "0x94",
    "9": "0x9b",
    "10": "0xa0"
  },
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

# Events

## Get All Events

```shell
curl "https://api.haloneuro.com/v1/events"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "user_id": "1",
    "message_id": "1",
    "message_content": {"key-1": "value-1"},
    "timestamp": "2015-06-10T12:05:23.800Z"
  },
  {
    "id": 2,
    "user_id": "1",
    "message_id": "1",
    "message_content": {"key-1": "value-2"},
    "timestamp": "2015-06-11T12:05:23.800Z"
  }
]
```

This endpoint retrieves all events.

### HTTP Request

`GET https://api.haloneuro.com/v1/events`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
NA | NA | NA
NA | NA | NA

<aside class="notice">
message_content is in JSON format.
</aside>

## Get a Specific Event

```shell
curl "https://api.haloneuro.com/v1/events/2"
```

> The above command returns JSON structured like this:

```json
  {
    "id": 2,
    "user_id": "1",
    "message_id": "1",
    "message_content": {"key-1": "value-2"},
    "timestamp": "2015-06-11T12:05:23.800Z"
  }
```

This endpoint retrieves a specific event.

### HTTP Request

`GET https://api.haloneuro.com/v1/events/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the event to retrieve

<aside class="notice">
message_content is in JSON format.
</aside>

## Create A Event

> This is the response from creating a event

```json
  {
    "id": 2,
    "user_id": "1",
    "message_id": "1",
    "message_content": {"key-1": "value-2"},
    "timestamp": "2015-06-11T12:05:23.800Z"
  }
```

### HTTP Request

`POST https://api.haloneuro.com/v1/events`

### Body Parameters

Parameter | Default | Description
--------- | ------- | -----------
user_id | NA | user id (optional)
message_id | NA | message id (optional)
message_content | NA | event content (JSON)
timestamp | NA | datetime of event (default is current time)

<aside class="notice">
message_content should be in JSON format.
</aside>
