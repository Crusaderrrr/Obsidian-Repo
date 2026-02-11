---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - JavaScript
  - redux
note type: Informational Note
---
1. **What is Redux?**
It is a JS library often used with [[00 - React MoC|React JS]]. It's main purpose is to keep track of everything that happens in an application in one place. It makes sure data changes in a clear, predictable way.

2. **Redux Core Principles**
- *Single source of truth* (Store): all data lives in one spot.
- *State is Read-Only*: data can't be changed directly, a particular action need to be executed.
- *Changes with pure functions* (Reducers): special rules (functions) decide how data updates. 

3. **Store** 
The place where all data lives, it's a JS object, not a class. The *state* lives here. 
```JavaScript
const store = {todos: [], count: 0}
```

4. **Action**
	A command that tells redux what to do, can be accompanied with a payload(data).
```JavaScript
{ type: "ADD_TODO", payload: "Buy milk" } // Note to add a task
```

5. **Action Creator**
The function that makes an action.
```JavaScript
function addTodo(task) {
  return { type: "ADD_TODO", payload: task };
}
addTodo("Buy milk"); // Returns { type: "ADD_TODO", payload: "Buy milk" }
```

6. **Reducer**
A recipe or set of instructions that decides how to update your app’s data (state) based on a request (action).
```JavaScript
const initialState = { todos: [] };
function todoReducer(state = initialState, action) {
  if (action.type === "ADD_TODO") {
    return { todos: [...state.todos, action.payload] };
  }
  return state;
}
// If action is { type: "ADD_TODO", payload: "Buy milk" }
// New state: { todos: ["Buy milk"] }
```

7. **Dispatch**
It tells the Store to use the Reducer to update the data.
```JavaScript
store.dispatch(addTodo("Buy milk")); // Sends the note to update the Store
```

8. **Selector**
A Selector is a helper to grab specific info from the notebook. It’s useful when you only need part of the data.
```JavaScript
function getTodos(state) {
  return state.todos;
}
console.log(getTodos(store)); // Returns ["Buy milk"]
```

## Advantages and Disadvantages
#### Advantages of Redux

- **Predictable State**: Redux ensures state changes follow clear rules, making it easy to understand and debug.
- **Centralized Data**: All app data is in one place (the Store), so everyone (components) knows where to look.
- **Great Tools**: Comes with debugging tools (like Redux DevTools) to track changes.
- **Scalability**: Works well as your app grows with lots of features or users.

#### Disadvantages of Redux

- **Extra Code**: Requires writing more code (e.g., actions, reducers), which can feel like overkill for small apps.
- **Learning Curve**: Takes time to learn, especially if you’re new to state management.
- **Boilerplate**: Repeating patterns can make code longer and less fun to write.

## When Does It Make Sense to Use Redux?

- Use Redux when your app has **complex state** that multiple parts need to access or change (e.g., a big to-do app or e-commerce site).
- It’s great for apps where **data sharing** between components is common.
- Ideal when you need **history tracking** or **undo/redo** features.
- Avoid it for **simple apps** with minimal state (e.g., a basic calculator), where local component state is enough.