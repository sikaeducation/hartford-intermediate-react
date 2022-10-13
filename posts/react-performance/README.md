# React Performance

React performance is primarily a function of controlling rerendering. A component rerenders when:

* Props or state have changed
* When the parent component rerenders
* When something in a hook triggers a rerender
* When it consumes a context and the value of a context provider changes

Some easy targets for improving performance in a React app include:

* If components manage state, memoize the parts of the render tree that don't use the state
* If the `value` of a context is an object, it should always be memoized
* Don't use `useCallback` to avoid re-renders of child components when passing a function as a prop. It won't prevent rerenders and add overhead.
* Never define a component in another component

## `useMemo`

The `useMemo` hook caches values so that once they're only calculated the first time. It allows you to selectively rerender things, which makes it your main tool for improving performance.

```js
import { useMemo } from "react"

function FilteredMovieList({ allMovies, searchTerm }){
  const filteredMovies = useMemo(() => {
    return allMovies.filter(movie => movie.name.includes(searchTerm))
  }, [allMovies, searchTerm])

  return (
    <div className="MovieList">
      {filteredMovies.map(movie => (
        <li key={movie.id}>{movie.name}</li>
      ))}
    </div>
  )
}

export default FilteredMovieList
```

* If a component has multiple sources of state, memoize the components that are only dependent on part of the state to minimize rerenders.
* `useMemo` also works with components, which can improve performance on mostly static parts of the component tree
* List items are a good target for memoization
* You can memoize the value of a context provider to reduce the number of rerenders

## Recomposition

An alternative to memoization is to recompose your components so that they're group by which state they depend on. Here are some examples:

* You can keep something that would trigger a ton of rerenders from affecting other components as much by making it a wrapper component. The children it wraps won't automatically rerender when the wrapper does.
* You can prevent a slow component from rerendering by passing it as a prop to the component that's triggering too much, it won't rerender its props because they haven't changed
* Split up a context's data and setter functions, you can split them into two different providers to reduce rerenders in the consumers, which may not all use both. You can also split up a large context data into smaller pieces.

## `useCallback`

`useCallback` is the same as `useMemo`, but works with functions instead of values.

```js
import { useCallback } from "react"

function FilteredMovieList({ allMovies, searchTerm }){
  const filterMovies = useCallback(movie => movie.name.includes(searchTerm), [allMovies, searchTerm])
  const filteredMovies = allMovies.filter(filterMovies)

  return (
    <div className="MovieList">
      {filteredMovies.map(movie => (
        <li key={movie.id}>{movie.name}</li>
      ))}
    </div>
  )
}

export default FilteredMovieList
```

`useCallback` only works when the function is being used in a dependency array or is a prop to a memoized component.

## Preserving Part of a Complex Object

```ts
setSomeState(previousState => {
  return {
    ...previousState,
    someProperty: "Only value that will be updated",
  }
})
```

## Watch Out!

* To know where these optimizations are helping or hurting, you need to measure them.
* `useMemo` only works if all of its reference values have been memoized or `useCallback`ed.
* `useMemo` doesn't stop a rerender if props change
* `useMemo` only makes sense if the data is deterministic.
* `useMemo` should mostly be used for component creation, most other calculations aren't slow enough to be worth it. Component creation is usually the most expensive thing.
* If a `useMemo` dependency array is all of the things that would cause the whole component to rerender, it's not doing anything
* You can only cache expensive calculations with with `useMemo`, not `useCallback`. `useCallback` is for functions, `useMemo` is for values or components.
* `useCallback` only has performance benefits when used in components that have been memoized, it should not be used just because a function is used as a prop

## Additional Resources

| Resource | Description |
| --- | --- |
| [Kent C. Dodds: When to use `useMemo` and `useCallback`](https://kentcdodds.com/blog/usememo-and-usecallback) | Blog post on the dangers of premature optimization |

