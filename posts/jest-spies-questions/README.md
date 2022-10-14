---
questions:
  - id: 1
    prompt: |
      **What is a test spy?**
    answer: |
      A function that records what it was called with
  - id: 2
    prompt: |
      **What is a test mock?**
    answer: |
      A copy of an object that makes assertions when its methods are called
  - id: 3
    prompt: |
      **You pass a spy into a function. How would you verify that this spy was called exactly twice in Jest?**
    answer: |
      ```ts
      expect(someSpy).toHaveBeenCalledTimes(2)
      ```
  - id: 4
    prompt: |
      **Why is it important to keep mocks simple?**
    answer: |
      It's easy to replicate the logic you used to implement it
  - id: 5
    prompt: |
      **What's the difference between `jest.fn()` and `jest.mock()`?**
    answer: |
      `jest.fn()` creates a spy, `jest.mock()` mocks an object
  - id: 6
    prompt: |
      **What does the `.mock` property on Jest spy contain?**
    answer: |
      Details about how it was used
  - id: 7
    prompt: |
      **How do you stub a promise?**
    answer: |
      ```ts
      const someStub = jest.fn().mockResolvedValue(someValue)
      ```
---

# Jest Spies Questions

_Please answer the following questions as best you can_
