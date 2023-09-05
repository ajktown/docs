# Domain Driven Design

<!-- TOC -->

- [Domain Driven Design](#domain-driven-design)
  - [Overview](#overview)
  - [Constructor](#constructor)
    - [build~Constructor Method](#buildconstructor-method)
    - [Private Constructor](#private-constructor)
    - [get functions](#get-functions)
  - [Static](#static)
    - [fromRawDangerously()](#fromrawdangerously)
    - [fromPostDto() PRIVATE](#frompostdto-private)
    - [fromMdbByAtd()](#frommdbbyatd)
    - [fromMdb()](#frommdb)
  - [Non-Static](#non-static)
    - [post()](#post)
    - [toDoc() PRIVATE](#todoc-private)
    - [toResDTO()](#toresdto)
    - [insert~()](#insert)
    - [updateWith~()](#updatewith)
    - [update() PRIVATE](#update-private)
    - [delete()](#delete)

<!-- /TOC -->

## Overview

How AJK Town defines `Domain Driven Design`.

Always make sure that the order of methods follow exactly the same as the order below.


## Constructor

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

### fromRawDangerously()

Deprecated method that is usually used by the test.

Try to delete it as much as possible.


### fromPostDto() PRIVATE

Return Domain with given DTO (atd is required to write who created the domain)

It is usually private because it is directly called by post() method.

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

Returns WordDomain after saving into persistence.

It uses `fromPostDto()` and `toDocument()` methods to save into persistence.

### toDoc() PRIVATE

Returns doc type data that can be saved into persistence.

It is usually private because it is directly called by post() method.


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
