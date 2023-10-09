# Add new field

<!-- TOC -->

- [Add new field](#add-new-field)
  - [Overview](#overview)
    - [Create Schema](#create-schema)
    - [Create Interface under domains directory](#create-interface-under-domains-directory)
    - [Create Response](#create-response)
    - [Create DTO](#create-dto)
    - [Create Factory](#create-factory)
      - [POST](#post)
      - [GET](#get)
      - [PUT](#put)
    - [Create Domain](#create-domain)
      - [constructor](#constructor-function Object() { [native code] }1)
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

### Create Interface under domains directory
Interface is used among domains, responses so must be created in earlier phase.

### Create Response


### Create DTO

Delete does not exist as many times delete only requires deleting id.
The permission is checked by the requester identity attached on http headers.


Delete does not exist as the DTO, but as the query.
Query still stays as the DTO though.


### Create Factory

#### POST


#### GET
You can still have the query for fine-grained GET request. (Like getting words)

#### PUT

### Create Domain
Copy from others and comment it out. And implement step by step

#### constructor
create constructor

#### fromMdb

#### post()


### Modify Word Domain

#### Modify Default if required


### Modify Factory

