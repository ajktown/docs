# Write a proper react style using atomic approach

<!-- TOC -->

- [Write a proper react style using atomic approach](#write-a-proper-react-style-using-atomic-approach)
  - [Overview](#overview)
  - [Atomic folders, Molecule folders, Organism folders](#atomic-folders-molecule-folders-organism-folders)
  - [Handlers](#handlers)
  - [Components](#components)
  - [Components Naming Rule](#components-naming-rule)

<!-- /TOC -->

## Overview

Learn how to write a proper React code using atomic approach


## Atomic folders, Molecule folders, Organism folders

- They are ideally must be done in library, if shared by different services.
- They should have their theme set up
  - The theme has to be managed by one source.

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

## Components Naming Rule

| Type  | Suffix | Explanation                                        | Example       |
|:------|:-------|:---------------------------------------------------|:--------------|
| Basic | N/A    | Any basic component does not get suffix            | WordCard      |
| Chunk | Chunk  | More than one basic components                     | WordCardChunk |
| Frame | Frame  | Component Chunk + Helper settings and tools within | WordCardFrame |
