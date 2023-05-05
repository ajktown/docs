# Auth Flow

<!-- TOC -->

- [Auth Flow](#auth-flow)
  - [TODOs](#todos)
  - [Sign in with Google](#sign-in-with-google)

<!-- /TOC -->

## TODOs
1. Delete this file if Akane understands Domain

## Sign in with Google


```plantuml

@startuml

title Test

participant "End User" as user
participant "API" as api
database "MongoDB" as db

activate user
  user -> api: データください
  activate api
    api -> api: はい！
    api -> db: 接続
    activate db
      db -> db: データを探す
      api <- db: データを返す (UserRaw)
    deactivate db
    api -> api: DBから来たデータを信じない
    api -> api: const userDomain = UserDomainClass.createFromDb(UserRaw)
    break If 間違っているデータが入ったら、
      user <[#red]-- api : あ、なんかエラーがありました。
    end break
    api -> api: UserDomainClassが作られました。（このデータは信じます)
    api -> api: UserDomainClassが作られる (クラスは信じる)
    user <- api: UserDomainClass.toResponse()
  deactivate api
  user -> user: もらったデータが見える
deactivate user


```


