# Domain Driven Design

<!-- TOC -->

- [Domain Driven Design](#domain-driven-design)
  - [Overview](#overview)
  - [Target Audience](#target-audience)
  - [Constructor](#constructor)
    - [withDefault](#withdefault)
    - [build~Constructor Method](#buildconstructor-method)
    - [Private Constructor](#private-constructor)
    - [get functions](#get-functions)
  - [Static](#static)
    - [underDevEnv()](#underdevenv)
    - [getDefault()](#getdefault)
    - [fromRawDangerously()](#fromrawdangerously)
    - [fromMdbByAtd()](#frommdbbyatd)
    - [fromMdb()](#frommdb)
  - [Non-Static](#non-static)
    - [post()](#post)
    - [toResDTO()](#toresdto)
    - [insert~()](#insert)
    - [updateWith~()](#updatewith)
    - [update() PRIVATE](#update-private)
    - [delete()](#delete)

<!-- /TOC -->

## Overview

How AJK Town defines `Domain Driven Design`.

Always make sure that the order of methods follow exactly the same as the order below.

## Target Audience
If you develop domain in AJK Town API, you should understand and follow the conventions below.


## Constructor


### withDefault
Returns the domain with default values, with given props.
Always used by the private constructor.

### build~Constructor Method

To maintain consistency, privateConstructor may have its own methods to create the domain.

i.e buildIdConstructor => builds id for the domain inside the constructor.

And this method is private / non-static

### Private Constructor
```ts
private constructor(props: Partial<IObject>, atd: AccessTokenDomain) {
  this.props.id = this.buildIdConstructor(props.code, atd)
  this.props = props
}
```
### get functions
```ts
get property() {
  return this.props.property
}
```


## Static

### underDevEnv()

Method only used under development environment. non-dev environment will throw an error.

### getDefault()
Returns the basic domain with default values.
Usually used when end user has no data yet.

### fromRawDangerously()

Deprecated method that is usually used by the test.

Try to delete it as much as possible.


### fromMdbByAtd()

Some of the resources like `support` or `preference` are automatically created by the system.

This method is used to create the domain with the given atd, acquired by successfully signed in user.

Usually the system checks the following thing
- If it does not exist => Create a new one
- If it is more than 1 => Error => Leave the first one as the valid one and delete the rest of them

Usually it depends on `fromMdb` method to finally return domain with either newly-created data or existing data.



### fromMdb()

Usually takes Document type data and return domain.

this can be also `fromPersistence()` but then `fromMdb()` was chosen for its short method name

## Non-Static

### post()

Returns Domain after saving into persistence with given atd, dto and model.

It uses `fromPostDto()` and `toDocument()` methods to save into persistence.

```ts
async post(
  atd: AccessTokenDomain,
  dto: PostSharedResourceDTO,
  model: SharedResourceModel,
): Promise<SharedResourceDomain> {
  return SharedResourceDomain.fromMdb(
    await new model({
      ownerId: atd.userId,
      expireInSecs: dto.expireInSecs,
      wordId: dto.wordId,
    }).save(),
  )
}
```


### toResDTO()

Returns the properties of the domain, only the data that end user can see.

Certain hidden data won't be visible to the user.

### insert~()

Unlike Update methods, it simply modifies the data without modifying the persistence.

### updateWith~()

Updates as the properties. Any name can be given with the tilda(~) sign.


Examples:
- updateWithPostedWord
- updateWithPutDto
- updateWithDeletedWord


### update() PRIVATE

Updates as the properties of the domain to the persistence.

It is usually private as it is called by other update functions such as `updateFrom~()`


### delete()

Deletes the domain from the persistence.

the method contains access control to prevent unauthorized access.
