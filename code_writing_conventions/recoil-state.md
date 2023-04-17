# Recoil State File Name

<!-- TOC -->

- [Recoil State File Name](#recoil-state-file-name)
  - [Overview](#overview)
  - [Rules](#rules)
    - [Every state must have its key with RecoilKeyPrefix](#every-state-must-have-its-key-with-recoilkeyprefix)
      - [RecoilKeyPrefix](#recoilkeyprefix)
      - [PrivateRecoilKey](#privaterecoilkey)
      - [RecoilKeySuffix](#recoilkeysuffix)
    - [State and Selector must be separated as different files](#state-and-selector-must-be-separated-as-different-files)
    - [Recoil state data must be named properly with the correct suffix](#recoil-state-data-must-be-named-properly-with-the-correct-suffix)

<!-- /TOC -->

## Overview

Recoil is a state management library for React.

## Rules

### Every state must have its key with RecoilKeyPrefix


#### RecoilKeyPrefix
- The main key so that separated files for recoils will never share the same key

| Recoil Key Prefix |
|:------------------|
| Words             |
| Semesters         |
| Tags              |

#### PrivateRecoilKey


#### RecoilKeySuffix

| RecoilKeySuffix |
|:----------------|
| FamilyDialog    |
| SelectorFamily  |
| Selector        |

### State and Selector must be separated as different files

i.e
- src/recoil/words/tags.selectors.ts
- src/recoil/words/semesters.state.ts

### Recoil state data must be named properly with the correct suffix


| Source                 | Suffix          | Example                            |
|:-----------------------|:----------------|:-----------------------------------|
| API                    | ~Data           | WordData, UserData                 |
| Recoil: Atom           | ~State          | SearchInputState, CurrentUserState |
| Recoil: AtomFamily     | ~Family         | wordsFamily, usersFamily           |
| Recoil: Selector       | ~Selector       | isFavoriteClickedSelector          |
| Recoil: SelectorFamily | ~SelectorFamily | wordsSelectorFamily                |