---
title: Let's talk about Flux
date: 2018-12-12 00:33:37
categories: 
    - Redux Origin
tags:
    - Flux
    - Redux
    - React
toc: true
description: Flux is a one-way data flow design pattern that helps you write a structured front-end architecture.
---
In the highly interactive front-end applications, the data state of the application and the user's operation events are the most vexing. Therefore, when we are dealing with complex interactions such as "event changes state, state refresh UI". A pattern is needed to regulate the data flow of the application. Flux is used to solve these problems.
<!-- more -->
<br>

# Flux origin
Flux is a design concept proposed by Facebook. Its most important thinking is one-way data flow.

![Flux vs MVC](/images/1_oRBseHE_yxtlbcRTrbkRnQ.jpeg)

Although not all MVC implementations are as shown above. It is easy to cause maintenance problems because of the two-way data flow. However, Flux clearly defines the roles' responsibilities and each role's interactions, which improves maintainability. Flux is a one-way data flow design concept, not a library, so it has a variety of implementations.
<br>

# Flux composition
![Flux flow](/images/Capture1.PNG)
**The main roles in Flux:**
- Action: Standardize all actions to change data, so you can quickly master the behavior of the entire App.
- Action Creator: Responsible for creating action and passing action to dispatcher.
- Dispatcher: Inform all registered stores of the current behavior.
- Store: Store data and business logic, and only provide getter API for other modules to obtain data.
- Controller View: Responsible for registering the listener with the store, and obtaining the latest data to pass to the view.
- View: Render the UI according to the data and listen to the user's operation events.
<br><br>

# Flux process flow
![Flux flow detail](/images/Capture2.PNG)
1. User operation app.
2. Action creator creates the action and passes it to dispatcher.
3. The dispatcher sequentially passes the action to the store.
4. The store determines whether the data needs to be updated according to the action type.
5. If the data is updated, then trigger the controller view listener.
6. Controller view gets the latest data from the store.
7. View re-renders the UI based on the data.
<br><br>

# Conclusion
Flux is a one-way data flow design pattern that helps you write a structured front-end architecture.

The benefits Flux brings to you are:
1. You can quickly master the behavior in the entire app.
2. Information and business logic are also stored uniformly.
3. Let View only need to be responsible for the layout of the UI.
<br><br>

Next article - [High level overview of Redux](http://tingkaiwu.com/2018/12/20/high-level-overview-of-redux/)

<br><br><br><br>
--------------------------------------------------------------------------------

**Reference link:**
[https://medium.com/4cats-io/flux-44a48c320e11](https://medium.com/4cats-io/%E6%B7%B1%E5%85%A5%E6%B7%BA%E5%87%BA-flux-44a48c320e11)
[https://medium.com/@w3bh4ck/the-flux-architecture-pattern](https://medium.com/@w3bh4ck/the-flux-architecture-pattern-for-frontend-development-1f2dae32b789)