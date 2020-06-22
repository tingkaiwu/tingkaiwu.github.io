---
title: "Design Principles of Middleware"
date: 2019-02-09 15:33:38
categories:
  - Middleware Trilogy
tags:
  - Middleware
  - Redux
  - React
toc: true
description: Why should Middleware declare it as store => next => action => {}?
feature:
---
After reading the previous article ([Middleware Implementation](http://tingkaiwu.com/2019/02/03/deep-dive-into-middleware-2/)), there must be some questions. First of all, Middleware should be able to process the Action after it is dispatched and before entering the Reducer. So Middleware should be a function that can get the action parameters:
<!-- more -->

```sh
function middleware(action) {}
```

Then, in order to be able to chain multiple Middleware, Middleware should be able to get a current dispatch() function and return a function that will call the dispatch(), so derived from the above form:

```sh
function middlewareWrapper(dispatch) {
  return function(action) {
    dispatch(action)
  }
}
```

Finally, in order to get the current state or re-dispatch an action, Middleware needs to get the store parameter, so wrap it with another layer:

```sh
function storeWrapper(store)
  function middlewareWrapper(dispatch) {
    return function(action) {
      dispatch(action)
    }
  }
}
```

Rewrite in ES6 Arrow Function:

```sh
const = storeWrapper = store => dispatch => action => {
  dispatch(action)
}
```

The function and parameter names are changed to customary naming:

```sh
const middleware = store => next => action => {
  next(action)
}
```
<br>

# How does Redux apply multiple Middleware?
Redux applies multiple Middleware, mainly in the function applyMiddleware, The following is an applyMiddleware function that imitates Redux official source code and can be applied to three Middleware:

```sh
function applyMiddleware(middleware1, middleware2, middleware3) {
  const store = {
    dispatch: action => action
  };
  const [mw1, mw2, mw3] = [middleware1, middleware2, middleware3].map(middleware => middleware(store))
  store.dispatch = mw1(mw2(mw3(store.dispatch)))
  return store
}
```

Most of the time we use Redux Middleware written by others directly and rarely implement it ourselves, but if we try to understand the logic behind Redux Middleware, we can better use Redux Middleware to solve the problem.
<br><br><br><br>

----------------------------------------------------------

**Reference link:**
[https://medium.com/@max80713/redux-middleware-efd6a506357e](https://medium.com/@max80713/%E8%A9%B3%E8%A7%A3-redux-middleware-efd6a506357e)
[https://medium.com/@WendellLiu/redux-middleware-ace7e646c929](https://medium.com/@WendellLiu/redux-middleware%E5%A4%A7%E7%95%A5%E6%9E%B6%E6%A7%8B-ace7e646c929)