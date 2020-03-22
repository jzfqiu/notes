## 3. Async and `Promise()`

### 3.1. Async and Web API

When JS is asked to "perform a time-consuming task in the background", it can delegate the task upon the browser's many **web APIs** and move on to other tasks at hand. APIs live on different threads than the event loop, therefore do not interfere with JS's own order of execution. When the API finish the task, it will throw the result into the job queue so that the event loop can process the result with the task's call back function.

A list of Web APIs can be found [here](https://developer.mozilla.org/en-US/docs/Web/API). It is worth noting that the majority of functions in web applications are implemented through APIs, such as DOM API and fetch API. While

### 3.2. `Promise()`

    A Promise is a proxy for a value not necessarily known when the promise is created. It allows you to associate handlers with an asynchronous action's eventual success value or failure reason

As a function `Promise()` is used to wrap around functions that does not return the `Promise` object

![Promise Execution Flowchart](https://mdn.mozillademos.org/files/15911/promises.png)

When a `Promise` is resolved, the callback function is pushed into the 