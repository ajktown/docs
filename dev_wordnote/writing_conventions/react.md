# Write a proper react style using atomic approach

<!-- TOC -->

- [Write a proper react style using atomic approach](#write-a-proper-react-style-using-atomic-approach)
  - [Overview](#overview)
  - [Atomic folders, Molecule folders, Organism folders](#atomic-folders-molecule-folders-organism-folders)
  - [Callback functions](#callback-functions)
  - [Handlers](#handlers)
  - [Components](#components)
  - [Component's functions](#components-functions)
  - [Components Naming Rule for Atom](#components-naming-rule-for-atom)
  - [Components Naming Rule for Molecule & Organism](#components-naming-rule-for-molecule--organism)

<!-- /TOC -->

## Overview

Learn how to write a proper React code using atomic approach


## Atomic folders, Molecule folders, Organism folders

- They are ideally must be done in library, if shared by different services.
- They should have their theme set up
  - The theme has to be managed by one source.


## Callback functions
- Every React Node's component
  - Either business logic implemented component
  - Styled component
- Must have its function useCallback as default, so any re-rendering should not cause 
  - infinite loop
  - Unnecessary writing coding


## Handlers

- Handlers contain any shared functions between components (where the business logic lives)
- Handlers are required to have the test file
  - They must be tested and covered 100% all time
- There should not be too many handlers for FE, and it should not be too heavy as well. 
  - Too heavy handlers can be exported to the API side

## Components

Components contain business connected ideas, and therefore cannot be used by other applications

Components must start with its prefix from the following
- organism
- molecule
- atom



## Component's functions

Every component's props given function must start with on~ (i.e onClick)

Every component's internal function must start with handle~ (i.e handleClick)
- By this rule, we can know that it is an internal function, when it starts with handle, and vice versa.

Every component has its inside function with useCallback and useMemo for any memorization. 

## Components Naming Rule for Atom

| Type  | Suffix | Explanation                                        | Example                                       |
|:------|:-------|:---------------------------------------------------|:----------------------------------------------|
| Basic | N/A    | Any basic atom does not get suffix                 | LanguageSelector                              |
| Part  | N/A    | Atom sized part component for molecule or organism | WordCardExamplePart, WordCardFavoriteIconPart |

## Components Naming Rule for Molecule & Organism

| Type  | Suffix | Explanation                                        | Example       |
|:------|:-------|:---------------------------------------------------|:--------------|
| Basic | N/A    | Any basic Molecule or Organism does not get suffix | WordCard      |
| Chunk | Chunk  | More than one basic components                     | WordCardChunk |
| Frame | Frame  | Component Chunk + Helper settings and tools within | WordCardFrame |
