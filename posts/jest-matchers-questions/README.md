---
questions:
  - id: 1
    prompt: |
      **What is a Jest matcher?**
    answer: |
      A method that asserts something about a value given to `expect()`
  - id: 2
    prompt: |
      **Why not use `.toEqual()` for all Jest assertions?**
    answer: |
      `.toEqual()` is the least expressive matcher and can lead to you putting logic in your assertions
  - id: 3
    prompt: |
      **What is the difference between the `.toEqual()` and `toBe()` matchers in Jest?**
    answer: |
      `toBe()` asserts that two values have the same location in memory, `toEqual` asserts that two values are equivalent
  - id: 4
    prompt: |
      **Which Jest matcher asserts that a string is included in another string?**
    answer: |
      `.toContain()`
  - id: 5
    prompt: |
      **Which Jest matcher asserts that a value is present when the specific value isn't important?**
    answer: |
      `toBeTruthy()`
  - id: 6
    prompt: |
      **Which Jest matcher asserts that something is `undefined`?**
    answer: |
      `toBeUndefined()`
  - id: 7
    prompt: |
      **Which Jest matcher tests a string against a regular expression?**
    answer: |
      `toMatch()`
  - id: 8
    prompt: |
      **How do you invert an assertion in Jest?**
    answer: |
      `.not`
  - id: 9
    prompt: |
      **How do you make assertions about promises in Jest?**
    answer: |
      `.resolves` and `.rejects`
  - id: 10
    prompt: |
      **Which Jest matcher asserts an object is present in an array?**
    answer: |
      `.toContainEqual()`
  - id: 11
    prompt: |
      **Which Jest matcher asserts a string is present in an array?**
    answer: |
      `.toContain()`
  - id: 12
    prompt: |
      **A test that makes assertions about promises always passes. What is it probably missing?**
    answer: |
      Testing a promises makes the entire test asynchronous
---

# Jest Matchers Questions

_Please answer the following questions as best you can_
