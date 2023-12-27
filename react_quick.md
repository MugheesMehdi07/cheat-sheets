
# React with Redux Cheat Sheet

## Basic React Setup

```bash
# Install React and create a new app
npx create-react-app my-app
cd my-app
npm start
```

## Functional Component

```javascript
import React from 'react';

function MyComponent() {
  return <h1>Hello, React!</h1>;
}

export default MyComponent;
```

## Using State Hook

```javascript
import React, { useState } from 'react';

function MyComponent() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

## Using Effect Hook

```javascript
import React, { useState, useEffect } from 'react';

function MyComponent() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

## Redux Setup

### Install Redux

```bash
npm install redux react-redux
```

### Create a Redux Store

```javascript
// store.js
import { createStore } from 'redux';

function reducer(state = { count: 0 }, action) {
  switch (action.type) {
    case 'INCREMENT':
      return { count: state.count + 1 };
    default:
      return state;
  }
}

const store = createStore(reducer);

export default store;
```

### Provide the Store to React

```javascript
// index.js
import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';
import App from './App';
import store from './store';

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);
```

## Connecting React Components to Redux

```javascript
import React from 'react';
import { useSelector, useDispatch } from 'react-redux';

function MyComponent() {
  const count = useSelector(state => state.count);
  const dispatch = useDispatch();

  return (
    <div>
      <p>{count}</p>
      <button onClick={() => dispatch({ type: 'INCREMENT' })}>
        Increment
      </button>
    </div>
  );
}

export default MyComponent;
```

## Async Actions with Redux Thunk

### Install Redux Thunk

```bash
npm install redux-thunk
```

### Configure Redux Store with Thunk

```javascript
// store.js
import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';

const store = createStore(
  reducer,
  applyMiddleware(thunk)
);

export default store;
```

### Async Action Creators

```javascript
function fetchData() {
  return dispatch => {
    fetch('https://api.example.com/data')
      .then(response => response.json())
      .then(data => dispatch({ type: 'FETCH_DATA_SUCCESS', data }));
  };
}
```

## React Router for Navigation

### Install React Router

```bash
npm install react-router-dom
```

### Setup Routes

```javascript
import React from 'react';
import { BrowserRouter as Router, Route, Link } from 'react-router-dom';

function App() {
  return (
    <Router>
      <nav>
        <Link to="/">Home</Link>
        <Link to="/about">About</Link>
      </nav>

      <Route path="/" exact component={Home} />
      <Route path="/about" component={About} />
    </Router>
  );
}

function Home() {
  return <h1>Home Page</h1>;
}

function About() {
  return <h1>About Page</h1>;
}

export default App;
```
