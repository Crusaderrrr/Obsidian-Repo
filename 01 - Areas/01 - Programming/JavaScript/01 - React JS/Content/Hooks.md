---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - React_JS
  - JavaScript
  - programming
note type: Informational Note
---
Hooks are React JS built-in **functions**, that let you use features like *state*, *lifecycle methods* or *context* without any need of defining class components, as it was before. Hooks are useful, offer more features than classes and are convenient to use.

## There are some examples:

### useState
```JavaScript
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0); // count starts at 0

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}

```
- `useState(0)` creates a value `count` (starts at 0)
- `setCount` is a function to change the count
- Every time you click the button, `count` goes up

### useEffect
```JavaScript
import { useState, useEffect } from 'react';

function Logger() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log('The count is now:', count);
  }, [count]); // Runs this code every time `count` changes

  return (
    <button onClick={() => setCount(count + 1)}>
      Clicked {count} times
    </button>
  );
}

```
- This is like saying: “Every time count changes, run this code (in this case, log to the console).”

### useRef
```JavaScript
import { useState, useRef } from 'react';

function HiddenTracker() {
  const [count, setCount] = useState(0);
  const totalClicks = useRef(0); // Doesn't trigger re-render

  const handleClick = () => {
    setCount(count + 1);
    totalClicks.current += 1;
    console.log('Clicked', totalClicks.current, 'times total');
  };

  return (
    <button onClick={handleClick}>
      Visible Count: {count}
    </button>
  );
}

```
- `useRef` stores a value that doesn’t reset, but also doesn’t make the component update.
- Good for timers, tracking things, DOM elements, etc.

### useContext
```JavaScript
import { createContext, useContext } from 'react';

const UserContext = createContext();

function App() {
  return (
    <UserContext.Provider value="Alice">
      <Welcome />
    </UserContext.Provider>
  );
}

function Welcome() {
  const user = useContext(UserContext);
  return <h1>Welcome, {user}!</h1>;
}
```
- `UserContext.Provider` gives the value to any component inside it
- `useContext(UserContext)` lets you access it easily