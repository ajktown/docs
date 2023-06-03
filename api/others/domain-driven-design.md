# Domain Driven Design

<!-- TOC -->

- [Domain Driven Design](#domain-driven-design)
  - [Order](#order)
  - [Every domain has the following methods](#every-domain-has-the-following-methods)
    - [fromRawDangerously()](#fromrawdangerously)
    - [private fromPostDto()](#private-frompostdto)
    - [fromRawDoc()](#fromrawdoc)
    - [fromMdb()](#frommdb)
    - [post()](#post)
    - [private toModel()](#private-tomodel)
    - [toResDTO()](#toresdto)
    - [updateFrom~()](#updatefrom)
    - [private update ()](#private-update-)
    - [delete ()](#delete-)
  - [Methods](#methods)

<!-- /TOC -->

TODO: Write documentation of DDD

## Order

Static Post > Static Get > Non-Static Put > Non-Static Delete


## Every domain has the following methods

### fromRawDangerously()

Deprecated method that is usually used by the test.

Try to delete it as much as possible.


### private fromPostDto()

Return Domain with given DTO (atd is required to write who created the domain)

It is usually private because it is directly called by post() method.

### fromRawDoc()

### fromMdb()

Usually takes Document type data and return domain.

this can be also `fromPersistence()` but then `fromMdb()` was chosen for its short method name


### post()

Returns WordDomain after saving into persistence.

It uses `fromPostDto()` and `toDocument()` methods to save into persistence.

### private toModel()

Returns model type data that can be saved into persistence.

It is usually private because it is directly called by post() method.


### toResDTO()

Returns the properties of the domain, only the data that end user can see.

Certain hidden data won't be visible to the user.



### updateFrom~()

Updates as the properties. Any name can be given with the tilda(~) sign.


### private update ()

Updates as the properties of the domain to the persistence.

It is usually private as it is called by other update functions such as `updateFrom~()`


### delete ()

Deletes the domain from the persistence.

the method contains access control to prevent unauthorized access.



## Methods

| Suffix      | Method Type | Remarks                       |
|:------------|:------------|:------------------------------|
| from, under | static      | When you create a new domain  |
| to          | non-static  | When you modify to other data |