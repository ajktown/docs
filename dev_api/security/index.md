# Security Index

<!-- TOC -->

- [Security Index](#security-index)
  - [Overview](#overview)
  - [Controller](#controller)
  - [Service](#service)
  - [Domain](#domain)
    - [toRes(atd)](#toresatd)
    - [toSharedRes()](#tosharedres)

<!-- /TOC -->

## Overview
This documentation contains security related information of the API.

AJK Town values user data protection as the most important duty even before the service itself. Therefore, the security of the API is the most important part of the service. This documentation contains the security related information of the API.



## Controller

Controller must return data using either of the following functions:
- `toRes(atd)`: Where atd is required to be a `ResponseDTO` object.
- `toSharedRes(atd)`: Where it is publicly accessible and does not require authentication.

## Service

Service must return data using either of the following format:
- Domain
- void (none)


## Domain

### toRes(atd)
- Returns almost every data of the domain
  - Most of the time, only the owner can access to the resource
    - `toRes()` must require atd to verify if it is really the correct owner
  - The returning resource should return `I~`
    - i.e) `IWord`, `ISemester`


### toSharedRes()
- Returns only sharable data
  - This function is most of the time used by the SharedResource
  - The returning resource should return `IShared~`
    - i.e) `ISharedWord`, `ISharedSemester`