# API Errors

<!-- TOC -->

- [API Errors](#api-errors)
  - [Overview](#overview)
  - [Allowed Nest JS Exceptions](#allowed-nest-js-exceptions)
    - [401](#401)
      - [UnauthorizedException](#unauthorizedexception)
    - [500](#500)
      - [InternalServerException](#internalserverexception)
  - [Rules](#rules)

<!-- /TOC -->

## Overview

Summarizes the errors of AJK Town and their rules

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

## Rules

1. Do not use customized errors. Only use 
1. Do not use the full name `error`. Always use `err`