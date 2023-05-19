# API Errors

<!-- TOC -->

- [API Errors](#api-errors)
  - [Overview](#overview)
  - [Rules and Suggestions](#rules-and-suggestions)
  - [Allowed Nest JS Exceptions](#allowed-nest-js-exceptions)
    - [401](#401)
      - [UnauthorizedException](#unauthorizedexception)
    - [500](#500)
      - [InternalServerException](#internalserverexception)

<!-- /TOC -->

## Overview

Summarizes the errors of AJK Town and their rules.


## Rules and Suggestions

1. Please use the standard nest js provided exceptions as much as possible.

1. Please follow the same responses type, if you need to make a customized exceptions.


## Allowed Nest JS Exceptions

Please write in alphabetic order

### 401
#### UnauthorizedException
```json
{
    "response": {
        "statusCode": 401,
        "message": "Unauthorized"
    },
    "status": 401,
    "options": {},
    "message": "Unauthorized",
    "name": "UnauthorizedException"
}
```

### 500
#### InternalServerException

```json
{
    "response": {
        "statusCode": 500,
        "message": "Internal Server Error"
    },
    "status": 500,
    "options": {},
    "message": "Internal Server Error",
    "name": "InternalServerErrorException"
}
```

