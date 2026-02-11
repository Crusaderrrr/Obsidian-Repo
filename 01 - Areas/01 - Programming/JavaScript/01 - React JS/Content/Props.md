---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - React_JS
  - JavaScript
  - programming
note type: Informational Note
---
## 🔍 What Are **Props** in React?
**Props** (short for **properties**) are how you pass **data** into a component.

Imagine components are like **functions** — and **props are the arguments** you pass into those functions to customize how they behave or what they display.

In React, **components are reusable**, and props allow you to change the content they show **without rewriting them**.

---

## 🧠 Think of it like this:
> [!info] 📦 **Props are "packages of data"** you give to components so they know **what to display** or **how to behave**.

---

### 🎯 Real-life analogy:
Imagine a **Greeting Card Factory** that creates cards.
You give it:
- a **name** ("Maria")
- a **message** ("Happy Birthday!")

The factory uses those to print:
> **"Dear Maria, Happy Birthday!"**

You don’t need a new factory for each name — you just **send in different props**.

---

## 🛠️ React Code Example
**Parent component**:
```jsx
export default function App() {
  return (
    <div>
      <Greeting name="Alice" />
      <Greeting name="Bob" />
    </div>
  );
}
```

**Child component** (Greeting):
```jsx
function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}
```

**This will show**:
```
Hello, Alice!
Hello, Bob!
```

You reused the same `Greeting` component — but changed what it says, **thanks to props**.

---

## 🔧 How props work

1. The **parent component** (`App`) sends `name="Alice"` to `Greeting`.
2. Inside `Greeting`, that prop is accessible as `props.name`.
3. The component renders `<h1>Hello, Alice!</h1>`.

You can pass any kind of data:
- Text (strings)
- Numbers
- Arrays
- Objects
- Even functions!

---
## ✨ With Destructuring (a cleaner way):

```jsx
function Greeting({ name }) {
  return <h1>Hello, {name}!</h1>;
}
```

This just pulls `name` directly out of `props`.

---

## 🧪 Another example (passing multiple props):

```jsx
function UserProfile({ name, age }) {
  return <p>{name} is {age} years old.</p>;
}
```

Used like this:

```jsx
<UserProfile name="Carlos" age={28} />
```

Output:  
**Carlos is 28 years old.**

---

## 📌 Summary

|Concept|Meaning|
|---|---|
|Props|Data passed into a component|
|Purpose|Customize component behavior/content|
|Who sends?|The **parent** component|
|Who receives?|The **child** component|
