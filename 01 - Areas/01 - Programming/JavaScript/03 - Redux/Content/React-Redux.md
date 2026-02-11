---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - JavaScript
  - React_JS
  - redux
note type: Informational Note
---
`react-redux` is a js module, that helps to work with these libraries.
### Why Use React-Redux?
1. **React Integration**: React-Redux bridges Redux with React, allowing components to access and update the store efficiently without manual subscriptions.
2. **Performance Optimization**: React-Redux optimizes component re-rendering by only updating components when relevant state changes occur.
3. **Developer Tools**: Redux offers powerful debugging tools like Redux DevTools for tracking state changes over time.

### Provider
- A React component provided by React-Redux that wraps the root of your React application.
- It makes the Redux store available to all components in the component tree without needing to pass the store as a prop.

```JavaScript
import { Provider } from 'react-redux';
import store from './store';

function App() {
  return (
    <Provider store={store}>
      <YourApp />
    </Provider>
  );
}
```

### connect(), mapStateProps(), mapDispatchToProps()

`connect()`
- A higher-order component (HOC) that connects a React component to the Redux store.
- It allows components to access state and dispatch actions without directly interacting with the store.

```JavaScript
import { connect } from 'react-redux';

const MyComponent = ({ someState, someAction }) => (
  <div>{someState} <button onClick={someAction}>Click</button></div>
);

export default connect(mapStateToProps, mapDispatchToProps)(MyComponent);
```

`mapStateToProps()`
- A function that maps parts of the Redux store’s state to the component’s props.
- It defines which pieces of the state the component needs.

```JavaScript
const mapStateToProps = (state) => ({
  someState: state.someReducer.someValue,
});
```

`mapDispatchToProps()`
- A function that maps action creators to the component’s props, allowing the component to dispatch actions to the Redux store.

```JavaScript
import { someActionCreator } from './actions';

const mapDispatchToProps = (dispatch) => ({
  someAction: () => dispatch(someActionCreator()),
});
```