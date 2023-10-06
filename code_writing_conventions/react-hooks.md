# React Hooks

<!-- TOC -->

- [React Hooks](#react-hooks)
  - [Overview](#overview)
  - [Rules](#rules)
  - [Hook Type](#hook-type)
  - [Hooks Return and Usage](#hooks-return-and-usage)

<!-- /TOC -->

## Overview
Basic rules for React Hooks in FE

## Rules
- There should be at least one or more hooks for each API
  - API should be never called on ReactNode (React Component)
  - But instead, should depend on the hook that calls the API


## Hook Type
| Suffix   | Sample             | Usage                                                        |
|:---------|:-------------------|:-------------------------------------------------------------|
| NoSuffix | useDeleteWord      | When you simply call API and update recoil state accordingly |
| ~Cache   | useDeleteWordCache | When you want to delete the cache                            |


## Hooks Return and Usage

Hooks should always return data as you can use it.

```ts
export const usePutWordArchive = () => {
  ...
  return [loading, onPutWordArchive]
}
```

Hook above should be called as the following with same variable names.

```ts
...
const [loading, onPutWordArchive] = usePutWordArchive()
...
```

