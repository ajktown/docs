# API Errors

<!-- TOC -->

- [API Errors](#api-errors)
  - [Overview](#overview)
  - [Fundamental Goals](#fundamental-goals)
  - [Rules](#rules)
    - [Do not directly throw nest js exceptions](#do-not-directly-throw-nest-js-exceptions)
  - [How Errors should be selected](#how-errors-should-be-selected)

<!-- /TOC -->

## Overview

Nest JS offers [Nest JS managed/defined errors](https://docs.nestjs.com/exception-filters#built-in-http-exceptions) and AJK Town takes advantages of it. [^1]

Yet, to avoid inconsistent error messages, we have to follow some strict rules.

[^1]: Any nest js defined errors will be automatically caught by nest js. No need to define error filters for them.

## Fundamental Goals

1. Throw messages must be consistent

1. Throwing messages must be easily modifiable

1. Should be independent from nest js defined errors

1. But still should take advantages of nest js defined errors

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

Directly extended to the nest js defined exception error must be defined a file name `index.error.ts` of a directory 
`400`, `401`, `403` and so on...
```
errors
├── 400
│   └── index.error.ts
│   └── some-kind-of-bad-request.error.ts
│   └── another-kind-of-bad-request.error.ts
└── 403
    └── index.error.ts
    └── some-kind-of-forbidden.error.ts
```

Customized Error must then extend index.error.ts containing error.
```ts
// Notice that it extends BadRequestError, not BadRequestException. Customized Error must extend only the 
// AJK TOWN defined "BadRequestError", that extends BadRequestException.\
export class SomeKindOfBadRequest extends BadRequestError {
  constructor(singInMethod: string) {
    // i.e) Something went wrong while we are signing you in with the following method: Google
    super(
      `Something went wrong while we are signing you in with the following method: ${singInMethod}`,
    )
  }
}
```

Then we can throw our own exceptions like this
```ts
throw new SomeKindOfBadRequest('Google')
```

do NOT throw nest js defined error like this[^2]
```ts
throw new BadRequestException('Something went wrong while we are signing you in with the following method: Google')
```
[^2]: This is not great, because we can't reuse the error message. If we want to change the error message, we have to change it everywhere.

## How Errors should be selected

1. Check which http status code is appropriate for the error

1. Try to select already-present AJK Town API defined errors.

1. If there is no appropriate error, instead of defining a new error, try to use non-categorized errors of index.error.ts

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