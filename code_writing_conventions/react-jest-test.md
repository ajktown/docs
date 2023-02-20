# Writing Correct Jest Test For React

<!-- TOC -->

- [Writing Correct Jest Test For React](#writing-correct-jest-test-for-react)
  - [Overview](#overview)
    - [Must start with Exposure Test](#must-start-with-exposure-test)
    - [Sample Test File Prefix](#sample-test-file-prefix)
    - [For loop must be `forEach`](#for-loop-must-be-foreach)
    - [Expect string must be following this for its neatness](#expect-string-must-be-following-this-for-its-neatness)

<!-- /TOC -->

## Overview

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
  it(`should return the expected output "${test.wantDaysAgo}" from ""${test.sampleDate}""`, () => {
    expect(gotDaysAgo).toBe(test.wantDaysAgo)
  })
})
```

### Expect string must be following this for its neatness

```ts
it(`expects "${test.wantDaysAgo}" from "${test.sampleDate}""`, () => {
    expect(gotDaysAgo).toBe(test.wantDaysAgo)
  })
```
