# React Hooks


## Overview


## Rules
- There should be at least one or more hooks for each API
  - API should be never called on ReactNode (React Component)
  - But instead, should depend on the hook that calls the API


## Hook Type
| Suffix   | Sample             | Usage                                                        |
|:---------|:-------------------|:-------------------------------------------------------------|
| NoSuffix | useDeleteWord      | When you simply call API and update recoil state accordingly |
| ~Cache   | useDeleteWordCache | When you want to delete the cache                            |