# React Hooks

## Table of Contents
1. [Rules of Hooks](#rules-of-hooks)

2. [useState](#usestate): This is the most fundamental hook, which lets you add state to function components. By calling useState, you can declare state variables in a component.

3. [useEffect](#useeffect): This hook lets you perform side effects in function components. It is a powerful tool for data fetching, subscriptions, or manually changing the DOM in React components. You can think of useEffect as componentDidMount, componentDidUpdate, and componentWillUnmount combined.

4. [useContext](#usecontext): This hook allows you to subscribe to React context without introducing nesting. It lets you share values like themes or user data across the component tree without passing props down manually at every level.

5. [useRef](#useref): This hook allows you to persist values between renders without causing a re-render of the component. It can be used to store a mutable value that does not cause re-renders when updated. It’s also useful for referencing DOM elements directly.

6. [useMemo](#usememo): Both hooks let you optimize performance by memoizing values and functions. useMemo saves the computed value of a function so it doesn’t need to be re-executed if its dependencies haven’t changed

7. [useCallback](#usecallback): returns a memoized version of the callback that only changes if one of the dependencies has changed

## Rules of Hooks
React Hooks, introduced in React 16.8, must be used following certain rules to ensure that your components function correctly and to maintain code consistency and readability. Here are the key rules of hooks:

* **Only Call Hooks at the Top Level:** Hooks should be called at the top level of your React function components or custom hooks. This means you shouldn't call hooks inside loops, conditions, or nested functions. This rule ensures that hooks are called in the same order each time a component renders, which is essential for React to correctly preserve the state of hooks across multiple renders.

* **Only Call Hooks from React Functions:** You should only call hooks from React function components or from custom hooks. This rule helps ensure that all stateful logic in a component is clearly visible from its source code and follows React's functional programming paradigm.

* **Use the `eslint-plugin-react-hooks` Plugin:** While this isn’t a rule enforced by React itself, it is highly recommended to use the eslint-plugin-react-hooks which enforces both of the above rules and more at linting time. This plugin will help catch violations of the rules of hooks as part of your development process, making your code safer and more bug-resistant.

These rules are crucial for taking full advantage of React Hooks' capabilities while avoiding bugs and inconsistencies in your application's behavior. Adhering to them ensures that hooks work as expected, maintaining the internal state and lifecycle events of your components correctly across renders.

## useState
The `useState` hook is a fundamental hook in React that lets you add state to functional components. Before hooks, state was only available in class components, but `useState` allows you to use local state within function components.

### Basic Syntax
```javascript
const [state, setState] = useState(initialState);
```
* `state` is the current value of the state variable.
* `setState` is a function that updates the state.
* `initialState` is the value the state is initialized to; it can be any data type.
  
### Simple Example: Counter
Example 1: Counter

```javascript
function Counter() {
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

In this example, the `useState` hook is used to keep track of how many times a button has been clicked.

### Intermediate Example: Form Input
Example 2: Text Input

```javascript
function TextInput() {
  const [text, setText] = useState("");

  const handleChange = (event) => {
    setText(event.target.value);
  };

  return (
    <input type="text" value={text} onChange={handleChange} />
  );
}
```

This example demonstrates how useState can manage the input field’s state. The state updates on every keystroke.

### Complex Example: Multiple State Variables
Example 3: User Registration Form

```javascript
function RegistrationForm() {
  const [formData, setFormData] = useState({
    username: '',
    email: '',
    password: ''
  });

  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData(prevData => ({
      ...prevData,
      [name]: value
    }));
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log(formData);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        name="username"
        value={formData.username}
        onChange={handleChange}
        placeholder="Username"
      />
      <input
        type="email"
        name="email"
        value={formData.email}
        onChange={handleChange}
        placeholder="Email"
      />
      <input
        type="password"
        name="password"
        value={formData.password}
        onChange={handleChange}
        placeholder="Password"
      />
      <button type="submit">Register</button>
    </form>
  );
}
```

In this more complex example, `useState` is used to manage an object containing multiple fields. The `handleChange` function updates the specific field in the object based on the input name.

### Dynamic List Management
Example 4: Todo List

```javascript
function TodoApp() {
  const [todos, setTodos] = useState([]);
  const [text, setText] = useState('');

  const addTodo = () => {
    if (text !== "") {
      setTodos([...todos, { text, id: Date.now() }]);
      setText('');
    }
  };

  return (
    <div>
      <input
        type="text"
        value={text}
        onChange={(e) => setText(e.target.value)}
      />
      <button onClick={addTodo}>Add Todo</button>
      <ul>
        {todos.map(todo => (
          <li key={todo.id}>{todo.text}</li>
        ))}
      </ul>
    </div>
  );
}
```

Here, `useState` is used for managing a list of todos and a text input. This demonstrates handling arrays in state, showing how to add new items without mutating the original state array.

### Best Practices and Tips
1. Initialization: Use lazy initialization for expensive calculations:

    ```javascript
    const [value, setValue] = useState(() => computeExpensiveValue());
    ```

2. Functional Updates: When updating state based on previous state, use functional updates to ensure that you are working with the most current state:

    ```javascript
    setCount(prevCount => prevCount + 1);
    ```
    
3. Object Updates: Remember to spread previous state when updating objects or arrays to avoid accidental state mutations:

    ```javascript
    setFormData(prev => ({ ...prev, ...newData }));
    ```

`useState` is a highly flexible hook that can handle various types of data, making it suitable for nearly any kind of state management scenario in a functional component.

## useEffect
`useEffect` is a versatile hook in React that manages side effects in functional components. It replaces lifecycle methods such as `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` from class components, providing a unified API to handle side effects.

### Basic Syntax and Examples
The basic syntax of useEffect is as follows:

```javascript
useEffect(() => {
  // Code to run on mount and updates
  return () => {
    // Cleanup code
  };
}, [dependencies]);
```

* The first argument is a function that React will run after the DOM updates.
* The optional second argument is a dependencies array that tells React when to re-run the effect.

### Example 1: Component Did Mount

```javascript
Copy code
useEffect(() => {
  // This code runs after the component mounts
  console.log('Component mounted');
}, []); // Empty dependency array means this effect runs only once
```

### Example 2: Component Did Update

```javascript
const [count, setCount] = useState(0);

useEffect(() => {
  // This runs after `count` changes
  document.title = `You clicked ${count} times`;
}, [count]); // Effect depends on `count`
```

Example 3: Component Will Unmount

```javascript
useEffect(() => {
  return () => {
    // This code runs when the component is about to unmount
    console.log('Component will unmount');
  };
}, []); // Effect runs only once
```

### Gotchas
* Skipping the Dependency Array: Without a dependencies array, useEffect will run after every render, which can lead to performance issues or unexpected behavior.
* Incorrect Dependency Array: If the dependencies array does not include every variable used inside the effect that changes over time, it can lead to bugs where old values are used.
* Overfetching in Effects: Placing API calls directly inside useEffect without any conditions can lead to unnecessary data fetching on every render.

#### Incorrect Dependency Array
Handling missing dependencies in the useEffect hook is a common challenge when developing React applications. Here are strategies to manage dependencies effectively, ensuring that your effects run correctly without introducing bugs:

1. Always Include All Used State and Props

The simplest rule is to always include all state and props that you use inside the effect in the dependencies array. This ensures that if any of these values change, the effect will rerun, using the latest values.

Example: Correct Dependencies
```javascript
const [count, setCount] = useState(0);

useEffect(() => {
  const interval = setInterval(() => {
    console.log(count); // `count` is included in the dependencies array
  }, 1000);

  return () => clearInterval(interval);
}, [count]); // Correctly includes `count`
```

2. Refactor Your Code to Minimize Dependencies

If your effect depends on a prop or state value that changes frequently, causing the effect to run too often, consider refactoring your component. Sometimes, splitting a component into smaller parts or changing the structure of your state can help reduce unnecessary dependencies.

Example: Refactoring to Reduce Dependencies

```javascript
const useInterval = (callback, delay) => {
  const savedCallback = useRef(callback);

  // Remember the latest callback.
  useEffect(() => {
    savedCallback.current = callback;
  }, [callback]);

  // Set up the interval.
  useEffect(() => {
    function tick() {
      savedCallback.current();
    }
    if (delay !== null) {
      let id = setInterval(tick, delay);
      return () => clearInterval(id);
    }
  }, [delay]); // `delay` is stable, doesn't depend on changing state directly
}
```

3. Use a Ref for Values You Don’t Want to Trigger Reruns
   
If you need to use a value inside an effect but don’t want changes to it to cause the effect to rerun, you can store the value in a `useRef`. This is useful for values that are used for reading in the effect but shouldn’t necessarily trigger it to re-execute.

Example: Using Refs to Ignore Updates
```javascript
const [count, setCount] = useState(0);
const countRef = useRef(count);

useEffect(() => {
  const timer = setTimeout(() => {
    console.log(countRef.current); // Reads from ref, changes do not trigger rerun
  }, 1000);
  
  return () => clearTimeout(timer);
}, []); // Empty dependency array, effect runs only once

// Update ref whenever count changes
useEffect(() => {
  countRef.current = count;
}, [count]);
```

4. Use Functional Updates for SetState When Possible

If you need to update state based on the previous state and want to avoid including it in the dependencies array, you can use a functional update. This lets you update the state without depending on its current value in the effect.

Example: Functional Update for State
```javascript
const [count, setCount] = useState(0);

useEffect(() => {
  const interval = setInterval(() => {
    setCount(currentCount => currentCount + 1); // No dependency on `count`
  }, 1000);

  return () => clearInterval(interval);
}, []); // No need to include `count`
```

By using these strategies, you can manage your dependencies more effectively, ensuring that your effects are both correct and performant.

### Good Use Cases
* Fetching Data: Ideal for API calls but should be combined with condition checks or dependencies to prevent overfetching.
* Setting up Subscriptions or Event Listeners: Useful for adding event listeners to the DOM or subscribing to a data source, with cleanup to remove them.
* Synchronizing with External Systems: Such as updating the document title or syncing with local storage.

Example: Fetching Data

```javascript
useEffect(() => {
  const fetchData = async () => {
    const response = await fetch('https://api.example.com/data');
    const data = await response.json();
    console.log(data);
  };

  fetchData();
}, []); // Run once on mount
```

### Bad Use Cases
* Heavy Computations: Heavy synchronous computations in useEffect can block rendering. Use useMemo for expensive calculations instead.
* Non-Dependent Side Effects: If you're using variables inside useEffect that change over time but aren't included in the dependencies array, it can lead to bugs.
* 
Example: Misusing Dependencies

```javascript
const [count, setCount] = useState(0);

useEffect(() => {
  const timer = setTimeout(() => {
    // This may not always log the latest count
    console.log(count);
  }, 1000);

  return () => clearTimeout(timer);
}, []); // `count` is missing from dependencies
```

To make the most out of `useEffect`, always ensure your dependencies array is correct, understand when your effects run, and clean up any external subscriptions or event listeners to avoid memory leaks.



## useContext
The `useContext` hook in React allows functional components to access the value of a React context. This hook simplifies the process of passing data through the component tree without having to pass props manually at every level.

### Basic Syntax
```javascript
const value = useContext(MyContext);
```
* `MyContext` is the context object (the value returned from` React.createContext()`).
* `value` will be equal to the current context value for that context, determined by the closest matching `Provider` above it in the tree.
  
Simple Example: Theme Context
Example 1: Using Context to Manage Themes

```javascript
import React, { useContext, createContext, useState } from 'react';

// Create a Context
const ThemeContext = createContext();

function ThemeProvider({ children }) {
  const [theme, setTheme] = useState('light');
  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

function Button() {
  const { theme, setTheme } = useContext(ThemeContext);
  return (
    <button onClick={() => setTheme(theme === 'light' ? 'dark' : 'light')}>
      Switch to {theme === 'light' ? 'dark' : 'light'} theme
    </button>
  );
}

function App() {
  return (
    <ThemeProvider>
      <div>
        <Button />
      </div>
    </ThemeProvider>
  );
}
```

In this example, `ThemeContext` allows any component within the `ThemeProvider` to read or update the theme without prop drilling.

Intermediate Example: Authentication Context
Example 2: Using Context for User Authentication

```javascript
import React, { useContext, createContext, useState } from 'react';

const AuthContext = createContext(null);

function AuthProvider({ children }) {
  const [user, setUser] = useState(null);

  const login = (username) => {
    setUser({ username });
  };

  const logout = () => {
    setUser(null);
  };

  return (
    <AuthContext.Provider value={{ user, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
}

function Login() {
  const { login } = useContext(AuthContext);
  return <button onClick={() => login('JohnDoe')}>Log in</button>;
}

function UserProfile() {
  const { user, logout } = useContext(AuthContext);
  if (!user) {
    return <div>Please log in</div>;
  }
  return (
    <div>
      Welcome {user.username}! <button onClick={logout}>Log out</button>
    </div>
  );
}

function App() {
  return (
    <AuthProvider>
      <Login />
      <UserProfile />
    </AuthProvider>
  );
}
```

This example provides an authentication context that can be accessed by any component within the `AuthProvider` to display user information or manage login/logout actions.

Complex Example: Language and Localization Context
Example 3: Multi-Language Support

```javascript
import React, { useContext, createContext, useState } from 'react';

const LanguageContext = createContext();

function LanguageProvider({ children }) {
  const [language, setLanguage] = useState('en');
  const phrases = {
    en: { greeting: "Hello" },
    fr: { greeting: "Bonjour" },
    es: { greeting: "Hola" }
  };

  return (
    <LanguageContext.Provider value={{ language, setLanguage, phrases: phrases[language] }}>
      {children}
    </LanguageContext.Provider>
  );
}

function Greeting() {
  const { phrases, setLanguage } = useContext(LanguageContext);
  return (
    <div>
      {phrases.greeting}
      <button onClick={() => setLanguage('fr')}>French</button>
      <button onClick={() => setLanguage('es')}>Spanish</button>
    </div>
  );
}

function App() {
  return (
    <LanguageProvider>
      <Greeting />
    </LanguageProvider>
  );
}
```
This example shows how to use context for language and localization, allowing any component to access and modify the current language and get the correct phrases.

### Good Use Cases
* **Global State Management:** Ideal for data like user authentication, themes, or preferred languages, which needs to be accessed throughout the application.
* **Avoiding Prop Drilling:** When you need to pass data through many layers of components, useContext reduces complexity.

### Bad Use Cases
* **High-Frequency Updates:** Context is not optimized for high-frequency updates. Using context for frequently changing values (like the state of an animation or rapidly updating data) can lead to performance issues.
* **Local Component State:** Using context as a substitute for local component state management can overcomplicate the component architecture unnecessarily.

`useContext` is a powerful tool for specific scenarios where shared state or behaviors are logically scoped to a large part of your application's component tree. However, it should be used judiciously to avoid performance pitfalls and unnecessary re-renders.

## useRef
The `useRef` hook in React is a versatile tool that provides a way to persist values across renders without causing the component to re-render. It returns a mutable ref object whose `.current` property is initialized to the passed argument. The object returned from `useRef` will persist for the lifetime of the component.

### Basic Syntax
```javascript
const refContainer = useRef(initialValue);
```

### Examples
Example 1: Accessing DOM Elements
One of the most common uses of useRef is to access DOM elements directly. You can use the ref as a way to hold a reference to a DOM node.

```javascript
function TextInputWithFocusButton() {
  const inputEl = useRef(null);

  const onButtonClick = () => {
    // Explicitly focus the text input using the raw DOM API
    inputEl.current.focus();
  };

  return (
    <>
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
}
```

Example 2: Storing Previous State or Props
`useRef` can be used to keep track of previous state or props value, which can be useful in effects where you need to compare the previous and current value.

```javascript
function Counter() {
  const [count, setCount] = useState(0);
  const prevCountRef = useRef();

  useEffect(() => {
    prevCountRef.current = count;
  }, [count]);

  return (
    <div>
      <h1>Now: {count}, before: {prevCountRef.current}</h1>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

### Gotchas
1. **Modifying `.current` Does Not Trigger Re-render:** Changes to the `.current` property do not cause the component to re-render. This can be a feature or a bug depending on what you’re trying to achieve.

2. **Initialization and Referential Integrity:** The initial value of `.current` is set only once during the initial render. If you pass props or state to `useRef` as an initial value, it won't update when props or state changes.

### Good Use Cases
* **Manipulating DOM Elements:** Perfect for cases when you need to directly interact with a DOM node, like setting focus, scrolling an item into view, or integrating with third-party DOM libraries.
* **Storing the Previous Values:** Useful for comparing previous and current props or state inside `useEffect`.
* **Storing Instances:** Such as timers (e.g., `setTimeout` or `setInterval`) or other mutable values that shouldn't cause a re-render when updated.

Example: Storing Instances

```javascript
function TimerComponent() {
  const intervalRef = useRef();

  useEffect(() => {
    intervalRef.current = setInterval(() => {
      console.log('Timer tick');
    }, 1000);

    return () => clearInterval(intervalRef.current);
  }, []);

  return <div>Check the console for timer ticks.</div>;
}
```

### Bad Use Cases
* **Avoid Using Ref for Deriving Data:** Ref should not be used as a workaround to avoid re-rendering when deriving data from props or state. Instead, use memoization techniques like useMemo.
* **Overusing Refs for Business Logic:** Storing everything in refs to avoid re-renders can lead to a design where component's local state is difficult to track and debug. Use state management appropriately.

`useRef` is a powerful hook when used properly. It can help manage focus, manage timers, and read values across renders without additional rendering costs, but it should be used judiciously to keep your components' logic clear and maintainable.

## useMemo
The `useMemo` hook in React is used to memoize expensive calculations. It returns a memoized value, meaning the value is recalculated only when one of its dependencies has changed. This can help to avoid costly recalculations on every render and can improve performance in certain scenarios.

### Basic Syntax
```javascript
const memoizedValue = useMemo(() => computeExpensiveValue(), [dependencies]);
```

* The first parameter is a function that returns the value you want to memoize.
* The second parameter is an array of dependencies. The memoized function will only recompute when one of these dependencies has changed.

Simple Example: Memoizing a Computed Value
Example 1: Calculating Factorial

```javascript
import { useMemo, useState } from 'react';

function Factorial() {
  const [number, setNumber] = useState(1);
  const factorial = useMemo(() => {
    const calculateFactorial = n => (n <= 0 ? 1 : n * calculateFactorial(n - 1));
    return calculateFactorial(number);
  }, [number]);

  return (
    <div>
      Factorial of 
      <input 
        type="number" 
        value={number} 
        onChange={e => setNumber(Number(e.target.value))}
      />
      is {factorial}
    </div>
  );
}
```

This example shows how `useMemo` is used to calculate the factorial of a number only when the number changes, avoiding unnecessary recalculations.

Intermediate Example: Memoizing Components
Example 2: Memoizing a List Component

```javascript
import { useMemo, useState } from 'react';

function List({ items }) {
  const sortedList = useMemo(() => {
    const sortedItems = [...items];
    sortedItems.sort((a, b) => a - b);
    return sortedItems.map(item => <li key={item}>{item}</li>);
  }, [items]);

  return <ul>{sortedList}</ul>;
}

function App() {
  const [numberList, setNumberList] = useState([3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5]);

  return (
    <div>
      <List items={numberList} />
      <button onClick={() => setNumberList([...numberList, Math.floor(Math.random() * 10)])}>
        Add Number
      </button>
    </div>
  );
}
```

This example demonstrates how `useMemo` can be used to sort a list only when the items in the list change, thus avoiding unnecessary computations on every render.

Complex Example: Memoizing with Multiple Dependencies
Example 3: Expense Report Calculation

```javascript
import { useMemo, useState } from 'react';

function ExpenseReport({ expenses, filter }) {
  const filteredExpenses = useMemo(() => {
    return expenses.filter(e => e.amount > filter.minAmount && e.category === filter.category);
  }, [expenses, filter]);

  const total = useMemo(() => {
    return filteredExpenses.reduce((sum, current) => sum + current.amount, 0);
  }, [filteredExpenses]);

  return (
    <div>
      Total Expense: ${total}
      <ul>
        {filteredExpenses.map(expense => (
          <li key={expense.id}>{expense.description}: ${expense.amount}</li>
        ))}
      </ul>
    </div>
  );
}
```

In this example, useMemo is used to filter and calculate the total of expenses, which are recomputed only when expenses or filter changes.

### Good Use Cases
* Expensive Calculations: Ideal for expensive calculations that don’t need to be recomputed on every render unless specific data changes.
* Referential Equality: Useful when you need to maintain the same reference between renders if the inputs have not changed (e.g., complex configurations, large data sets).
### Bad Use Cases
* Simple Calculations: Using `useMemo` for trivial calculations is unnecessary and can lead to more overhead than benefit.
* Running Effects: `useMemo` should not be used for side effects; useEffect is designed for handling side effects.
* 
`useMemo` is a powerful optimization tool when used correctly. It helps avoid unnecessary computations and maintains referential equality, which can prevent unnecessary renders in child components that rely on reference equality for performance optimizations (like `React.memo` or `shouldComponentUpdate`). However, it should be used judiciously and not for every value or function in a component, as misuse can lead to more complex and less performant code.

## useCallback
The `useCallback` hook in React is used to memoize callback functions. This hook is particularly useful when passing callbacks to optimized child components that rely on reference equality to prevent unnecessary renders. It returns a memoized version of the callback that only changes if one of the dependencies has changed.

### Basic Syntax
```javascript
const memoizedCallback = useCallback(() => {
    doSomething(a, b);
}, [a, b]);
```

* The first parameter is the callback function you want to memoize.
* The second parameter is an array of dependencies. The callback will only be recomputed if one of these dependencies changes.

Simple Example: Increment Counter
Example 1: Memoizing a Counter Callback

```javascript
import { useState, useCallback } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  const increment = useCallback(() => {
    setCount(prevCount => prevCount + 1);
  }, []);

  return (
    <div>
      Count: {count}
      <button onClick={increment}>Increment</button>
    </div>
  );
}
```

This example shows how `useCallback` can be used to ensure that the increment function does not get recreated on every render unless its dependencies change. Since there are no dependencies, the function is created only once.

Intermediate Example: Passing Callbacks to Child Components
Example 2: Memoizing Callbacks Passed to Child Components

```javascript
import { useState, useCallback } from 'react';

function Button({ onClick, children }) {
  console.log("Button rendered:", children);
  return <button onClick={onClick}>{children}</button>;
}

const MemoizedButton = React.memo(Button);

function App() {
  const [count, setCount] = useState(0);
  const [otherState, setOtherState] = useState(false);

  const increment = useCallback(() => {
    setCount(prevCount => prevCount + 1);
  }, []);

  return (
    <div>
      <MemoizedButton onClick={increment}>Increment</MemoizedButton>
      <button onClick={() => setOtherState(!otherState)}>Toggle Other State</button>
      <p>Other state: {otherState.toString()}</p>
    </div>
  );
}
```

In this example, the `increment` callback is passed to a memoized `Button` component. Using `useCallback` ensures that the `Button` component does not re-render unnecessarily when App re-renders due to changes in otherState, as the `increment` function’s reference remains the same.

Complex Example: Callback with Multiple Dependencies
Example 3: Using useCallback with Multiple Dependencies

```javascript
import { useState, useCallback } from 'react';

function SearchResults({ query, onSearch }) {
  console.log("Rendering SearchResults");
  return (
    <div>
      <input 
        type="text" 
        value={query} 
        onChange={(e) => onSearch(e.target.value)} 
        placeholder="Search..." 
      />
    </div>
  );
}

const MemoizedSearchResults = React.memo(SearchResults);

function App() {
  const [query, setQuery] = useState("");
  const [otherState, setOtherState] = useState(false);

  const handleSearch = useCallback((newQuery) => {
    setQuery(newQuery);
  }, []);

  return (
    <div>
      <MemoizedSearchResults query={query} onSearch={handleSearch} />
      <button onClick={() => setOtherState(!otherState)}>Toggle Other State</button>
      <p>Other state: {otherState.toString()}</p>
    </div>
  );
}
```

Here, `handleSearch` uses `useCallback` to avoid unnecessary re-renders of the `MemoizedSearchResults` component when other parts of the component tree update (`otherState` in this case).

### Good Use Cases
* Optimized Child Components: Useful when passing callbacks to child components that should only re-render when actual changes occur.
* Complex Callbacks with Dependencies: When callbacks depend on props or state that might change frequently, `useCallback` can help in reducing unnecessary recalculations and re-renders.
### Bad Use Cases
* **Trivial Callbacks:** Using `useCallback` for simple callbacks (like setting state) that are passed to components that do not require memoization can introduce unnecessary complexity and overhead.
* **Static Callbacks without Dependencies:** If a callback does not depend on props or state, defining it inside the component without `useCallback` can be simpler and more efficient, especially if it’s not passed down.
  
`useCallback` is a powerful tool when used in the right context, particularly in performance optimizations involving deeply nested components or complex React applications. However, it should be used judiciously to avoid premature optimization and additional complexity in cases where it's not beneficial.