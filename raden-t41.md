# Raden T41

device type: `RadenT41`

## Table of Contents <!-- omit in toc -->

- [Test Connection](#test-connection)
- [Device Information](#device-information)

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

## Device Information

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
