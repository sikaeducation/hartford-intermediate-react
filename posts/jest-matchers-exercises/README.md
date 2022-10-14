---
questions:
  - id: 1
    prompt: |
      ```ts
      expect(undefined).toEqual(undefined)
      ```
    answer: |
      ```ts
      expect(undefined).toBeUndefined()
      ```
  - id: 2
    prompt: |
      ```ts
      expect(!someString).toEqual(false)
      ```
    answer: |
      ```ts
      expect(someString).toBeFalsy()
      ```
  - id: 3
    prompt: |
      ```ts
      expect(!!someNumber).toEqual(true)
      ```
    answer: |
      ```ts
      expect(someNumber).toBeTruthy()
      ```
  - id: 4
    prompt: |
      ```ts
      const someString = "Hello, world!"
      const containsHello = someString.includes("Hello")
      expect(containsHello).toEqual(true)
      ```
    answer: |
      ```ts
      const someString = "Hello, world!"
      expect(someString).toContain("Hello")
      ```
  - id: 5
    prompt: |
      ```ts
      const someString = "Hello, world!"
      const startsWithHello = (/^hello/i).test(someString)
      expect(startsWithHello).toEqual(true)
      ```
    answer: |
      ```ts
      const someString = "Hello, world!"
      const startsWithHello = (/^hello/i).test(someString)
      expect(someString).toMatch(/^hello/)
      ```
  - id: 6
    prompt: |
      ```ts
      const five = await Promise.resolve(5)
      expect(five).toEqual(5)
      ```
    answer: |
      ```ts
      const five = Promise.resolve(5)
      await expect(five).resolves.toEqual(5)
      ```
  - id: 7
    prompt: |
      ```ts
      const array = [1, 2, 3]
      expect(array.length).toEqual(3)
      ```
    answer: |
      ```ts
      const array = [1, 2, 3]
      expect(array).toHaveLength(3)
      ```
  - id: 8
    prompt: |
      ```ts
      const numbers = [1, 2, 3]
      const includesThree = numbers.includes(3)
      expect(includesThree).toEqual(true)
      ```
    answer: |
      ```ts
      const numbers = [1, 2, 3]
      expect(numbers).toContain(3)
      ```
  - id: 9
    prompt: |
      ```ts
      const array = [{ id: 1 }, { id: 2 }, { id: 3 }]
      const includesThree = array.filter(item => item.id === 3).length > 0
      expect(includesThree).toEqual(true)
      ```
    answer: |
      ```ts
      const array = [{ id: 1 }, { id: 2 }, { id: 3 }]
      const includesThree = array.filter(item => item.id = 3).length > 0
      expect(array).toContainEqual({ id: 3 })
      ```
  - id: 10
    prompt: |
      ```ts
      const person = { id: 1, name: "Kyle" }
      const hasName = person.hasOwnProperty("name")
      expect(hasName).toEqual(true)
      ```
    answer: |
      ```ts
      const person = { id: 1, name: "Kyle" }
      expect(person).toHaveProperty("name")
      ```
  - id: 11
    prompt: |
      ```ts
      const person = { id: 1, name: "Kyle" }
      const isKyle = person.name === "Kyle"
      expect(isKyle).toEqual(true)
      ```
    answer: |
      ```ts
      const person = { id: 1, name: "Kyle" }
      expect(person).toHaveProperty("name", "Kyle")
      ```
  - id: 12
    prompt: |
      ```ts
      const numbers = [1, 2, 3]
      const includesThree = numbers.includes(3)
      expect(!includesThree).toEqual(true)
      ```
    answer: |
      ```ts
      const numbers = [1, 2, 3]
      expect(numbers).not.toContain(3)
      ```
---

# Jest Matchers Exercises

_Revise the following assertions to use more appropriate matchers_
