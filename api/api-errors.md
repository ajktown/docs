# API Errors

<!-- TOC -->

- [API Errors](#api-errors)
  - [Overview](#overview)
  - [Rules](#rules)
    - [Do not directly throw nest js exceptions](#do-not-directly-throw-nest-js-exceptions)
  - [How Errors should be selected](#how-errors-should-be-selected)

<!-- /TOC -->

## Overview

Nest JS offers [Nest JS managed/defined errors](https://docs.nestjs.com/exception-filters#built-in-http-exceptions) and AJK Town takes advantages of it. [^1]

Yet, to avoid inconsistent error messages, we have to follow some strict rules.

[^1]: Any nest js defined errors will be automatically caught by nest js. No need to define error filters for them.

## Rules


### Do not directly throw nest js exceptions
By extending nest js exception, we can define our own errors.
We name our exceptions with suffix `Error`, so we know that we only throw our own exceptions.
```ts
export class DataNotPresentError extends BadRequestException {
  constructor(dataType: string, optional?: PrivateOptional) {
    const messageSuffix = optional.isPlural
      ? 'are not present'
      : 'is not present'
    super(`${dataType} ${messageSuffix}`) // i.e) User email is not present
  }
}
```


Then we can throw our own exceptions like this 
```ts
throw new DataNotPresentError('User email')
```

do NOT throw errors like this[^2]
```ts
throw new BadRequestException('User email is not present')
```
[^2]: This is not great, because we can't reuse the error message. If we want to change the error message, we have to change it everywhere.

## How Errors should be selected

1. Check which http status code is appropriate for the error

1. Try to select already-present AJK Town API defined errors.

1. If there is no appropriate error, instead of defining a new error, try to use non-categorized errors

```ts
// TODO: Anything that is not standardized should be thrown with this exception.
export class BadRequestError extends BadRequestException {
  constructor(message: string) {
    super(message)
  }
}
```

The above is clear that it is not categorized, with params `message` is just simply set for `super()`[^3][^4]

[^3]: If it was customized one, it would have strict message rules. But the class does not have such rules and simply pass the message.

[^4]: We are doing this so that if there are common errors message that we can reuse, we can define new error afterward.