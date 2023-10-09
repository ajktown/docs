# Add new field

<!-- TOC -->

- [Add new field](#add-new-field)
  - [Overview](#overview)
    - [Create Schema](#create-schema)
    - [Create DTO](#create-dto)
      - [POST](#post)
      - [GET](#get)
      - [PUT](#put)
    - [Create Interface under domains directory](#create-interface-under-domains-directory)
    - [Create Domain](#create-domain)
      - [fromMdb](#frommdb)
      - [post()](#post)
    - [Modify Word Domain](#modify-word-domain)
      - [Modify Default if required](#modify-default-if-required)
    - [Modify Factory](#modify-factory)

<!-- /TOC -->

## Overview
When you create a new schema field, you need to modify the following files.

### Create Schema

Simply copy from others and change the name only!
If you cannot come up with a name, you can ask ChatGPT for help.

### Create DTO

Delete does not exist as many times delete only requires deleting id.
The permission is checked by the requester identity attached on http headers.


Delete does not exist as the DTO, but as the query.
Query still stays as the DTO though.

#### POST


#### GET
You can still have the query for fine-grained GET request. (Like getting words)

#### PUT

### Create Interface under domains directory
Before create domain, create the interface for the domain.

### Create Domain
Copy from others and comment it out. And implement step by step

#### fromMdb

#### post()


### Modify Word Domain

#### Modify Default if required


### Modify Factory

