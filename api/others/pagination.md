# Pagination

<!-- TOC -->

- [Pagination](#pagination)
  - [Overview](#overview)
  - [How it works](#how-it-works)
  - [Sample Response](#sample-response)
  - [Pagination Root](#pagination-root)
    - [Error Handling](#error-handling)
      - [pageIndex](#pageindex)

<!-- /TOC -->

## Overview

The generalized pagination mechanism of AJK Town

## How it works

## Sample Response

```json
{
  "pageIndex": 0,
  "lastPageIndex": 0,
  "isNextPageExist": false,
  "totalPages": 1,
  "totalItems": 65,
  "itemPerPage": 100,
  "dataLength": 65,
  "data": [
    // ...
  ]
}
```


## Pagination Root

Straight copy from AJK Town API repository path: src/dto/index.root.ts

```ts
export class PaginationReqDTORoot {
  @IsNumber()
  @IsOptional()
  pageIndex: string

  @IsNumber()
  @IsOptional()
  itemsPerPage: string
}
```

| keys         | default | description                                  |
|:-------------|:--------|:---------------------------------------------|
| pageIndex    | 0       | The index of the page to be returned.        |
| itemsPerPage | 100     | The number of items to be returned per page. |

### Error Handling

#### pageIndex

1. If pageIndex is negative number, it will be returning with default pageIndex, which is 0.