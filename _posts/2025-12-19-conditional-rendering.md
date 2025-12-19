---
title: "Conditional Rendering in React"
date: 2025-12-19
---



Conditional rendering is a very common pattern in React: in some cases we render component A, and in others we render component B.

React intentionally does **not** introduce new syntax for this. Instead, it relies entirely on features already provided by JavaScript. However, there is one important constraint: JSX uses curly braces `{}` as **expression slots**, and only **expressions** are allowed inside them—not **statements**.

If you need to use statements, the logic must be executed *outside* of JSX, and the result can then be inserted into an expression slot. For the sake of readability and conciseness, when the logic is simple and can be expressed as an expression, it is usually best to prefer expressions over statements.

------

## `if–else` Statements

Why can’t we use `if` statements directly inside an expression slot?

I didn’t fully understand this until I studied *The Joy of React*. Consider the following example:

```jsx
function Friend({ name, isOnline }) {
  return (
    <li className="friend">
      {if (isOnline) {
        <div className="green-dot" />
      }}
      {name}
    </li>
  );
}
```

After compilation, `{if (...) { ... }}` would become a **child** of the `li` React element. But `if` is a **statement**, and statements do not produce values. Since a child must be a value, this simply cannot work.

If you want to use `if` for conditional logic, you must do so **outside** the JSX and store the result in a variable:

```jsx
function Friend({ name, isOnline }) {
  let prefix;
  if (isOnline) {
    prefix = <div className="green-dot" />;
  }

  return (
    <li className="friend">
      {prefix}
      {name}
    </li>
  );
}
```

------

## Control Flow Operators

Logical operators such as **AND (`&&`)** and **OR (`||`)** produce expressions, which means they can be used directly inside expression slots:

```jsx
function Friend({ name, isOnline }) {
  return (
    <li className="friend">
      {isOnline && <div className="green-dot" />}
      {name}
    </li>
  );
}
```

This works because if `isOnline` is truthy, the expression evaluates to `<div className="green-dot" />`; otherwise, it evaluates to `isOnline`.

However, this pattern can be dangerous if the left-hand side is not strictly boolean. For example, if `isOnline` is `0`, React would render `0` instead of nothing.

A good rule of thumb is to ensure that the left-hand side of `&&` always evaluates to a boolean. Two common ways to do this are:

```jsx
{isOnline > 0 && <div className="green-dot" />}
```

or

```jsx
{!!isOnline && <div className="green-dot" />}
```

------

## Ternary Expressions

The ternary operator is very similar to `if–else`, but with one key difference: `if` is a **statement**, while a ternary is an **expression**.

That makes ternaries a natural fit for JSX:

```jsx
function App({ user }) {
  const isLoggedIn = !!user;

  return (
    <>
      {isLoggedIn
        ? <AdminDashboard />
        : <p>Please log in first</p>}
    </>
  );
}
```

------

## Performance Considerations

In vanilla JavaScript, we often use CSS properties like `display` to control whether an element is visible. React’s conditional rendering can achieve a similar effect: in both cases, users—including screen reader users—cannot perceive the hidden element.

However, there is an important difference:

- **React conditional rendering** does not insert the node into the DOM at all, which can be more performant in large applications.
- **CSS-based toggling** only changes a property like `display`, so switching visibility is usually faster.

For most small applications, the difference is negligible. In performance-sensitive scenarios, it may be worth testing both approaches to see which works better for your specific case.