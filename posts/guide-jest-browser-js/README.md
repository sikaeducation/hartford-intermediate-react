# Guide to Using Jest to Test Browser JavaScript

Jest runs code in an isolated Node.js environment, which means it doesn't have access to the DOM or any of the browser APIs. To get around this, Jest uses a popular DOM faking library called [jsdom](https://github.com/jsdom/jsdom) to provide these for your tests.

## Set the environment to `jsdom`

By default, Jest operates in a `node` environment without `jsdom`. To set up Jest for browser testing, set its environment to `jsdom`. You can either do this in a `jest.config.js` file:

```js
module.exports = {
  testEnvironment: "jsdom",
}
```

Or by adding this to your `package.json` file:

```json
{
  "jest": {
    "testEnvironment": "jsdom"
  }
}
```

## Using `require` instead of `import`

`import` needs all of the code to be loaded before any of it is run. To test DOM code, we need to setup documents in test files before running the code, which means using Node's built-in `require` function to import files:

```js
// Instead of this
import lodash from "lodash"
import myFile from "./my-file"

// Do this
const lodash = require("lodash")
const myFile = require("./my-file")
```

## Faking a Document

If the code you're testing interacts with the document, such as querying or attaching to DOM elements, you need to manually put these in the document. For example, if you have this code:

```js
const $button = document.querySelector("button")
const $message = document.querySelector("#message")
$button.addEventListener("click", () => {
  $message.textContent = "Hello, world!"
})
```

This code expects a `<button>` element and an element with an ID of `message` to exist in the DOM when it runs. You can manually add these inside the test:

```js
test("Some Test", () => {
  document.body.innerHTML = `
    <main>
      <button>Click Me</button>
      <p id="message"></p>
    </main>
  `
  require("../index.js")
})
```

Since your code needs the document to exist when it's loaded, use `require()` to load it after you've set up your document. Then you can query and write assertions about the document:

```js
test("Button prints hello world", () => {
  document.body.innerHTML = `
    <main>
      <button>Click Me</button>
      <p id="message"></p>
    </main>
  `
  require("../index.js")

  const $button = document.querySelector("button")
  const $message = document.querySelector("#message")

  $button.click()

  expect($p).toHaveProperty("textContent", "Hello, world!")
})
```

Note that you don't need to recreate the entire document for each test; only include the parts of the document necessary to run each test.

## Code with Network Requests

Mocking network requests with Jest alone is difficult and brittle. Rather than try to intercept or mock the requests, separate out the code making network requests from code that works with network requests. Instead of this:

```js
fetch(apiUrl)
  .then(response => response.json())
  .then(response => {
    const $h1 = document.querySelector("h1")
    $h1.textContent = response.text
  })
```

Split it into multiple files:

```js
// dom.js
export function setHeading(name){
  const $h1 = document.querySelector("h1")
  $h1.textContent = name
}

// network.js
import { setHeading } from "./dom"

fetch(apiUrl)
  .then(response => response.json())
  .then(response => {
    setHeading(response.text)
  })
```

Now the DOM code can imported and tested separately from the network code.

## Faking `localStorage`

The easiest way to fake `localStorage` is to replace the real implementations with normal Jest spies:

```js
const localStorageMock = {
  getItem: jest.fn(),
  setItem: jest.fn(),
  clear: jest.fn()
};
global.localStorage = localStorageMock;
```

You can mock implementations with these just as you can with any Jest spy:

```js
const localStorageMock = {
  getItem: jest.fn(() => {
    return "louisarmstrong"
  }),
};
```

As well as making assertions on them:

```js
expect(localStorage.getItem).toBeCalledWith("username")
```

## Additional Resources

| Resource | Description |
| --- | --- |
| [`jsdom`](https://github.com/jsdom/jsdom) | Official `jsdom` documentation |
| [`jest-fetch-mock`](https://www.npmjs.com/package/jest-fetch-mock) | Official `jest-fetch-mock` documentation |
