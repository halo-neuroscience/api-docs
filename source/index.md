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

All client requests should include the application client key using this format:

`Authorization: Halo client-key=43cdfc04d99680dcc9828bd44ff41`

For user requests after sign in (see Sessions), the Authorization header should also include the user ID and access token which is returned
as a response to user sign in.  For example:

`Authorization: Halo client-key=43cdfc04d99680dcc9828bd44ff41, user-id=1, user-access-token=-gjzZa8aHs7M7wjyE8xU`

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

# Firmware Update

## Get Latest Firmware Update

> This is the response from getting a firmware update

```json
{
  "id": 1,
  "version_number": "0.0.1",
  "url": "https://halo-api-images.s3.amazonaws.com/firmware/1/raw.bin?1447288415"
}
```
This endpoint retrieves the most recent firmware version

### HTTP Request

`GET https://api.haloneuro.com/v1/firmware_update`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
NA | NA | NA
NA | NA | NA

# Organization

## Get Organization

> This is the response from getting an organization

```json
{
  "id": 1,
  "name": "Sparta",
  "city": "Menlo Park",
  "state": "California",
  "participants": [
    {
      "id": 1,
      "name": "Steve Smith"
    },
    {
      "id": 2,
      "name": "Jane Stevens"
    },
    {
      "id": 1,
      "name": "Bob Jones"
    }
  ]
}
```
This endpoint retrieves the organization that is associated with
the logged in user.  The user access token should be passed in via
the Authorization Header..

### HTTP Request

`GET https://api.haloneuro.com/v1/organization`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
NA | NA | NA
NA | NA | NA

# Sessions

## Create a Session (Login)

> This is the response from logging in

```json
{
  "id": 1,
  "name": "John Doe",
  "email": "example@haloneuro.com",
  "access_token": "-gjzZa8aHs7M7wjyE8xU",
  "organization": {
    "id": 1,
    "name": "Sparta",
    "city": "Menlo Park",
    "state": "California",
    "participants": [
      {
        "id": 1,
        "name": "Steve Smith"
      },
      {
        "id": 2,
        "name": "Jane Stevens"
      },
      {
        "id": 1,
        "name": "Bob Jones"
      }
    ]
  }
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
      "aux": false,
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
      }
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
      "aux": false,
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
      }
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
    "aux": false,
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
    }
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
    "aux": false,
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
    }
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

# Stimulations

## Get All Stimulations

```shell
curl "https://api.haloneuro.com/v1/stimulations"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "organization_participant_id": "2",
    "waveform_id": "12",
    "start_time": "2015-08-12T14:12:14.000Z",
    "end_time": "2015-08-12T14:32:14.000Z"
  },
  {
    "id": 1,
    "organization_participant_id": "2",
    "waveform_id": "13",
    "start_time": "2015-08-12T15:12:14.000Z",
    "end_time": "2015-08-12T15:32:14.000Z"
  }
]
```

This endpoint retrieves all stimulations for a given user.
The user's access token must be passed in via the Authorization header.

### HTTP Request

`GET https://api.haloneuro.com/v1/stimulations`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
NA | NA | NA
NA | NA | NA

## Log A Stimulation Event

> This is the response from logging a stimulation event

```json
  {
    "id": 2,
    "organization_participant_id": "5",
    "waveform_id": "12",
    "start_time": "2015-06-11T12:05:23.800Z",
    "end_time": "2015-06-11T12:25:23.800Z"
  }
```
This endpoint should include the user token via the Authorization header.

### HTTP Request

`POST https://api.haloneuro.com/v1/stimulations`

### Body Parameters

Parameter | Default | Description
--------- | ------- | -----------
waveform_id | NA | valid waveform id
start_time | NA | datetime of stimulation starting (default is current time)
end_time | NA | datetime of stimulation ending (optional)
