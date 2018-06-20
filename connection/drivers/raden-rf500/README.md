# Raden RF500

![Raden RF500](picture.jpg)

![Device Type](https://img.shields.io/badge/Device%20Type-RadenRF500-blue.svg)

## Table of Contents <!-- omit in toc -->

- [Test Connection](#test-connection)
- [Get Information](#get-information)
- [Admins](#admins)
  - [Get Admins](#get-admins)
  - [Set Admins](#set-admins)
  - [Remove Admins](#remove-admins)
  - [Get Admin Authority](#get-admin-authority)
- [Users](#users)
  - [Get Users](#get-users)
  - [Set Users](#set-users)

## Test Connection

command: `test:connection`

> no params

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "type": "RadenRF500",
    "password": "123"
  },
  "command": "test:connection"
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "message": "Connection Successful"
}
```

## Get Information

command: `get:info`

> no params

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "type": "RadenRF500",
    "password": "123"
  },
  "command": "get:info"
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "info": {
    "result": "success",
    "time": "2018-06-19 10:53:21",
    "dev_id": "xxxxxxxxxxxxxxxx",
    "edition": "2.500.251",
    "volume": 0,
    "weigen": 0,
    "ip": "192.168.20.20",
    "gateway": "192.168.20.1",
    "netmask": "255.255.255.0",
    "mac": "xx:xx:xx:xx:xx:xx",
    "max_managernum": 8,
    "managernum": 0,
    "max_faceregist": 1000,
    "real_faceregist": 2,
    "max_facerecord": 100000,
    "real_facerecord": 4,
    "max_employee": 13000,
    "real_employee": 2,
    "max_finger": 2000,
    "real_finger": 0,
    "max_other": 10000,
    "real_other": 0,
    "type": "FA100",
    "alg_edition": "3.1",
    "managerlock": false
  }
}
```

## Admins

### Get Admins

command: `get:admins`

> no params

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "type": "RadenRF500",
    "password": "123"
  },
  "command": "get:admins"
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "admins": [
    {
      "id": 222,
      "name": "ardalan amini",
      "card_num": "xxxxxxxxxx",
      "pass_word": "",
      "enter_type": "face",
      "authority": 0,
      "face_data": [
        "xxx...", "xxx...", "xxx...", "xxx...",
        "xxx...", "xxx...", "xxx...", "xxx...",
        "xxx...", "xxx...", "xxx...", "xxx...",
        "xxx...", "xxx...", "xxx...", "xxx...",
        "xxx...", "xxx..."
      ]
    },
    ...
  ]
}
```

### Set Admins

command: `set:admins`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| admins | [Admin](#admin)[] | - |

#### Admin <!-- omit in toc -->

| Param | Type | Default | Description |
|:-----:|:----:|:-------:|:-----------:|
| id | [Number](number) | - | - |
| name | [String](string) | - | - |
| [authority] | `0` \| `1` | `1` | `0`: super administrator, `1`: normal administrator |
| [card_num] | [String](string) | `"0Xffffffff"` | - |
| [password] | [String](string) | `""` | - |
| face_data | [String](string)[] | - | `18` face templates |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "type": "RadenRF500",
    "password": "123"
  },
  "command": "set:admins",
  "params": {
    "admins": [
      {
        "id": 222,
        "name": "ardalan amini",
        "authority": 0,
        "face_data": [
          "xxx...", "xxx...", "xxx...", "xxx...",
          "xxx...", "xxx...", "xxx...", "xxx...",
          "xxx...", "xxx...", "xxx...", "xxx...",
          "xxx...", "xxx...", "xxx...", "xxx...",
          "xxx...", "xxx..."
        ]
      },
      ...
    ]
  }
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "message": "success"
}
```

### Remove Admins

command: `remove:admins`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| admins | [Number](number)[] | - |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "type": "RadenRF500",
    "password": "123"
  },
  "command": "remove:admins",
  "params": {
    "admins": [222, ...]
  }
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "message": "success"
}
```

### Get Admin Authority

command: `get:admin_authority`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| admin | [Number](number) | - |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "type": "RadenRF500",
    "password": "123"
  },
  "command": "get:admin_authority",
  "params": {
    "admin": 222
  }
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "authority": 0
}
```

## Users

### Get Users

command: `get:users`

> no params

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "type": "RadenRF500",
    "password": "123"
  },
  "command": "get:users"
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "users": [
    {
      "id": 1,
      "name": "ardalan amini",
      "authority": "0X11",
      "card_num": "xxxxxxxxxx",
      "check_type": "face",
      "opendoor_type": "face",
      "password": "",
      "alg_edition": "3.1",
      "sn": "xxxxxxxxxxxxxxxx",
      "photo": "xxx...",
      "face_data": [
        "xxx...", "xxx...", "xxx...", "xxx...",
        "xxx...", "xxx...", "xxx...", "xxx...",
        "xxx...", "xxx...", "xxx...", "xxx...",
        "xxx...", "xxx...", "xxx...", "xxx...",
        "xxx...", "xxx..."
      ]
    },
    ...
  ]
}
```

### Set Users

command: `set:users`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| users | [User](#user)[] | - |

#### User <!-- omit in toc -->

| Param | Type | Default | Description |
|:-----:|:----:|:-------:|:-----------:|
| id | [Number](number) | - | - |
| name | [String](string) | - | - |
| [authority] | `"0X11"` \| `"0X55"` \| `"0Xaa"` | `"0X55"` | `"0X11"`: Access control & Attendance, `"0X55"`: Attendance only, `"0Xaa"`: Access only |
| [card_num] | [String](string) | `"0Xffffffff"` | - |
| check_type | `"face"` \| `"card&face"` \| `"card"` \| `"num&password"` | - | - |
| opendoor_type | `"face"` \| `"card&face"` \| `"card"` \| `"num&password"` | - | - |
| [password] | [String](string) | `""` | - |
| [photo] | [String](string) | `""` | `base64` format |
| face_data | [String](string)[] | - | `18` face templates |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "type": "RadenRF500",
    "password": "123"
  },
  "command": "set:users",
  "params": {
    "users": [
      {
        "id": 1,
        "name": "ardalan amini",
        "authority": "0X11",
        "card_num": "xxxxxxxxxx",
        "check_type": "face",
        "opendoor_type": "face",
        "password": "",
        "alg_edition": "3.1",
        "sn": "xxxxxxxxxxxxxxxx",
        "photo": "xxx...",
        "face_data": [
          "xxx...", "xxx...", "xxx...", "xxx...",
          "xxx...", "xxx...", "xxx...", "xxx...",
          "xxx...", "xxx...", "xxx...", "xxx...",
          "xxx...", "xxx...", "xxx...", "xxx...",
          "xxx...", "xxx..."
        ]
      },
      ...
    ]
  }
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "message": "success"
}
```

[string]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String
[boolean]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean
[number]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number
[object]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object
