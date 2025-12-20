---
title: "Iterating and Rendering Lists in React"
date: 2025-12-20
---



In React, we often need to render different UI based on data. Sometimes this means conditional rendering—showing component A in one case and component B in another. In many other situations, however, we need to **iterate over a collection of data** and render UI based on each item’s content.

React considers JavaScript powerful enough to handle this problem on its own, so it does not introduce any new mechanisms specifically for iteration or list rendering.

Instead, React encourages us to rely on existing JavaScript array methods. These methods all follow a similar pattern: we pass a function (a **callback**) as an argument to an iteration method. The iteration method loops over the array and applies the callback to each element.

Commonly used iteration methods include:

- `forEach`
- `map`
- `filter`

The names of these methods are very descriptive and closely reflect what they do.

------

## `forEach`

The `forEach` method is used to iterate over each element in an array.

Key characteristics:

- It **does not return a value**
- The original array is **not modified**
- The callback function can receive the element’s index as its second argument

Because it has no return value, `forEach` is usually used for side effects rather than for rendering UI.

------

## `map`

The `map` method is very similar to `forEach`, but with one crucial difference.

Key characteristics:

- The return values of the callback are collected into a **new array**
- The original array is **not modified**
- The callback function can receive the index as its second argument

Because `map` returns a new array, it is the most commonly used method for rendering lists in React.

------

## `filter`

The `filter` method is used to select a subset of elements from an array.

Key characteristics:

- The callback function returns a **boolean value**
- The original array is **not modified**
- Elements for which the callback returns `true` are included in a **new array**

This makes `filter` especially useful when you want to conditionally render only certain items based on their data.