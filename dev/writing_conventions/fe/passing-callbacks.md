# Passing Callbacks


<!-- TOC -->

- [Passing Callbacks](#passing-callbacks)
  - [Overview](#overview)
  - [Hooks](#hooks)
  - [Components](#components)
  - [Style Components](#style-components)

<!-- /TOC -->

## Overview
When you develop a React application, you will face a situation where you need to pass a callback function to a child component. And AJK Town offers a naming convention for this situation.

## Hooks

Hooks should return callback with on~ prefix, but should never be onClick.

- Samples
  - onPostWords
  - onGetWords
  - onPutWordTagDeleted
  - onDeleteWord


## Components

Components are allowed to define a callback simply named `onClick()`. If you have to define multiple `onClick()`, you should either create separate hooks or separate components.


The reason behind this is that component does only one job. If you have to define multiple `onClick()`, it means that your component is doing multiple jobs. And it is not a good practice.


## Style Components

Style Components should receive a callback function as `onClick()` props. If internal function is required, it should be named `handleClick()`.