# Raden T41

![Device Type](https://img.shields.io/badge/Device%20Type-RadenT41-blue.svg)

## Table of Contents <!-- omit in toc -->

- [Test Connection](#test-connection)
- [Information](#information)
- [Users](#users)
  - [Get](#get)
  - [Set](#set)
  - [Remove](#remove)

## Test Connection

command: `test:connection`

> no params

**Example Request**:

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

**Example Response**:

```http
HTTP/1.1 200 Ok

{
  "message": "Connection Successful"
}
```

## Information

command: `get:info`

> no params

**Example Request**:

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

**Example Response**:

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

### Get

command: `get:users`

> no params

**Example Request**:

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

**Example Response**:

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

### Set

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

**Example Request**:

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

**Example Response**:

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

### Remove

removes the given users from device, in case no param given it will remove all users

command: `remove:users`

**User object**:

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| [users] | [Number](number)[] | Users identification codes |

**Example Request**:

```json
{
  "users": [222, ...]
}
```

**Example Response**:

```http
HTTP/1.1 200 Ok

{
  "message": "SUCCESSFUL"
}
```

[string]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String
[boolean]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean
[number]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number
[object]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object
