---
title: High level overview of Redux
date: 2019-01-17 05:22:34
categories:
    - React Ecosystem
tags:
    - Redux
    - Flux
    - React
toc: true
description: “Redux is a predictable state container for JavaScript apps.”
---
Redux is inspired by Flux and Elm architecture. So, be sure to understand what Flux is before reading this article. Flux is a one-way data flow design pattern that helps you write a structured front-end architecture. If you want to explore Flux in more depth, you can refer to this - [LET'S TALK ABOUT FLUX](http://tingkaiwu.com/2019/01/12/lets-talk-about-flux/)
<!-- more -->
# Quick overview Flux
![Flux flow](https://drive.google.com/uc?export=view&id=1wqpOMUrlUZqzEXpS1hfoVouA9XPEEddl)
1. One-way data flow: The behavior of changing data must go through Action, Dispatcher, and then to the Store.
2. Single Source of Truth: The data is stored in the Store in a unified manner, and all the data required by the Viewer must be obtained from the Store.
3. Use a clearer model to regulate the flow of data in complex interaction scenarios of data and pages.