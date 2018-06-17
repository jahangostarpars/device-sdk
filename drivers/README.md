# General

![SDK Port](https://img.shields.io/badge/SDK%20Port-8020-brightgreen.svg)

## Table of Contents <!-- omit in toc -->

- [Urls](#urls)
  - [Request](#request)
  - [Example Request](#example-request)
  - [Example Responses](#example-responses)

## Urls

- <http://localhost:8020/v1/connect> (`POST`)

### Request

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| device | [`Device`](#device) | Target device |
| command | [`String`](string) | The request you want to send to the device |
| [params] | [`Object`](object) | Parameters that are neede to handle the request |

#### Device <!-- omit in toc -->

| Param | Type | default | Description |
|:-----:|:----:|:-------:|:-----------:|
| type | [`RadenT41`](raden-drivers/raden-t41.md) \| [`RadenRF500`](drivers/raden-rf500.md) \| [`V800`](drivers/v800.md) | - | device type |
| host | [`String`](string) | - | device address |
| port | [`Number`](number) | - | device port |
| [username] | [`String`](string) | "admin" | device network username |
| [password] | [`String`](string) | - | device network password |

### Example Request

```json
{
  "device": {
    "host": "192.168.20.20",
    "port": 8080,
    "type": "RadenT41",
    "username": "admin",
    "password": "123"
  },
  "command": "test:connection"
}
```

### Example Responses

```http
HTTP/1.1 500 Internal Server Error

{
  "message": "Connection Failed"
}
```

```http
HTTP/1.1 401 Unauthorized

{
  "message": "Authentication Failed"
}
```

[string]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String
[number]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number
[object]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object
