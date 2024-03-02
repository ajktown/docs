# To Res Security

<!-- TOC -->

- [To Res Security](#to-res-security)
  - [Overview](#overview)
  - [Naming Rules of toRes()](#naming-rules-of-tores)
    - [toRes()](#tores)
    - [toSharedRes()](#tosharedres)

<!-- /TOC -->


## Overview
This documentation handles the writing convention of the methods `toRes()` that is used by the Domain that contains possible sensitive information.


## Naming Rules of toRes()


### toRes()
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