# Writing Correct Jest Test For React

<!-- TOC -->

- [Writing Correct Jest Test For React](#writing-correct-jest-test-for-react)
  - [Overview](#overview)
    - [Testing function must have its argument(s)](#testing-function-must-have-its-arguments)
    - [Must start with Exposure Test](#must-start-with-exposure-test)
    - [Sample Test File Prefix](#sample-test-file-prefix)
    - [For loop must be `forEach`](#for-loop-must-be-foreach)

<!-- /TOC -->

## Overview

### Testing function must have its argument(s)
```ts
describe(`timeHandler.getDaysAgo(date: Date)`, () => {
  // ...
})
```

### Must start with Exposure Test

```ts
it(`should be exposed as a function`, () => {
  expect(timeHandler).toBeDefined()
  expect(timeHandler.getDaysAgo).toBeDefined()
})
```

### Sample Test File Prefix

```ts
interface Test { // Interface => Test
  sampleDate: Date // Prefix => sample~
  wantDaysAgo: number // Prefix => want~
}
```

### For loop must be `forEach`

```ts
tests.forEach((test) => {
  const gotDaysAgo = timeHandler.getDaysAgo(test.sampleDate)
  it(`should return "${test.wantDaysAgo}" with arg(s) "${test.sampleDate}""`, () => {
    expect(gotDaysAgo).toBe(test.wantDaysAgo)
  })
})
```
