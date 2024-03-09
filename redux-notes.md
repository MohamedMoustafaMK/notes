# Redux

-   ### Step 1: Install Redux Toolkit and Redux Persist

    ```bash
    npm install @reduxjs/toolkit react-redux redux-persist
    ```

-   ### Step 2: Create a Redux slice for the counter

    Create a file named `counterSlice.js` to define the reducer logic using createSlice from RTK.

    ```jsx
    // counterSlice.js
    import { createSlice } from '@reduxjs/toolkit'

    const counterSlice = createSlice({
    	name: 'counter',
    	initialState: {
    		value: 0,
    	},
    	reducers: {
    		increment: (state) => {
    			state.value += 1
    		},
    		decrement: (state) => {
    			state.value -= 1
    		},
    		customCounterAmountIncrement: (state, action) => {
    			state.value += action.payload
    		},
    	},
    })

    export const { increment, decrement, customCounterAmountIncrement } =
    	counterSlice.actions
    export default counterSlice.reducer
    ```

-   ### Step 3: Set up your Redux store with Redux Persist

    Create a file named `store.js` to configure your Redux store with Redux Persist.

    ```jsx
    //sotore.js
    import { configureStore, combineReducers } from '@reduxjs/toolkit'
    import counterReducer from './features/counterSlice'

    import storage from 'redux-persist/lib/storage'
    import { persistReducer, persistStore } from 'redux-persist'

    // Define the root reducer by combining all your reducers
    const rootReducer = combineReducers({
    	counter: counterReducer,
    	// Include other reducers if any
    })

    const persistConfig = {
    	key: 'root',
    	storage: storage,
    	// If 'counter' is in the blacklist, it won't be persisted
    	// blacklist: ['counter'],
    }

    const persistedRootReducer = persistReducer(persistConfig, rootReducer)

    const store = configureStore({
    	reducer: persistedRootReducer,
    	middleware: (getDefaultMiddleware) =>
    		getDefaultMiddleware({
    			serializableCheck: false,
    		}),
    })

    const persistor = persistStore(store)

    export { store, persistor }
    ```

      <br>

    ## what is Persistor?

    `PersistGate` is not a normal `div`. It's a special component provided by the `redux-persist` library for integration with React applications using Redux. `PersistGate` is designed to wrap your main component tree and manage the loading and rehydration of the persisted state before rendering your application.

    Here's a breakdown of what `PersistGate` does:

    1. **Loading Delay:**

        - While the persisted state is being retrieved and rehydrated, `PersistGate` can display a loading component (e.g., a spinner) until the process is complete.

    2. **Controlled Rendering:**
        - Once the state is ready, `PersistGate` will render the main component tree, allowing you to control when your application should start rendering based on the state rehydration status.

    Here's an example of how you might use `PersistGate` in your React application:

    ```javascript
    // App.js or index.js
    import React from 'react'
    import { PersistGate } from 'redux-persist/integration/react'
    import { store, persistor } from './store' // Import your store configuration

    function App() {
    	// Your main component logic goes here

    	return (
    		<PersistGate loading={<div>Loading...</div>} persistor={persistor}>
    			{/* Your main component tree goes here */}
    		</PersistGate>
    	)
    }

    export default App
    ```

    In this example, the `loading` prop specifies what should be rendered while the persisted state is being loaded. It can be any React element, not just a `div`. Once the persisted state is ready, the main component tree will be rendered.

    Remember that using `PersistGate` is optional, and if you don't need to control the rendering based on the state rehydration status, you can choose not to use it.

    <br>

-   ### Step 4: Connect the Redux store to your React app with Redux Persist

    In your `index.js` file, wrap your `App` component with the `PersistGate` from `redux-persist/integration/react` to ensure the persistence is applied before rendering your app.

    ```jsx
    // index.js
    import React from 'react'
    import ReactDOM from 'react-dom'
    import { Provider } from 'react-redux'
    import { PersistGate } from 'redux-persist/integration/react'
    import store, { persistor } from './store'
    import App from './App'

    ReactDOM.render(
    	<Provider store={store}>
    		<PersistGate loading={null} persistor={persistor}>
    			<App />
    		</PersistGate>
    	</Provider>,
    	document.getElementById('root'),
    )
    ```

-   ### Step 5: Use the counter state in your React component

    Now, you can use the counter state in your React components as before. The Redux state should persist in the local storage.

    ```jsx
    // App.js
    import React from 'react'
    import { useDispatch, useSelector } from 'react-redux'
    import {
    	increment,
    	decrement,
    	customCounterAmountIncrement,
    } from './reducers/counterSlice'

    function App() {
    	const dispatch = useDispatch()
    	const counter = useSelector((state) => state.counter.value)

    	return (
    		<div>
    			<h1>Counter: {counter}</h1>
    			<button onClick={() => dispatch(increment())}>Increment</button>
    			<button onClick={() => dispatch(decrement())}>Decrement</button>
    			<button
    				onClick={() => dispatch(customCounterAmountIncrement(5))}
    			>
    				Increment by 5
    			</button>
    		</div>
    	)
    }

    export default App
    ```


# Redux Toolkit Async Thunk

## Introduction

This repository provides information about using Redux Toolkit's Async Thunk middleware for handling asynchronous actions in your Redux applications.

## Usage

### Installation

To use Redux Toolkit and Async Thunk, you need to install `@reduxjs/toolkit`:

```bash
npm install @reduxjs/toolkit
```

### Creating an Async Thunk

1. Define an async function that contains the asynchronous logic you want to perform.

```javascript
// asyncActions.js
export const fetchData = async (apiEndpoint) => {
  const response = await fetch(apiEndpoint);
  const data = await response.json();
  return data;
};
```

2. Create an Async Thunk using the `createAsyncThunk` function from Redux Toolkit.

```javascript
// asyncActions.js
import { createAsyncThunk } from '@reduxjs/toolkit';

export const fetchUserData = createAsyncThunk(
  'user/fetchUserData',
  async (apiEndpoint) => {
    const response = await fetch(apiEndpoint);
    const data = await response.json();
    return data;
  }
);
```

### Reducer with Async Thunk

Create a reducer that handles the pending, fulfilled, and rejected states of the async action:

```javascript
// userReducer.js
import { createSlice } from '@reduxjs/toolkit';
import { fetchUserData } from './asyncActions';

const userSlice = createSlice({
  name: 'user',
  initialState: { data: null, status: 'idle', error: null },
  reducers: {},
  extraReducers: (builder) => {
    builder
      .addCase(fetchUserData.pending, (state) => {
        state.status = 'loading';
      })
      .addCase(fetchUserData.fulfilled, (state, action) => {
        state.status = 'succeeded';
        state.data = action.payload;
      })
      .addCase(fetchUserData.rejected, (state, action) => {
        state.status = 'failed';
        state.error = action.error.message;
      });
  },
});

export default userSlice.reducer;
```

### Dispatch Async Thunk

Dispatch the Async Thunk in your component or elsewhere in your application:

```javascript
// App.js
import { useEffect } from 'react';
import { useDispatch, useSelector } from 'react-redux';
import { fetchUserData } from './asyncActions';

function App() {
  const dispatch = useDispatch();
  const userData = useSelector((state) => state.user);

  useEffect(() => {
    dispatch(fetchUserData('https://api.example.com/user'));
  }, [dispatch]);

  return (
    <div>
      {userData.status === 'loading' && <p>Loading...</p>}
      {userData.status === 'succeeded' && <p>User Data: {userData.data}</p>}
      {userData.status === 'failed' && <p>Error: {userData.error}</p>}
    </div>
  );
}

export default App;
```


# Redux Toolkit Data Normalization

## Introduction

This repository provides information about using Redux Toolkit's `createEntityAdapter` for data normalization in your Redux applications.

## Usage

### Installation

To use Redux Toolkit, you need to install `@reduxjs/toolkit`:

```bash
npm install @reduxjs/toolkit
```

### Creating an Entity Adapter

1. Create an Entity Adapter using the `createEntityAdapter` function from Redux Toolkit.

```javascript
// userAdapter.js
import { createEntityAdapter } from '@reduxjs/toolkit';

const userAdapter = createEntityAdapter();

export default userAdapter;
```

### Creating a Slice with Entity Adapter

2. Create a slice that uses the Entity Adapter to handle user entities.

```javascript
// userSlice.js
import { createSlice } from '@reduxjs/toolkit';
import userAdapter from './userAdapter';

const userSlice = createSlice({
  name: 'users',
  initialState: userAdapter.getInitialState(),
  reducers: {
    // Additional reducers can be added here
  },
});

export const { selectAll: selectAllUsers, selectById: selectUserById } = userAdapter.getSelectors((state) => state.users);

export default userSlice.reducer;
```

### Adding Async Thunk with Normalized Data

3. If you have an async operation that fetches user data, you can use Async Thunk along with the Entity Adapter:

```javascript
// asyncActions.js
import { createAsyncThunk } from '@reduxjs/toolkit';
import userAdapter from './userAdapter';

export const fetchUserData = createAsyncThunk('users/fetchUserData', async (apiEndpoint) => {
  const response = await fetch(apiEndpoint);
  const data = await response.json();
  return data;
});

// userSlice.js
import { createSlice } from '@reduxjs/toolkit';
import userAdapter from './userAdapter';
import { fetchUserData } from './asyncActions';

const userSlice = createSlice({
  name: 'users',
  initialState: userAdapter.getInitialState(),
  reducers: {},
  extraReducers: (builder) => {
    builder
      .addCase(fetchUserData.fulfilled, (state, action) => {
        userAdapter.setAll(state, action.payload);
      });
  },
});

export const { selectAll: selectAllUsers, selectById: selectUserById } = userAdapter.getSelectors((state) => state.users);

export default userSlice.reducer;
```

### Dispatch Async Thunk

4. Dispatch the Async Thunk in your component or elsewhere in your application:

```javascript
// App.js
import { useEffect } from 'react';
import { useDispatch, useSelector } from 'react-redux';
import { fetchUserData } from './asyncActions';
import { selectAllUsers } from './userSlice';

function App() {
  const dispatch = useDispatch();
  const users = useSelector(selectAllUsers);

  useEffect(() => {
    dispatch(fetchUserData('https://api.example.com/users'));
  }, [dispatch]);

  return (
    <div>
      <h1>User List</h1>
      {users.map((user) => (
        <div key={user.id}>
          <p>User ID: {user.id}</p>
          <p>Name: {user.name}</p>
          {/* Additional user details */}
        </div>
      ))}
    </div>
  );
}

export default App;
```