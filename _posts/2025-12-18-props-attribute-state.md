---
title:"Props, Attributes and States"
date:2025-12-18
---







## What They Are

- **HTML attributes** are static values written directly inside HTML tags. For example, in `<a href="www.wikipedia.org">`, `href` is an attribute. In JavaScript, it can be set using `element.setAttribute('href', 'www.wikipedia.org')`.
- **Props** (short for *properties*) are similar to HTML attributes, but they belong to React components. For example, in `<ContactInfo name="Ivy" />`, `name` is a prop.
   We receive props through a component’s function parameters, such as `function ContactInfo({ name }) { ... }`, and use them inside the component.
   Internally, props live under the `props` key of a React element, roughly like this:
   `{ type: 'ContactInfo', props: { name: 'Ivy', ... }, ... }`.
- **State** can be thought of as a special kind of variable. What makes it different from a normal variable is that we delegate the responsibility of *re-rendering when it changes* to React.

------

## Props vs. State

Props are the **only communication channel** between a parent component and a child component.

If a prop is just a regular value—such as a number, string, or plain JavaScript object—React does not manage it directly. As a result, if a prop that is *not derived from state* changes, React will not automatically re-render based solely on that change.

State, on the other hand, explicitly tells React to manage this value. When state updates, React decides whether and how the component should re-render based on the component’s internal logic.

------

## Props vs. Attributes

Some values on HTML elements exist as both **DOM properties** and **HTML attributes**, such as `href`. For these values, updating them through HTML or through JavaScript will keep the property and attribute in sync.

However, some properties exist **only in JavaScript**, such as props on custom React components. When these properties change, they do not appear in the HTML markup, because they are not HTML attributes at all.