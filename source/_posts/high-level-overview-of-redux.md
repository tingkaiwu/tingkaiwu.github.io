---
title: High level overview of Redux
date: 2018-12-20 05:22:34
categories:
    - Redux Origin
tags:
    - Redux
    - Flux
    - React
toc: true
description: “Redux is a predictable state container for JavaScript apps.”
---
Redux is inspired by Flux and Elm architecture. So, be sure to understand what Flux is before reading this article. Flux is a one-way data flow design pattern that helps you write a structured front-end architecture. If you want to explore Flux in more depth, you can refer to this - [LET'S TALK ABOUT FLUX](http://tingkaiwu.com/2018/12/12/lets-talk-about-flux/)
<!-- more -->
<br>

# Quick walkthrough Flux
![Flux flow](/images/Capture1.PNG)
**Pros:**
- One-way data flow: The behavior of changing data must go through Action, Dispatcher, and then to the Store.
- Single Source of Truth: The data is stored in the Store in a unified manner, and all the data required by the Viewer must be obtained from the Store.
- Use a clearer model to regulate the flow of data in complex interaction scenarios of data and pages.

**Cons:**
- The store contains logic and state. When we need to dynamically replace the logic of a store, we can only replace the entire store, and then we cannot maintain the state stored in the store.
<br><br>

# Redux vs Flux
![Redux vs Flux](/images/1_68Ymu2WbuIb4CC7RFvh7hw.png)

| Flux | Redux |
| :--- | :--- |
| Flux provides Dispatcher to deliver action objects to each store | Redux Store provides dispatch API to deliver action objects |
| Flux has multiple stores | Redux has only one store |
| Data is stored in each store | Data is stored in a state object and managed by the Store |
| Business logic is stored in each store | Business logic corresponds to multiple Reducers functions |

<br><br>

# Redux core concepts
![Redux core concepts](/images/1_C0sWwmHXIY414rzEUDFEmg.png)
- Single state tree
- Action description changes
- Reducer implementation changes
<br><br>

# Redux from the code
The concept of Store in Redux is very simple, the following code:
```sh
let listeners = []
// 1. Only one status tree in Redux which stores all data
let state

// 2. When user trigger events, call store.dispatch(action)
function dispatch(action) {
  // 3. Get the latest status according to reducer
  state = reducer(state, action)
  // 4. Notify all listener store status has changed
  listeners.slice().forEach(l => l())
}

// 5. Call the getter API to get the latest status
//    when the viewer knows that the Store status has changed
function getState() {
  return state
}

// 6. Let viewer registration status change listener
function subscribe(listener) {
  listeners.push(listener)
  // 7. Return unsubscribe function
  return () => listeners.filter(l => l !== listener)
}
```
<br><br>

# Conclusion
Redux is a very simple state container that manages the state of the entire application. You can not change the data directly through the setter, new data must be obtained through the action and reducers.

The reducer returns new data based on the action object and old data, so you can store the action and call the reducer function again to get the same state. It helps us with predictable state management.

Therefore, Redux can be summarized in a sentence:

**“Redux is a predictable state container for JavaScript apps.”**
<br><br><br><br>
----------------------------------------------------------

**Reference link:**
[https://medium.com/4cats-io/-redux-7b08403c4957](https://medium.com/4cats-io/%E6%B7%B1%E5%85%A5%E6%B7%BA%E5%87%BA-redux-7b08403c4957)
[https://blog.quizup.com/react-in-retrospective-quizup-db1dcc0dc8a1](https://blog.quizup.com/react-in-retrospective-quizup-db1dcc0dc8a1)
[https://blog.csdn.net/DFF1993/article/details/80403309](https://blog.csdn.net/DFF1993/article/details/80403309)