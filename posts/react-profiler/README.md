# React Profiler

Modern versions of the React Devtools come with the React Profiler, which measures how and why components rerender over time.

When a state change occurs in a React app, React begins a 2-part process:

1. **Render Phase**: React executes all of the component functions, processes all the templates, and populates an in-memory representation of the component tree. React calculates the difference between the component tree and the current DOM.
2. **Commit Phase**: The difference is updated in the DOM.

Collectively, each cycle of this called a commit.

## Profiling an app

To profile an app, go to the `Profile` tab in your dev tools. Hit the circle button to start recording, and then start using your app. After you've taken the actions you want to measure, stop recording. Each action in the app correlates to a commit, which is shown as a vertical bar. The size and color of these bars tell you how fast each action was. This alone is enough to be useful, but by clicking on a commit you can also see the rendering speed of every component in the rendering phase.

* If you have too many commits because you profiled for a long time, you can filter out fast commits so that you're only looking at your slowest actions.
* The Timeline tab shows the duration of the recording and when particular commits occurred. Render phase is shown in blue, commit phase is shown in purple.
* Profile recordings can be saved for later analysis or comparison.
* You can record additional information about commits, such as the component that initiated the commit and which props triggered rerenders, as well as the names of hooks. This comes at a cost to performance.

## Interpreting bars

Here's how to interpret the size and color of the bars:

* The length of the bar is the speed of the last render, the color is the speed of the current render
* Everything orange is slow, short and orange means it's getting worse
* Everything blue is fast, long and blue means it's getting better
* Gray bars didn't rerender, and their length is the speed of their last render. These won't get updated in the DOM and help speed up commits.

You can inspect details about individual component renders (as well as control the zoom of graphs) by clicking on a bar. Bar focus is maintained through different tabs, making them a powerful navigation tool.

### Flamegraph

The Flamegraph tab shows a bar for each component that rendered, as well as all of their childrens' renders. This is used to see the renders in order and see which components in a tree is slow or compare trees to each other. Each component's children are represented as bars nested underneath them.

The proportion of time a parent spent rendering only itself compared to its total time including children is captured separately. On the Flamegraph, it's displayed as `(this-component-only out of total-component-tree)`. For example, `(0.1ms out of 245.4ms)` implies that this component rendered very efficiently, but its children took much longer.

Here's how to interpret the curve of the bars:

* A long line leading to the next child component implies that it took a long time to process the body of the function before rendering the children
* A deep curve represents a heavily nested hierarchy
* A steep curve means that each layer rendered relatively quickly, shallow curve means it was slower
* Lots of gray means that fewer unnecessary renders are happening

## Ranked Chart

To only look at the components that render the slowest, use the Ranked Chart tab. This is a descending list of each component from slowest to fastest. In this chart, children's rendering time is not counted toward the measurement. This means components that look long on the Flamegraph because of their slow children may look short on the Ranked Chart if their own code was efficient.

## Guide to Profiling

1. Decide what you're trying to measure. An initial load? A particular user interaction? How something's rendering improves or degrades on subsequent commits? Identifying which part of a process is slow?
2. Record examples of these behaviors
3. Look at the Timeline view of the recording. Is it what you expected? Pay particular attention to the longest bars, as well as the triggering events and relative speed of the render and commit phases. Select a commit you want to inspect.
4. Look at the Ranked Chart for that commit. Which components rendered the slowest? Are any of them surprising?
5. Look at the Flamegraph for those renders. Is there anything unusual about what caused the render? What about the rest of the tree?
6. Still on the Flamegraph, are there any areas of the tree that appear to be rerendering too much? Any getting slower or faster? Are any components repeat offenders? Should any of these bars be gray?

## Watch Out!

* If you're trying to profile something in an online IDE, you'll likely need to break out the browser preview to its own Window.
* It's not possible to profile the initial render with the record button. Next to is the refresh button, which will start profiling and refresh the page, capturing the initial render.

## Additional Resources

| Resource | Description |
| --- | --- |

| [Introducing The React Profiler](https://reactjs.org/blog/2018/09/10/introducing-the-react-profiler.html) | Official release notes |
| [Pluralsight: Profiling Performance With React Developer Tools](https://www.pluralsight.com/guides/profiling-performance-with-react-developer-tools) | Pluralsight overview of features |
| [Pluralsight: Guide To React Dev Tools](https://www.pluralsight.com/guides/profiling-performance-with-react-developer-tools) | Sample app with performance issue |
