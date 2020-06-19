---
title: Dive into Middleware - Implementation
date: 2019-02-03 14:00:13
categories:
  - Middleware Trilogy
tags:
  - Middleware
  - Redux
  - React
toc: true
description: How to build a Middleware?
feature:
---
Continued from the previous article ([Dive into Middleware - Introduction](http://tingkaiwu.com/2019/01/29/deep-dive-into-middleware-1/)). Let's continue to talk about how to use Middleware. The following is a Dummy Middleware, which represents the basic architecture of a Middleware, which can also be expressed by ES6 Arrow Function:
<!-- more -->

```sh
function middleware(store) {
  return function(next) {
    return function(action) {
      
      /* Code */
    
      return next(action);
    }
  }
}
```

ES6 Arrow Function Implementation:

```sh
const middleware = store => next => action => {
  /* Code */
  return next(action);
}
```
<br>

# What does next() in Middleware do?
next() is the function used to hand over the Action to the next Middleware. In other words, every Action received by Middleware will be the action passed by the previous Middleware call next(). If there is no next Middleware, it will let the Reducer handle it. Here is a simple example:

```sh
const middleware1 = store => next => action => {
  next(action);
};
const middleware2 = store => next => action => {
  next(action);
};
const reducer = (state, action) => {}
// create store & use middleware
store.dispatch(action);
```

1. When the Store dispatches an aAction, if there is Middleware, it will be processed by the first Middleware, otherwise it will be directly handled by the Reducer.
2. middleware1 is the first Middleware, received the action dispatched by store, call next() to hand over the Action to the next Middleware (middleware2).
3. middleware2 receives the action dispatched by middleware1, calls next() to hand over the Action to the next Middleware.
4. Because middleware2 is the last Middleware, the Reducer handles middleware2's dispatched actions.
<br><br>

# What is the return value of calling next() in Middleware?
Each Middleware return value will be obtained by calling next() in the previous Middleware. That is to say, the return value of calling next() in Middleware will be the value of the next Middleware return. If it is calling next() in the last Middleware, the return value will be the incoming action itself, for example:

```sh
const middleware1 = store => next => action => {
  const value = next(action);
  return value;
};
const middleware2 = store => next => action => {
  const value = next(action);
  return value;
};
// creatw store & use middleware
const value = store.dispatch(action);
```

1. The last Middleware (middleware2) call next() will return the incoming Action.
2. middleware1 calling next() will return the value of the next Middleware (middleware2) return.
3. Finally, store.dispatch() will return the value of the first Middleware (middleware1) return.

The complete sample code is attached below to demonstrate the execution sequence of calling next() and the execution result of its return value. Click on the console button below to see the results:

<iframe
     src="https://codesandbox.io/embed/next-ismo4?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="next"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-autoplay allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>
<br><br>

# Is there a return in Middleware?
Not necessarily. If there is no return in Middleware, calling next() in the previous Middleware will return undefined (if there is no return in the first Middleware, then calling store.dispatch() will return undefined). Generally speaking, Middleware can return any types of data, but if there is no special requirement, it is recommended to directly return the value returned by calling next(), to ensure that calling store.dispatch() can get the dispatch action.
<br>

# Can I get the current state in Middleware?
Of course can. One of the reasons Middleware is written as store => next => action => {} is to allow developers to get the store parameters in Middleware and get the current state through store.getState().
<br>

# What happens when I call store.dispatch() in Middleware?
The parameters of the store in Middleware can call getState() to get the current state, or you can call dispatch to send an action. The difference from calling next() is that the action of dispatching through next() is send to the next Middleware, and the action dispatched through store.dispatch() will go through all Middleware again (from the following picture you can understand the difference between the two).

![Middleware flow](/images/0_SGzQlCN4O4KMKVLy.png)
<br>

Next article - [Dive into Middleware - Principles](http://tingkaiwu.com/2019/02/09/deep-dive-into-middleware-3/)
<br><br><br><br>

----------------------------------------------------------

**Reference link:**
[https://medium.com/@max80713/redux-middleware-efd6a506357e](https://medium.com/@max80713/%E8%A9%B3%E8%A7%A3-redux-middleware-efd6a506357e)
[https://medium.com/@WendellLiu/redux-middleware-ace7e646c929](https://medium.com/@WendellLiu/redux-middleware%E5%A4%A7%E7%95%A5%E6%9E%B6%E6%A7%8B-ace7e646c929)