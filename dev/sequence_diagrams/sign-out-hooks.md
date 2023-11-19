# Sign Out Hooks

<!-- TOC -->

- [Sign Out Hooks](#sign-out-hooks)
  - [Overview](#overview)
  - [Hooks](#hooks)
    - [useOnSignOutApp](#useonsignoutapp)
    - [useIsAppBooted](#useisappbooted)
    - [useApiErrorHook](#useapierrorhook)

<!-- /TOC -->

## Overview

Summarizes each role of hooks for sign out process of AJK Town applications.


## Hooks

### useOnSignOutApp

Runs only when sign out is confirmed

1. Asks API to remove HttpOnly Cookies with postSignOut API[^1]

1. Reset appropriate recoil state reset

1. Goes to welcome page with appropriate [reasons](./sign-out.md#overview).

### useIsAppBooted

1. Runs only once for refresh

1. Opens/Closes Backdrop during the loading

1. Calls postAuthPrep API
- To get fundamental state data from API server
  - Env Data
  - Is end user signed in

1. Calls [useOnClickSignOutApp](#useonclicksignoutapp) only if not signed in

1. Redirects to home page, if signed in.


### useApiErrorHook

Catches every error of every api call of AJK Town Frontend applications.

1. If Error is related to authentication, runs [useOnClickSignOutApp](#useonclicksignoutapp).


<!-- Footnote -->

[^1]: Note that HttpOnly Cookie cannot be deleted by FE and must be asked by API.

<!-- Footnote -->