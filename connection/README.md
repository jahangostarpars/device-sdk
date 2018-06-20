# General

![SDK Version](https://img.shields.io/badge/SDK%20Version-v1-brightgreen.svg)
![SDK Port](https://img.shields.io/badge/SDK%20Port-8020-brightgreen.svg)

## Table of Contents <!-- omit in toc -->

- [Urls](#urls)

## Urls

- <http://localhost:8020/v1/connect> (`POST`)

| Param | Type | Description |
|:-----:|:----:|:-----------:|
| device | [`Device`](#device) | Target device |
| command | [`String`](string) | The request you want to send to the device |
| [params] | [`Object`](object) | Parameters that are needed to handle the request |

### Device <!-- omit in toc -->

| Param | Type | default | Description |
|:-----:|:----:|:-------:|:-----------:|
| type | [`V800`](drivers/v800/README.md) \| [`RadenT41`](drivers/raden-t41/README.md) \| [`RadenRF500`](drivers/raden-rf500/README.md) \| [`RadenRF600`](drivers/raden-rf600/README.md) \| [`RadenRF620`](drivers/raden-rf620/README.md) \| [`RadenRF800`](drivers/raden-rf800/README.md) \| [`RadenRF900`](drivers/raden-rf900/README.md) | - | device type |
| host | [`String`](string) | - | device address |
| [port] | [`Number`](number) | V800: `5010` \| RadenT41: `8080` \| RadenRF series: `9922` | device port |
| [username] | [`String`](string) | "admin" | device network username |
| [password] | [`String`](string) | - | device network password |

*Example Request*:

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

*Example Responses*:

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
