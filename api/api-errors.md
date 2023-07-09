# API Errors

<!-- TOC -->

- [API Errors](#api-errors)
  - [Overview](#overview)
  - [Rules](#rules)
    - [Do not directly throw nest js errors](#do-not-directly-throw-nest-js-errors)

<!-- /TOC -->

## Overview

Nest JS offers [Nest JS managed/defined errors](https://docs.nestjs.com/exception-filters#built-in-http-exceptions) and AJK Town takes advantages of it. [^1]

Yet, to avoid inconsistent error messages, we have to follow some strict rules.

[^1]: Any nest js defined errors will be automatically caught by nest js. No need to define error filters for them.

## Rules


### Do not directly throw nest js errors
By extending nest js errors, we can define our own errors.

```ts
export class DataNotPresentException extends BadRequestException {
  constructor(dataType: string, optional?: PrivateOptional) {
    const messageSuffix = optional.isPlural
      ? 'are not present'
      : 'is not present'
    super(`${dataType} ${messageSuffix}`) // i.e) User email is not present
  }
}
```


Then we can throw errors 
```ts
throw new DataNotPresentException('User email')
```

do NOT throw errors like this[^2]
```ts
throw new BadRequestException('User email is not present')
```
[^2]: This is not great, because we can't reuse the error message. If we want to change the error message, we have to change it everywhere.
