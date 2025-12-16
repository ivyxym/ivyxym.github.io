---
title: "Thinking in JSX"
date: 2025-12-16
---

Today, I want to write down some of my thoughts about **JSX**. JSX is React’s syntactic sugar—it blends JavaScript and HTML together.

JSX is built on top of JavaScript. It uses expression slots like `{}` to embed JavaScript expressions directly into the markup, fully embracing JavaScript as the foundation. When JavaScript already provides a capability, JSX uses it without hesitation. But when JavaScript alone isn’t enough, JSX introduces new syntax to enable things that vanilla JavaScript can’t easily express.

At the same time, JSX leverages the tree-like structure of HTML to represent logic. I think this design is incredibly smart. Almost all frontend developers are familiar with HTML, or at least have some exposure to it. The hierarchical, recursive structure also aligns very well with how humans naturally think.

That said, JSX is only *using* the form of HTML. JSX is transpiled into plain JavaScript—it never becomes an `.html` file. Even though tags like `<button>` look identical in JSX and HTML, they become fundamentally different things after transpilation. Because of this, JSX treats HTML with two distinct strategies: **accepting existing rules** and **introducing new ones**.

I believe that understanding these design decisions from the perspective of React’s maintainers helps reduce rote memorization. Instead of syntax slipping through our fingers like sand, it becomes something we genuinely understand—making it far easier to learn React effectively.

------

## Accepting Existing Rules

### Whitespace behavior

- **HTML whitespace**: Newlines, tabs, and multiple spaces are collapsed into a single space.
- **JavaScript whitespace**: Outside of strings (e.g. `const str = "This is a string."`), whitespace exists purely for readability.
- **JSX combines both behaviors**:
  - **Inside a node**, JSX collapses whitespace (HTML-style).
  - **Between nodes**, JSX treats whitespace as irrelevant for developers and discards it entirely (JavaScript-style).

For example, the following code renders as:

**`Posted Time: January 1st at 12:00am`**

```jsx
<footer>
  Posted Time:
  <time datetime="2024-01-01T00:00:00.000Z">
    January 1st at 12:00am
  </time>
</footer>
```

------

## Creating New Rules

### 1. Redefining the `value` attribute on `<input>`

- In **HTML**, `<input value="hello">` sets the default value, which the user can later change.
- In **React**, `<input value="hello">` *locks* the input’s value to `"hello"`, making it read-only unless you handle updates explicitly.

------

### 2. Unifying all form inputs

Beyond single-line text inputs, forms include:

- Textareas
- Radio buttons
- Checkboxes
- Select elements
- Range inputs
- Color pickers

React unifies all of them under the same mental model:

- Use `value` or `checked` (for checkboxes and radio buttons) to bind **state → form**, effectively locking the current input value.
- Use `onChange` to bind **form → state** when user input changes.

------

### 3. New syntax rules in JSX

From what I’ve learned so far, JSX introduces several new syntax rules:

- **Reserved keyword conflicts**
  Some HTML attributes conflict with JavaScript keywords, such as `class` and `for`. JSX resolves this by renaming them to `className` and `htmlFor`.

- **JSX must be closed**
  Some HTML tags don’t need closing tags (e.g. `<p>Hello world`) and some are self-closing by nature (e.g. `<img src="...">`).
  In JSX, everything must be explicitly closed:

  ```jsx
  <img src="..." />
  ```

- **JSX tags are case-sensitive**

- **JSX attributes are case-sensitive**
  Attributes must use camelCase. For example, `autoplay` in HTML becomes `autoPlay` in JSX.
  React helps by warning you in the console if something is wrong.
  There are two notable exceptions where dashes are allowed:

  - `data-test-id`
  - `aria-label`

- **Inline styles use double braces**
  Inline styles must be written as:

  ```jsx
  style={{ fontSize: '2rem' }}
  ```

  The outer `{}` is the expression slot, and the inner `{}` creates a JavaScript object. Hyphenated CSS properties are converted to camelCase.