# General

SDK port: `8020`

## Table of Contents <!-- omit in toc -->

- [Urls](#urls)
  - [Request](#request)
    - [Device](#device)
  - [Example Request](#example-request)
  - [Example Responses](#example-responses)

## Urls

- <http://localhost:8020/v1/connect> (`POST`)

### Request

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| device | [`Device`](#Device) | Target device |
| command | [`String`](string) | The request you want to send to the device |
| [params] | [`Object`](object) | Parameters that are neede to handle the request |

#### Device

| Param | Type | default | Description |
|:-----:|:----:|:-------:|:-----------:|
| type | [`RadenT41`](raden-t41) \| [`RadenRF500`](raden-rf500) \| [`V800`](v800) | - | device type |
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

[raden-t41]: ./raden-t41.md
[raden-rf500]: ./raden-rf500.md
[v800]: ./v800.md

[string]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String
[number]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number
[object]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object
