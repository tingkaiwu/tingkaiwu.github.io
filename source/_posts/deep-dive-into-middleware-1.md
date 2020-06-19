---
title: Dive into Middleware - Introduction
date: 2019-01-29 10:38:51
categories:
  - Middleware Trilogy
tags:
  - Middleware
  - Redux
  - React
toc: true
description: Middleware can process everything from the predefined start point to the end point.
feature:
---
Middleware is also called intermediary layer or middle layer. Middleware applications can be seen in many back-end server frameworks. Simply put, Middleware can process everything from the predefined start point to the end point.
<!-- more -->
<br>

# What role in Redux?
Redux Middleware can perform additional processing after the Action is assigned and before entering the Reducer, such as calling the API and so on. 

![Middleware's role](https://drive.google.com/uc?export=view&id=1EUk3RATpGN3UgOWTGhhE8xpvvKJ8_4qe)
<br>

# How to use Middleware?
Passing one or more middleware into the applyMiddleware() function provided by Redux will return an Enhancer, and then pass the Enhancer as a parameter to createStore() function.

```sh
import { applyMiddleware, createStore } from 'redux';
const enhancer = applyMiddleware(
  middlewareOne,
  middlewareTwo
);
const store = createStore(
  reducers,
  initialState,
  enhancer
);
```
<br>

Next article - [Dive into Middleware - Implementation](http://tingkaiwu.com/2019/02/03/deep-dive-into-middleware-2/)
<br><br><br><br>

----------------------------------------------------------

**Reference link:**
[https://medium.com/@max80713/redux-middleware-efd6a506357e](https://medium.com/@max80713/%E8%A9%B3%E8%A7%A3-redux-middleware-efd6a506357e)
[https://images.app.goo.gl/PjjzpBaYGNcZrpq87](https://images.app.goo.gl/PjjzpBaYGNcZrpq87)