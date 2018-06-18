# Raden T41

![Device Type](https://img.shields.io/badge/Device%20Type-RadenT41-blue.svg)

## Table of Contents <!-- omit in toc -->

- [Test Connection](#test-connection)
- [Get Information](#get-information)
- [Users](#users)
  - [Get Users](#get-users)
  - [Set Users](#set-users)
  - [Remove Users](#remove-users)
- [Clockings](#clockings)
  - [Get Clockings](#get-clockings)
  - [Remove Clockings](#remove-clockings)
  - [Mark Clockings](#mark-clockings)
- [Cards](#cards)
  - [Get Cards](#get-cards)
  - [Set Cards](#set-cards)
  - [Remove Cards](#remove-cards)
  - [Mark Cards](#mark-cards)
  - [Register Cards](#register-cards)
- [Fingerprints](#fingerprints)
  - [Get Fingerprints](#get-fingerprints)
  - [Set Fingerprints](#set-fingerprints)
  - [Remove Fingerprints](#remove-fingerprints)
  - [Mark Fingerprints](#mark-fingerprints)
- [Meals](#meals)
  - [Set Meals](#set-meals)
- [Foods](#foods)
  - [Get Foods](#get-foods)
  - [Set Fingerprints](#set-fingerprints)
  - [Remove Fingerprints](#remove-fingerprints)
  - [Mark Fingerprints](#mark-fingerprints)
- [Passwords](#passwords)
- [Settings](#settings)
- [Datetime](#datetime)
- [Others](#others)

## Test Connection

command: `test:connection`

> no params

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "port": 8080,
    "type": "RadenT41",
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
    "port": 8080,
    "type": "RadenT41",
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
    "adapter": true,
    "battery_level": 0,
    "battery": true,
    "cards": 1,
    "fingers": 95,
    "clockings": 6973,
    "id": "7b383834-6666-3837-352d-343337312d34",
    "name": "raden",
    "firmware": "1.0.38",
    "memory_available": 892480,
    "memory_size": 960504,
    "memory_used": 19232
  }
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
    "port": 8080,
    "type": "RadenT41",
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
      "allow_card": true,
      "allow_code": false,
      "allow_finger": true,
      "code": 222,
      "first_name": "اردلان",
      "full_name": "آقای اردلان امینی",
      "last_name": "امینی",
      "sex": "male",
      "verify_card": false
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

| Param | Type | default | Description |
|:-----:|:----:|:-------:|:-----------:|
| code | [Number](number) | - | User's identification code |
| first_name | [String](string) | - | - |
| last_name | [String](string) | - | - |
| [sex] | `male` \| `female` | `male` | User's gender |
| [allow_finger] | [Boolean](boolean) | `false` | Indicates permission for authentication this user by fingerprint |
| [allow_card] | [Boolean](boolean) | `false` | Indicates permission for authentication this user by card |
| [allow_code] | [Boolean](boolean) | `false` | Indicates permission for authentication this user by code |
| [verify_card] | [Boolean](boolean) | `false` | Indicates require authenticate card before authentication by fingerprint |
| [username] | [String](string) | - | - |
| [password] | [String](string) | - | - |
| [shift_length] | [Number](number) | `0` | - |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "port": 8080,
    "type": "RadenT41",
    "password": "123"
  },
  "command": "set:users",
  "params": {
    "users": [
      {
        "code": 222,
        "first_name": "اردلان",
        "last_name": "امینی",
        "allow_finger": true,
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
  "users": [
    {
      "allow_card": true,
      "allow_code": false,
      "allow_finger": true,
      "code": 222,
      "first_name": "اردلان",
      "full_name": "آقای اردلان امینی",
      "last_name": "امینی",
      "sex": "male",
      "verify_card": false
    },
    ...
  ]
}
```

### Remove Users

removes the given users from device, in case no param given it will remove all users

command: `remove:users`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| [users] | [Number](number)[] | Users identification codes |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "port": 8080,
    "type": "RadenT41",
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
  "message": "SUCCESSFUL"
}
```

## Clockings

### Get Clockings

command: `get:clockings`

| Param | Type | default | Description |
|:-----:|:----:|:-------:|:-----------:|
| [sended] | [Boolean](boolean) | `false` | Get clockings that are already sent |
| [from] | [String](string) | - | date or datetime (`YYYY-MM-DD HH:mm:ss`) |
| [to] | [String](string) | - | date or datetime (`YYYY-MM-DD HH:mm:ss`) |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "port": 8080,
    "type": "RadenT41",
    "password": "123"
  },
  "command": "get:clockings",
  "params": {
    "sended": true,
    "from": "2018-06-01",
    "to": "2018-06-17 23:59:59",
  }
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "clockings": [
    {
      "changed": false,
      "code": 222,
      "datetime": "2017-12-16T13:14:37",
      "factor": 1,
      "id": 31762,
      "io": 1,
      "reason": 55
    },
    ...
  ]
}
```

### Remove Clockings

removes the clockings from the device in the given time range, in case no params given it will remove all clockings

command: `remove:clockings`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| [from] | [String](string) | date or datetime (`YYYY-MM-DD HH:mm:ss`) |
| [to] | [String](string) | date or datetime (`YYYY-MM-DD HH:mm:ss`) |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "port": 8080,
    "type": "RadenT41",
    "password": "123"
  },
  "command": "remove:clockings",
  "params": {
    "from": "2018-06-01",
    "to": "2018-06-17 23:59:59"
  }
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "message": "SUCCESSFUL"
}
```

### Mark Clockings

command: `mark:clockings`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| [clockings] | [Number](number)[] | Clockings ids |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "port": 8080,
    "type": "RadenT41",
    "password": "123"
  },
  "command": "mark:clockings",
  "params": {
    "clockings": [31762, ...],
  }
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "message": "SUCCESSFUL"
}
```

## Cards

### Get Cards

gets the cards for given users from device, in case no param given it will get all cards

command: `get:cards`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| [users] | [Number](number)[] | Users identification codes |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "port": 8080,
    "type": "RadenT41",
    "password": "123"
  },
  "command": "get:cards",
  "params": {
    "users": [222, ...],
  }
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "cards": [
    {
      "card_id": "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}",
      "code": 222,
      "id": 3,
      "last_update": "2017-02-20T12:25:44"
    },
    ...
  ]
}
```

### Set Cards

command: `set:cards`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| cards | [Card](#card)[] | - |

#### Card <!-- omit in toc -->

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| code | [Number](number) | User's identification code |
| card_id | [String](string) | - |
| last_update | [String](string) | datetime |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "port": 8080,
    "type": "RadenT41",
    "password": "123"
  },
  "command": "set:cards",
  "params": {
    "cards": [
      {
        "card_id": "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}",
        "code": 222,
        "last_update": "2017-02-20 12:25:44"
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
  "message": "SUCCESSFUL"
}
```

### Remove Cards

removes the cards for the given users from device, in case no param given it will remove all cards

command: `remove:cards`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| [users] | [Number](number)[] | Users identification codes |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "port": 8080,
    "type": "RadenT41",
    "password": "123"
  },
  "command": "remove:cards",
  "params": {
    "users": [222, ...]
  }
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "message": "SUCCESSFUL"
}
```

### Mark Cards

command: `mark:cards`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| cards | [Number](number)[] | Cards ids |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "port": 8080,
    "type": "RadenT41",
    "password": "123"
  },
  "command": "mark:cards",
  "params": {
    "cards": [3, ...]
  }
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "message": "SUCCESSFUL"
}
```

### Register Cards

command: `register:card`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| user | [Number](number) | User Identification code |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "port": 8080,
    "type": "RadenT41",
    "password": "123"
  },
  "command": "register:card",
  "params": {
    "user": 222
  }
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "message": "SUCCESSFUL"
}
```

## Fingerprints

### Get Fingerprints

gets the fingerprints for given users from device, in case no param given it will get all fingerprints

command: `get:fingerprints`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| [users] | [Number](number)[] | Users identification codes |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "port": 8080,
    "type": "RadenT41",
    "password": "123"
  },
  "command": "get:fingerprints",
  "params": {
    "users": [222, ...],
  }
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "fingerprints": [
    {
      "code": 222,
      "finger_id": 1,
      "finger_number": 1,
      "finger_template": "xxxx...",
      "id": 381
    },
    ...
  ]
}
```

### Set Fingerprints

command: `set:fingerprints`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| fingerprints | [Fingerprint](#fingerprint)[] | - |

#### Fingerprint <!-- omit in toc -->

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| code | [Number](number) | User's identification code |
| finger_number | [Number](number) | - |
| finger_template | [String](string) | - |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "port": 8080,
    "type": "RadenT41",
    "password": "123"
  },
  "command": "set:fingerprints",
  "params": {
    "fingerprints": [
      {
        "code": 222,
        "finger_number": 6,
        "finger_template": "xxx...",
      },
      ...
    ],
  }
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "message": "SUCCESSFUL"
}
```

### Remove Fingerprints

removes the fingerprints for given users from device, in case no param given it will remove all fingerprints

command: `remove:fingerprints`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| [users] | [Number](number)[] | Users identification codes |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "port": 8080,
    "type": "RadenT41",
    "password": "123"
  },
  "command": "remove:fingerprints",
  "params": {
    "users": [222, ...],
  }
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "message": "SUCCESSFUL"
}
```

### Mark Fingerprints

command: `mark:fingerprints`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| fingerprints | [Number](number)[] | fingerprints ids |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "port": 8080,
    "type": "RadenT41",
    "password": "123"
  },
  "command": "mark:fingerprints",
  "params": {
    "fingerprints": [381, ...]
  }
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "message": "SUCCESSFUL"
}
```

## Meals

### Set Meals

command: `set:meals`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| meals | [Meal](#meal)[] | - |

#### Meal <!-- omit in toc -->

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| meal_id | [Number](number) | - |
| name | [String](string) | - |
| due_time | [String](string) | time in `HH:mm` format |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "port": 8080,
    "type": "RadenT41",
    "password": "123"
  },
  "command": "set:meals",
  "params": {
    "meals": [
      {
        "meal_id": 128,
        "name": "صبحانه",
        "due_time": "07:00",
      },
      ...
    ],
  }
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "message": "SUCCESSFUL"
}
```

## Foods

### Get Foods

gets the foods for given users from device, in case no param given it will get all foods

command: `get:foods`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| [meal_id] | [Number](number)[] | - |
| [from] | [String](string) | - | date or datetime (`YYYY-MM-DD HH:mm:ss`) |
| [to] | [String](string) | - | date or datetime (`YYYY-MM-DD HH:mm:ss`) |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "port": 8080,
    "type": "RadenT41",
    "password": "123"
  },
  "command": "get:foods",
  "params": {
    "meal_id": 128,
  }
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "foods": [
    {
      "code" : 222,
      "datetime" : "2014-11-18T15:43:05",
      "id" : 1,
      "meal_id" : 1
    },
    ...
  ]
}
```

### Set Foods

command: `set:foods`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| foods | [Food](#food)[] | - |

#### Food <!-- omit in toc -->

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| code | [Number](number) | User's identification code |
| meal_id | [Number](number) | - |
| datetime | [String](string) | datetime (`YYYY-MM-DD HH:mm:ss`) |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "port": 8080,
    "type": "RadenT41",
    "password": "123"
  },
  "command": "set:foods",
  "params": {
    "foods": [
      {
        "code" : 222,
        "datetime" : "2018-06-18 15:43:05",
        "meal_id" : 128
      },
      ...
    ],
  }
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "message": "SUCCESSFUL"
}
```

### Remove Foods

removes the foods for given users from device, in case no param given it will remove all foods

command: `remove:foods`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| [from] | [String](string) | date or datetime (`YYYY-MM-DD HH:mm:ss`) |
| [to] | [String](string) | date or datetime (`YYYY-MM-DD HH:mm:ss`) |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "port": 8080,
    "type": "RadenT41",
    "password": "123"
  },
  "command": "remove:foods"
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "message": "SUCCESSFUL"
}
```

### Mark Foods

command: `mark:foods`

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| foods | [Number](number)[] | foods ids |

*Example Request*:

```json
{
  "device": {
    "host": "192.168.20.20",
    "port": 8080,
    "type": "RadenT41",
    "password": "123"
  },
  "command": "mark:foods",
  "params": {
    "foods": [1, ...]
  }
}
```

*Example Response*:

```http
HTTP/1.1 200 Ok

{
  "message": "SUCCESSFUL"
}
```

## Passwords

## Settings

## Datetime

## Others

[string]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String
[boolean]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean
[number]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number
[object]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object
