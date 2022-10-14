# TypeScript: Jest

`ts-jest` is a TypeScript setup for Jest. This means that after you install it, you can use Jest as normal with TypeScript code. `@types/jest` contains the official types for Jest tests, which adds types for Jest's included functions. To add Jest to a TypeScript project, install them both with:

```bash
npm install -D ts-jest @types/jest
```

Next, set up a Jest config file with:

```bash
npx ts-jest config:init
```

Once these are installed and configured, you can add test files with `.spec.ts` extensions, import `.ts` files directly, and use TypeScript in your test files. Note that you still use the `npx jest` and `npx jest --watchAll` commands to run your tests.

Note that in most situations it's not necessary to explicitly annotate Jest-specific types inside Jest files. One type-specific thing you may need to do is typing mocked functions:

```ts
import { someObject } from "./some-object"
jest.mock("./some-object")
const mockedObject = jest.mocked(someObject, true)

test("Something", () => {
  mockedObject.some.nested.method()
  expect(mockedObject.some.nested.method.calls).toHaveLength(1)
})
```

## Additional Resources

| Resource | Description |
| --- | --- |
| [Using TypeScript Via `ts-jest`](https://jestjs.io/docs/getting-started#using-typescript-via-ts-jest) | Official documentation on using TypeScript with Jest. |
| [`jest.mocked<T>(item: T, deep = false)`](https://jestjs.io/docs/jest-object#jestmockedtitem-t-deep--false) | Official documentation on typing mocks with Jest. |
