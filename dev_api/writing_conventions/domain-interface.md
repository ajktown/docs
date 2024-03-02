# Domain Interface

<!-- TOC -->

- [Domain Interface](#domain-interface)
  - [Overview](#overview)
  - [Managed Prefix](#managed-prefix)
  - [Managed Name](#managed-name)
  - [Manged Suffix](#manged-suffix)

<!-- /TOC -->


## Overview

Basic rules of writing domain interface with fixed prefix and suffix.

## Managed Prefix
Every interface related to the domain must start with prefix `I`

## Managed Name
The Domain must be named the same as it would be stored in DB.

i.e) words (db) => IWord

## Manged Suffix
AJK Town uses only the following suffixes

|   Suffix   |                                           Description                                           |
|:----------:|:-----------------------------------------------------------------------------------------------:|
|   Input    | Used right before creating the domain. If certain data must be created in the constructor phase |
| (NoSuffix) |                    Props of the domain; has derived properties from `Input`                     |
|   Shared   |    Used to respond data for shared purpose. It contains less data than the original domain.     |
|  Derived   |                   Used when mother domain controls the respond of the domain                    |