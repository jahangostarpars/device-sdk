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
  - [Remove Users](#remove-users)
  - [Enroll Users](#enroll-users)
  - [Get User Photo](#get-user-photo)
  - [Set User Photo](#set-user-photo)
- [Clockings](#clockings)
  - [Get Clockings](#get-clockings)
  - [Remove Clockings](#remove-clockings)
  - [Mark Clockings](#mark-clockings)
- [Datetime](#datetime)
  - [Get Datetime](#get-datetime)
  - [Set Datetime](#set-datetime)
- [Workcodes](#workcodes)
  - [Get Workcodes](#get-workcodes)
  - [Set Workcodes](#set-workcodes)
  - [Remove Workcodes](#remove-workcodes)
- [Workstatus](#workstatus)
  - [Get Workstatus](#get-workstatus)
  - [Set Workstatus](#set-workstatus)
  - [Remove Workstatus](#remove-workstatus)

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
| id | [Number][number] | - | - |
| name | [String][string] | - | - |
| [authority] | `0` \| `1` | `1` | `0`: super administrator, `1`: normal administrator |
| [card_num] | [String][string] | `"0Xffffffff"` | - |
| [password] | [String][string] | `""` | - |
| face_data | [String][string][] | - | `18` face templates |

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
| admins | [Number][number][] | - |

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
| admin | [Number][number] | - |

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

gets the given users from device, in case no param given or the users is an empty array it will get all users

command: `get:users`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| [users] | [Number][number][] | Users identification codes |

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
| id | [Number][number] | - | - |
| name | [String][string] | - | maximum `17` characters |
| [authority] | `"0X11"` \| `"0X55"` \| `"0Xaa"` | `"0X55"` | `"0X11"`: Access control & Attendance, `"0X55"`: Attendance only, `"0Xaa"`: Access only |
| [card_num] | [String][string] | `"0Xffffffff"` | - |
| check_type | `"face"` \| `"card&face"` \| `"card"` \| `"num&password"` | - | - |
| opendoor_type | `"face"` \| `"card&face"` \| `"card"` \| `"num&password"` | - | - |
| [password] | [String][string] | `""` | - |
| [photo] | [String][string] | `""` | `base64` format |
| face_data | [String][string][] | - | `18` face templates |

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

### Remove Users

removes the given users from device, in case no param given or the users is an empty array it will remove all users

command: `remove:users`

| Param | Type | default | Description |
|:-----:|:----:|:-------:|:-----------:|
| [users] | [Number][number][] | `[]` | Users identification codes |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "type": "RadenRF500",
    "password": "123"
  },
  "command": "remove:users",
  "params": {
    "users": [222, ...]
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

### Enroll Users

command: `enroll:users`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| users | [User](#user-to-enroll)[] | - |

#### User to enroll <!-- omit in toc -->

| Param | Type | Default | Description |
|:-----:|:----:|:-------:|:-----------:|
| id | [Number][number] | - | - |
| name | [String][string] | - | maximum `17` characters |
| [authority] | `"0X11"` \| `"0X55"` | `"0X55"` | `"0X11"`: Access control & Attendance, `"0X55"`: Attendance only |
| [dutyrule] | `1` \| `2` \| `3` \| `4` \| `5` \| `6` \| `7` \| `8` \| `9` \| `10` \| `11` | `1` | `1`: Face, `2`: Card, `3`: Card and Photo, `4`: Card and Face, `5`: ID and Face, `6`: Card or Face, `7`: Card or Pin, `8`: ID and Pin, `9`: Face and Fingerprint, `10`: Face or Fingerprint, `11`: Fingerprint |
| [photo] | [Boolean](boolean) | `false` | `true`: Capture head photo, `false`: Don‟t capture head photo |
| [save] | `1` \| `2` \| `3` | `1` | `1`: Only save user data to the device, `2`: Only send back user data to PC, `3`: Save user data to the device and send back user data to PC |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "type": "RadenRF500",
    "password": "123"
  },
  "command": "enroll:users",
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

### Get User Photo

command: `get:user_photo`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| user | [Number][number] | User's identification code |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "type": "RadenRF500",
    "password": "123"
  },
  "command": "get:user_photo",
  "params": {
    "user": 1
  }
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "photo": "xxx..."
}
```

### Set User Photo

command: `set:user_photo`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| user | [Number][number] | User's identification code |
| photo | [String][string] | `base64` format |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "type": "RadenRF500",
    "password": "123"
  },
  "command": "set:user_photo",
  "params": {
    "user": 1,
    "photo": "xxx..."
  }
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "message": "Successful"
}
```

## Clockings

### Get Clockings

command: `get:clockings`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| [from] | [String][string] | date (`YYYY-MM-DD`) |
| [to] | [String][string] | date (`YYYY-MM-DD`) |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "type": "RadenRF500",
    "password": "123"
  },
  "command": "get:clockings",
  "params": {
    "from": "2018-06-01",
    "to": "2018-06-17"
  }
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "dev_id": "xxxxxxxxxxxxxxxx",
  "total": x,
  "message": "success",
  "clockings": [
    {
      "user_id": 1,
      "name": "ardalan amini",
      "datetime": "2018-06-01 08:00:00",
      "workcode": x,
      "status": x,
      "authority": "0X11",
      "card_src": "from_check"
    },
    ...
  ]
}
```

### Remove Clockings

command: `remove:clockings`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| [from] | [String][string] | date (`YYYY-MM-DD`) |
| [to] | [String][string] | date (`YYYY-MM-DD`) |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "type": "RadenRF500",
    "password": "123"
  },
  "command": "remove:clockings",
  "params": {
    "from": "2018-06-01",
    "to": "2018-06-17"
  }
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "message": "Successful"
}
```

### Mark Clockings

Removes device's sended clockings

command: `mark:clockings`

> no params

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "type": "RadenRF500",
    "password": "123"
  },
  "command": "mark:clockings"
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "message": "Successful"
}
```

## Datetime

### Get Datetime

command: `get:datetime`

> no params

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "type": "RadenRF500",
    "password": "123"
  },
  "command": "get:datetime"
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "datetime": "2018-07-14 12:03:50"
}
```

### Set Datetime

command: `set:datetime`

| Param | Type | Default | Description |
|:-----:|:----:|:-------:|:-----------:|
| [datetime] | [String][string] | now | `YYYY-MM-DD HH:mm:ss` |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "type": "RadenRF500",
    "password": "123"
  },
  "command": "set:datetime"
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "message": "Successful"
}
```

## Workcodes

### Get Workcodes

command: `get:workcodes`

> no params

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "type": "RadenRF500",
    "password": "123"
  },
  "command": "get:workcodes"
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "workcodes": [
    {
      "id": 1,
      "name": "normal"
    },
    ...
  ]
}
```

### Set Workcodes

command: `set:workcodes`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| workcodes | [Workcode](#workcode)[] | - |

#### Workcode <!-- omit in toc -->

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| id | [Number][number] | - |
| name | [String][string] | - |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "type": "RadenRF500",
    "password": "123"
  },
  "command": "set:workcodes",
  "params": {
    "workcodes": [
      {
        "id": 1,
        "name": "normal"
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
  "message": "Successful"
}
```

### Remove Workcodes

command: `remove:workcodes`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| workcodes | [Number][number][] | workcode ids |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "type": "RadenRF500",
    "password": "123"
  },
  "command": "remove:workcodes",
  "params": {
    "workcodes": [1, ...]
  }
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "message": "Successful"
}
```

## Workstatus

### Get Workstatus

command: `get:workstatus`

> no params

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "type": "RadenRF500",
    "password": "123"
  },
  "command": "get:workstatus"
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "workstatus": [
    {
      "id": 1,
      "name": "in"
    },
    ...
  ]
}
```

### Set Workstatus

command: `set:workstatus`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| workstatus | [Workstatus Object](#workstatus-object)[] | - |

#### Workstatus Object <!-- omit in toc -->

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| id | [Number][number] | - |
| name | [String][string] | - |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "type": "RadenRF500",
    "password": "123"
  },
  "command": "set:workstatus",
  "params": {
    "workstatus": [
      {
        "id": 1,
        "name": "in"
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
  "message": "Successful"
}
```

### Remove Workstatus

command: `remove:workstatus`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| workstatus | [Number][number][] | workcode ids |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "type": "RadenRF500",
    "password": "123"
  },
  "command": "remove:workstatus",
  "params": {
    "workstatus": [1, ...]
  }
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "message": "Successful"
}
```

[string]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String
[boolean]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean
[number]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number
[object]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object
