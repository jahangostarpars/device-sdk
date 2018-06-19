# Raden RF500

![Raden RF500](picture.jpg)

![Device Type](https://img.shields.io/badge/Device%20Type-RadenRF500-blue.svg)

## Table of Contents <!-- omit in toc -->

- [Test Connection](#test-connection)
- [Get Information](#get-information)

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

[string]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String
[boolean]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean
[number]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number
[object]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object
