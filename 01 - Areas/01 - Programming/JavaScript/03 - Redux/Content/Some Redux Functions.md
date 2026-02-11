---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - JavaScript
  - redux
note type: Informational Note
---
### combineReducers()
`combineReducers()` is a helper function in Redux that lets you **split your app’s state** into smaller, manageable pieces, each handled by its own reducer. It then combines these reducers into one big reducer that the Redux Store can use to manage the entire state. 

- When an action is dispatched, `combineReducers()` runs **each smaller reducer** with its slice of the state and the action, then combines the results into the new overall state.
### applyMiddleware()
- **Add Extra Features**:
    - Middleware lets you add capabilities to Redux that aren’t built-in, like handling asynchronous actions (e.g., API calls), logging, or crash reporting.
- **Intercept Actions**:
    - It sits between the dispatch (when you send an action) and the reducer (where the state updates). This middleman can change, delay, or even stop the action before it reaches the reducer.
- **Enhance the Store**:
    - applyMiddleware() takes middleware functions and applies them to the Store, giving it new superpowers while keeping the core Redux flow intact.

### bindActionCreators()
- **Simplify Dispatching**:
    - Normally, you’d need to call `store.dispatch()` every time you use an action creator. bindActionCreators() wraps the action creators so they automatically dispatch their actions for you.
- **Help Components**:
    - It’s especially useful when you want to pass action creators to React components (e.g., via connect from React-Redux) without the component needing to know about dispatch.
- **Reduce Boilerplate**:
    - It saves you from writing repetitive dispatch calls, making your code cleaner.

*Example*:
```JavaScript
import { bindActionCreators } from "redux";

const actions = bindActionCreators({ addTodo, toggleTodo }, store.dispatch);

// Direct calls 
actions.addTodo("Buy milk"); 
actions.toggleTodo(1);    
```