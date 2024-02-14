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
