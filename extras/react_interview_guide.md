# Complete React JS Interview Guide
## 50+ Questions | Beginner to Advanced | 2025

**Target Audience:** Freshers, MCA/B.Tech students, Mphasis & FAANG
**Framework:** React 16.8+ (Hooks focus)
**Difficulty Levels:** Beginner, Intermediate, Advanced, Expert
**Time to Master:** 2-3 weeks

---

## **REACT FUNDAMENTALS (10 Questions)**

### **1. What is React and why is it used?**

**Answer:**
React is a **JavaScript library** (not a framework) developed by Facebook for building user interfaces with reusable components.

**Why React:**
- **Component-based:** Break UI into reusable pieces
- **Virtual DOM:** Efficient updates, better performance
- **One-way data binding:** Data flows parent → child (predictable)
- **Declarative:** Describe what UI should look like, React handles DOM updates
- **Large ecosystem:** Redux, React Router, etc.

**Use Cases:**
- Single Page Applications (SPAs)
- Mobile apps (React Native)
- Progressive Web Apps (PWAs)
- Complex UIs with frequent updates

---

### **2. What is JSX?**

**Answer:**
JSX is **JavaScript XML** - syntax extension that allows writing HTML-like code in JavaScript.

```jsx
// JSX
const element = <h1 className="greeting">Hello, World!</h1>;

// Transpiles to:
const element = React.createElement('h1', { className: 'greeting' }, 'Hello, World!');
```

**Key Points:**
- Not valid JavaScript (must be transpiled by Babel)
- More readable than React.createElement()
- Can embed expressions using `{}`
- Always return single root element (or use fragment `<>...</>`)

**Common Mistakes:**
```jsx
// ❌ Wrong: Can't use 'class' (reserved keyword)
<div class="container"></div>

// ✅ Correct: Use 'className'
<div className="container"></div>

// ❌ Wrong: Reserved keywords
<div for="input"></div>

// ✅ Correct: Use 'htmlFor'
<label htmlFor="input"></label>
```

---

### **3. What is the difference between Functional and Class Components?**

**Functional Components:**
```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

**Class Components:**
```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

**Comparison Table:**

| Feature | Functional | Class |
|---------|-----------|-------|
| Syntax | Function returning JSX | Class extending React.Component |
| State (pre-Hooks) | ❌ Not possible | ✅ this.state |
| Lifecycle Methods | ❌ Not direct (use Hooks) | ✅ componentDidMount, etc. |
| This binding | ❌ No 'this' | ✅ Needs binding |
| Performance | ✅ Slightly faster | Slightly slower |
| Readability | ✅ Cleaner | More verbose |
| Modern Practice | ✅ Preferred (Hooks) | Older pattern |

**Modern Approach:** Functional components with Hooks are now standard.

---

### **4. What are Props?**

**Answer:**
Props (properties) are **read-only data passed from parent to child** components.

```jsx
// Parent Component
function App() {
  return <Greeting name="Alice" age={25} />;
}

// Child Component receives props
function Greeting(props) {
  console.log(props); // { name: 'Alice', age: 25 }
  return <p>Hello, {props.name}! You are {props.age}.</p>;
}

// Or using destructuring (cleaner)
function Greeting({ name, age }) {
  return <p>Hello, {name}! You are {age}.</p>;
}
```

**Key Characteristics:**
- **Immutable:** Child cannot modify props
- **One-way flow:** Parent → Child only
- **Type checking:** Use PropTypes or TypeScript
- **Default values:** Can set defaultProps

```jsx
function Button({ label = "Click me" }) {
  return <button>{label}</button>;
}
```

---

### **5. What is State?**

**Answer:**
State is **mutable data that belongs to a component** and can be updated.

**With Hooks (Modern):**
```jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0); // count = state, setCount = updater
  
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

**Key Differences from Props:**

| Props | State |
|-------|-------|
| Immutable | Mutable |
| Passed from parent | Local to component |
| Read-only | Can be updated |
| For data | For UI/behavior |

**State Rules:**
- Don't mutate state directly
- Treat state as immutable
- Use updater function for previous state

```jsx
// ❌ Wrong: Direct mutation
count = count + 1;

// ✅ Correct: Use setter
setCount(count + 1);

// ✅ Better: Use previous state
setCount(prev => prev + 1);
```

---

### **6. What is Virtual DOM and how does it work?**

**Answer:**
Virtual DOM is an **in-memory representation of the real DOM**.

**How it works:**
1. When state/props change, React creates new Virtual DOM tree
2. Compares (diffs) new Virtual DOM with old one
3. Identifies changed elements (reconciliation)
4. Updates only changed elements in real DOM (batched)

**Example:**
```
State change: name = "Bob"
        ↓
React creates new Virtual DOM
        ↓
Diffing algorithm compares old vs new
        ↓
Finds: <p>Hello, Bob</p> changed
        ↓
Updates only that element in real DOM
```

**Benefits:**
- **Batching updates:** Multiple changes → single DOM update
- **Performance:** Real DOM updates are expensive
- **Developer experience:** Don't think about DOM, just state

**Real DOM operations are ~1000x slower than Virtual DOM operations!**

---

### **7. What is Reconciliation?**

**Answer:**
Process where React **compares old and new Virtual DOM** and decides what to update.

**Keys Concepts:**
- **Diffing:** Line-by-line comparison of Virtual DOM trees
- **Element Type Changes:** If type changed, old tree discarded, new tree created
- **Key attribute:** Helps React identify which items changed in lists

**Without Keys (Bad):**
```jsx
// Reorders items, might cause state/focus issues
{todos.map(todo => <TodoItem todo={todo} />)}
```

**With Keys (Good):**
```jsx
// React knows which item is which
{todos.map(todo => <TodoItem key={todo.id} todo={todo} />)}
```

---

### **8. What is the difference between Real DOM and Virtual DOM?**

| Real DOM | Virtual DOM |
|----------|------------|
| Actual DOM in browser | In-memory representation |
| Updates are slow | Updates are fast |
| Direct manipulation expensive | Efficient diffing |
| Browser re-renders entire page | React batches updates |
| 1 update = 1 reflow/repaint | Multiple updates batched |
| Direct access via selectors | Abstracted by React |

---

### **9. What is a Component and why are they used?**

**Answer:**
A component is a **reusable piece of UI** that returns JSX.

**Why Components:**
- **Modularity:** Break UI into manageable pieces
- **Reusability:** Write once, use many places
- **Maintainability:** Easier to update and test
- **Scalability:** Compose complex UIs from simple components

**Component Hierarchy Example:**
```
App
├── Header
│   └── NavBar
├── Main
│   ├── Sidebar
│   └── Content
└── Footer
```

---

### **10. What is the difference between State and Props?**

| State | Props |
|-------|-------|
| Owned by component | Passed from parent |
| Mutable (via setState/Hooks) | Immutable |
| Local to component | Can be shared |
| Updated internally | Updated externally |
| Causes re-render on change | Causes re-render on change |

---

## **REACT HOOKS (15 Questions)**

### **11. What are React Hooks and why were they introduced?**

**Answer:**
Hooks are **functions that let you use state and other features in functional components** without writing class components.

**Why Introduced:**
- Avoid class component complexity (this binding, lifecycle methods)
- Reuse logic across components (custom hooks)
- Better code organization
- Easier to test

**Core Hooks:**
- `useState` - Manage state
- `useEffect` - Side effects
- `useContext` - Access context
- `useRef` - Access DOM directly
- `useReducer` - Complex state logic

---

### **12. Explain useState Hook with examples**

**Answer:**
`useState` adds state to functional components.

```jsx
const [state, setState] = useState(initialValue);
```

**Basic Example:**
```jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);
  
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <button onClick={() => setCount(0)}>Reset</button>
    </div>
  );
}
```

**Multiple States:**
```jsx
function Form() {
  const [name, setName] = useState('');
  const [email, setEmail] = useState('');
  const [age, setAge] = useState(0);
  
  // Equivalent to this.state = { name, email, age } in class
}
```

**Using Previous State (Important):**
```jsx
// ❌ Wrong: Can have stale closure issues
const increment = () => setCount(count + 1);

// ✅ Correct: Use function to access latest state
const increment = () => setCount(prev => prev + 1);
```

**Lazy Initialization:**
```jsx
// If initial state is expensive to compute
const [state, setState] = useState(() => {
  // This function runs only once
  return expensiveComputation();
});
```

---

### **13. Explain useEffect Hook**

**Answer:**
`useEffect` runs **side effects** (fetch data, subscribe, update DOM) in functional components.

**Syntax:**
```jsx
useEffect(() => {
  // Effect logic
  return () => {
    // Cleanup (optional)
  };
}, [dependencies]);
```

**Dependency Array Controls When Effect Runs:**

```jsx
// 1. No dependency array → Runs after EVERY render
useEffect(() => {
  console.log('Runs on every render');
});

// 2. Empty array → Runs ONCE on mount
useEffect(() => {
  console.log('Runs once on mount');
}, []);

// 3. With dependencies → Runs when dependencies change
useEffect(() => {
  console.log('Runs when count changes');
}, [count]);
```

**Common Use Cases:**

```jsx
// Fetch data on mount
useEffect(() => {
  const fetchData = async () => {
    const response = await fetch('/api/data');
    setData(await response.json());
  };
  fetchData();
}, []); // Empty array = run once on mount

// Subscribe to events
useEffect(() => {
  window.addEventListener('resize', handleResize);
  
  // Cleanup function
  return () => window.removeEventListener('resize', handleResize);
}, []);

// Update document title
useEffect(() => {
  document.title = `Count: ${count}`;
}, [count]); // Run when count changes
```

**Pitfalls:**
```jsx
// ❌ Missing dependency → Stale closure
const handleClick = () => setName(name + ' updated');
useEffect(() => {
  const timer = setTimeout(handleClick, 1000);
  return () => clearTimeout(timer);
}, []); // name is stale!

// ✅ Add dependency
useEffect(() => {
  const timer = setTimeout(() => setName(name + ' updated'), 1000);
  return () => clearTimeout(timer);
}, [name]);
```

---

### **14. What is useContext Hook and how does it solve prop drilling?**

**Answer:**
`useContext` allows sharing state without passing props through every component (prop drilling).

**Problem - Prop Drilling:**
```jsx
// Passing theme prop through many levels
<App theme="dark">
  <Header theme={theme} />
    <NavBar theme={theme} />
      <Button theme={theme} />
```

**Solution - useContext:**
```jsx
import { createContext, useContext, useState } from 'react';

// 1. Create context
const ThemeContext = createContext();

// 2. Provide context (at top level)
function App() {
  const [theme, setTheme] = useState('light');
  
  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      <Header />
      <Main />
      <Footer />
    </ThemeContext.Provider>
  );
}

// 3. Use context anywhere
function Button() {
  const { theme, setTheme } = useContext(ThemeContext);
  
  return (
    <button style={{ background: theme === 'dark' ? '#333' : '#fff' }}>
      Current theme: {theme}
    </button>
  );
}
```

**When to Use Context:**
- Global state (theme, language, auth)
- Avoid prop drilling
- Don't overuse for every state

**Performance Note:**
```jsx
// ❌ Creates new object on every render → unnecessary re-renders
<ThemeContext.Provider value={{ theme, setTheme }}>

// ✅ Memoize the value
const value = useMemo(() => ({ theme, setTheme }), [theme]);
<ThemeContext.Provider value={value}>
```

---

### **15. What is useRef Hook?**

**Answer:**
`useRef` gives **direct access to DOM elements** without causing re-renders.

**Common Use Cases:**

```jsx
// 1. Focus input
function TextInput() {
  const inputRef = useRef(null);
  
  return (
    <>
      <input ref={inputRef} type="text" />
      <button onClick={() => inputRef.current.focus()}>
        Focus Input
      </button>
    </>
  );
}

// 2. Store mutable value that persists across renders
function Timer() {
  const intervalRef = useRef(null);
  const [time, setTime] = useState(0);
  
  const startTimer = () => {
    intervalRef.current = setInterval(() => {
      setTime(t => t + 1);
    }, 1000);
  };
  
  const stopTimer = () => {
    clearInterval(intervalRef.current);
  };
  
  return <>...</>;
}

// 3. Access DOM properties
function VideoPlayer() {
  const videoRef = useRef(null);
  
  const handlePlay = () => videoRef.current.play();
  const handlePause = () => videoRef.current.pause();
  
  return (
    <>
      <video ref={videoRef} src="video.mp4" />
      <button onClick={handlePlay}>Play</button>
      <button onClick={handlePause}>Pause</button>
    </>
  );
}
```

**Key Differences from State:**

| useRef | useState |
|--------|----------|
| Returns same object always | New value on update |
| Doesn't cause re-render | Causes re-render |
| Mutable | Immutable (use setter) |
| `.current` property | Direct access |

**DON'T overuse useRef** - it breaks React's declarative nature.

---

### **16. What is useReducer Hook?**

**Answer:**
`useReducer` manages **complex state logic** with multiple actions.

```jsx
const [state, dispatch] = useReducer(reducer, initialState);
```

**Example - Todo App:**
```jsx
function TodoApp() {
  const [todos, dispatch] = useReducer(todoReducer, []);
  
  const addTodo = (text) => {
    dispatch({ type: 'ADD_TODO', payload: text });
  };
  
  const toggleTodo = (id) => {
    dispatch({ type: 'TOGGLE_TODO', payload: id });
  };
  
  const deleteTodo = (id) => {
    dispatch({ type: 'DELETE_TODO', payload: id });
  };
  
  return <>...</>;
}

function todoReducer(state, action) {
  switch(action.type) {
    case 'ADD_TODO':
      return [...state, { id: Date.now(), text: action.payload, done: false }];
    
    case 'TOGGLE_TODO':
      return state.map(todo =>
        todo.id === action.payload ? { ...todo, done: !todo.done } : todo
      );
    
    case 'DELETE_TODO':
      return state.filter(todo => todo.id !== action.payload);
    
    default:
      return state;
  }
}
```

**When to Use:**
- Multiple related state updates
- Complex state transitions
- Pass dispatch to child components (avoid prop drilling)

---

### **17. What are Rules of Hooks?**

**Answer:**
Hooks have strict rules (enforced by linter):

**Rule 1: Only call Hooks at top level**
```jsx
// ❌ Wrong: Inside condition
if (name) {
  const [age, setAge] = useState(0);
}

// ✅ Correct: At top level
const [age, setAge] = useState(0);
if (name) {
  // use age here
}
```

**Rule 2: Only call Hooks from React functions**
```jsx
// ❌ Wrong: In regular function
function regularFunction() {
  const [count, setCount] = useState(0); // ERROR
}

// ✅ Correct: In component or custom hook
function MyComponent() {
  const [count, setCount] = useState(0);
}

function useCustomHook() {
  const [count, setCount] = useState(0);
  return count;
}
```

**Rule 3: Don't call Hooks in loops, conditions, or nested functions**
```jsx
// ❌ Wrong
for (let i = 0; i < 5; i++) {
  const [count, setCount] = useState(0); // Don't call hooks in loop
}

// ✅ Correct
const [count1, setCount1] = useState(0);
const [count2, setCount2] = useState(0);
const [count3, setCount3] = useState(0);
```

**Reason:** React relies on call order of Hooks to maintain state correctly.

---

### **18. What are Custom Hooks?**

**Answer:**
Custom Hooks are **functions that use other hooks** and return values/functions for reuse.

**Example - useWindowWidth:**
```jsx
function useWindowWidth() {
  const [width, setWidth] = useState(window.innerWidth);
  
  useEffect(() => {
    const handleResize = () => setWidth(window.innerWidth);
    window.addEventListener('resize', handleResize);
    
    return () => window.removeEventListener('resize', handleResize);
  }, []);
  
  return width;
}

// Usage
function ResponsiveComponent() {
  const width = useWindowWidth();
  return <p>Window width: {width}px</p>;
}
```

**Example - useFetch:**
```jsx
function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);
  
  useEffect(() => {
    fetch(url)
      .then(res => res.json())
      .then(data => {
        setData(data);
        setLoading(false);
      })
      .catch(err => {
        setError(err);
        setLoading(false);
      });
  }, [url]);
  
  return { data, loading, error };
}

// Usage
function UserProfile({ userId }) {
  const { data: user, loading, error } = useFetch(`/api/users/${userId}`);
  
  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error.message}</p>;
  
  return <div>{user.name}</div>;
}
```

**Name Convention:** Always start with `use` prefix.

---

### **19. What is useMemo Hook?**

**Answer:**
`useMemo` **memoizes expensive calculations** and only recalculates when dependencies change.

```jsx
const memoizedValue = useMemo(() => {
  return expensiveCalculation(a, b);
}, [a, b]); // Only recalculates if a or b changes
```

**Example - Filtering Long List:**
```jsx
function ProductList({ products, filterText }) {
  // Without useMemo: filters on every render (slow!)
  // const filteredProducts = products.filter(p => p.name.includes(filterText));
  
  // With useMemo: filters only when products or filterText changes
  const filteredProducts = useMemo(() => {
    console.log('Filtering products...'); // Only logs when needed
    return products.filter(p => p.name.includes(filterText));
  }, [products, filterText]);
  
  return (
    <ul>
      {filteredProducts.map(p => <li key={p.id}>{p.name}</li>)}
    </ul>
  );
}
```

**When to Use:**
- Expensive calculations (sorting, filtering large lists)
- Creating objects/arrays passed as props
- Don't overuse - measurement first!

---

### **20. What is useCallback Hook?**

**Answer:**
`useCallback` **memoizes a function** so it doesn't get recreated on every render.

```jsx
const memoizedCallback = useCallback(() => {
  doSomething(a, b);
}, [a, b]); // Only recreates if a or b changes
```

**Example - Avoid Unnecessary Re-renders of Child:**
```jsx
function Parent() {
  const [count, setCount] = useState(0);
  
  // Without useCallback: handleClick recreated every render
  // const handleClick = () => console.log('clicked');
  
  // With useCallback: same function reference if dependencies unchanged
  const handleClick = useCallback(() => {
    console.log('clicked');
  }, []); // No dependencies = same function always
  
  return <Child onClick={handleClick} />;
}

// Child only re-renders if onClick prop changes (same reference)
function Child({ onClick }) {
  console.log('Child rendered');
  return <button onClick={onClick}>Click me</button>;
}
```

**Comparison: useMemo vs useCallback**

```jsx
// useMemo: Memoizes value
const value = useMemo(() => computeValue(), [deps]);

// useCallback: Memoizes function (actually calls useMemo internally!)
const func = useCallback(() => { doSomething(); }, [deps]);

// These are equivalent:
const func1 = useCallback(() => doSomething(), [deps]);
const func2 = useMemo(() => () => doSomething(), [deps]);
```

---

## **REACT LIFECYCLE & CLASS COMPONENTS (8 Questions)**

### **21. What are React Lifecycle Methods?**

**Answer:**
Lifecycle methods are called at different stages of a component's existence: Mounting, Updating, Unmounting.

**Mounting Phase (Component created & inserted to DOM):**
```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    // Initialize state
  }
  
  componentDidMount() {
    // Called after component renders
    // Good for: API calls, subscriptions
  }
  
  render() {
    return <div>...</div>;
  }
}
```

**Updating Phase (Props or state change):**
```jsx
shouldComponentUpdate(nextProps, nextState) {
  // Return false to skip re-render (optimization)
  return true;
}

componentDidUpdate(prevProps, prevState) {
  // Called after component updates
  // Good for: side effects based on props/state change
  if (this.props.id !== prevProps.id) {
    this.fetchData();
  }
}
```

**Unmounting Phase (Component removed from DOM):**
```jsx
componentWillUnmount() {
  // Called before component is destroyed
  // Good for: cleanup (remove listeners, cancel requests)
  clearInterval(this.timerID);
}
```

**Rare/Deprecated Methods:**
- `getDerivedStateFromProps` (rarely used)
- `getSnapshotBeforeUpdate` (rarely used)
- ~~`componentWillMount`~~ (deprecated)
- ~~`componentWillReceiveProps`~~ (deprecated)

**Modern Approach - Use Hooks instead:**
```jsx
// componentDidMount equivalent
useEffect(() => {
  // ...
}, []);

// componentDidUpdate equivalent
useEffect(() => {
  // ...
}, [dependency]);

// componentWillUnmount equivalent
useEffect(() => {
  return () => {
    // cleanup
  };
}, []);
```

---

### **22. What is shouldComponentUpdate and when to use it?**

**Answer:**
`shouldComponentUpdate` is **optimization method that prevents unnecessary re-renders**.

```jsx
shouldComponentUpdate(nextProps, nextState) {
  // Return true to re-render, false to skip
  return true;
}
```

**Example:**
```jsx
class ExpensiveComponent extends React.Component {
  shouldComponentUpdate(nextProps, nextState) {
    // Only re-render if id changes
    return this.props.id !== nextProps.id;
  }
  
  render() {
    return <div>ID: {this.props.id}</div>;
  }
}
```

**Modern Alternative - React.memo (for functional components):**
```jsx
const MyComponent = React.memo(({ id }) => {
  return <div>ID: {id}</div>;
});

// Or with custom comparison
const MyComponent = React.memo(
  ({ id, name }) => <div>{id}: {name}</div>,
  (prevProps, nextProps) => {
    // Return true if props are equal (don't re-render)
    return prevProps.id === nextProps.id;
  }
);
```

---

## **FORM HANDLING & VALIDATION (5 Questions)**

### **23. What are Controlled Components?**

**Answer:**
Controlled components have React control their value through state.

```jsx
function Form() {
  const [name, setName] = useState('');
  const [email, setEmail] = useState('');
  
  const handleSubmit = (e) => {
    e.preventDefault();
    console.log({ name, email });
  };
  
  return (
    <form onSubmit={handleSubmit}>
      <input
        value={name}
        onChange={(e) => setName(e.target.value)}
        placeholder="Name"
      />
      
      <input
        value={email}
        onChange={(e) => setEmail(e.target.value)}
        type="email"
        placeholder="Email"
      />
      
      <button type="submit">Submit</button>
    </form>
  );
}
```

**Advantages:**
- Single source of truth (state)
- Real-time validation
- Can manipulate input value programmatically
- Easier to test

---

### **24. What are Uncontrolled Components?**

**Answer:**
Uncontrolled components manage their own state using the DOM.

```jsx
function Form() {
  const nameRef = useRef(null);
  const emailRef = useRef(null);
  
  const handleSubmit = (e) => {
    e.preventDefault();
    console.log({
      name: nameRef.current.value,
      email: emailRef.current.value
    });
  };
  
  return (
    <form onSubmit={handleSubmit}>
      <input ref={nameRef} placeholder="Name" defaultValue="John" />
      <input ref={emailRef} type="email" placeholder="Email" defaultValue="john@example.com" />
      <button type="submit">Submit</button>
    </form>
  );
}
```

**When to Use Uncontrolled:**
- Simple forms
- File inputs
- Integrating with non-React code

**Controlled vs Uncontrolled:**

| Controlled | Uncontrolled |
|-----------|-------------|
| Value from state | Value from DOM |
| Real-time validation | Validation on submit |
| More code | Less code |
| Easier testing | Harder testing |
| Recommended | Avoid if possible |

---

## **STATE MANAGEMENT & PERFORMANCE (8 Questions)**

### **25. What is prop drilling and how to solve it?**

**Answer:**
Prop drilling is passing props through multiple levels of components to reach deeply nested child.

**Problem:**
```jsx
// App.js
<Parent user={user} />

// Parent.js
<Child user={user} />

// Child.js
<GrandChild user={user} />

// GrandChild.js
<GreatGrandChild user={user} />

// GreatGrandChild.js - finally uses user
function GreatGrandChild({ user }) {
  return <p>{user.name}</p>;
}
```

**Solutions:**

1. **Context API:**
```jsx
const UserContext = createContext();

function App() {
  const [user, setUser] = useState({ name: 'Alice' });
  
  return (
    <UserContext.Provider value={user}>
      <Parent /> {/* No need to pass user prop! */}
    </UserContext.Provider>
  );
}

// GrandChild
function GrandChild() {
  const user = useContext(UserContext);
  return <p>{user.name}</p>;
}
```

2. **State Management Library (Redux):**
```jsx
import { useSelector } from 'react-redux';

function GrandChild() {
  const user = useSelector(state => state.user);
  return <p>{user.name}</p>;
}
```

3. **Component Composition:**
```jsx
// Pass component instead of prop
<Parent render={<GreatGrandChild />} />
```

---

### **26. What is React.memo and when to use it?**

**Answer:**
`React.memo` **memoizes a component** to prevent unnecessary re-renders when props haven't changed.

```jsx
const MyComponent = React.memo(({ name }) => {
  console.log('Component rendered');
  return <div>Hello, {name}</div>;
});

// Only re-renders if 'name' prop changes
```

**Example:**
```jsx
function Parent() {
  const [count, setCount] = useState(0);
  const [name, setName] = useState('Alice');
  
  return (
    <div>
      <button onClick={() => setCount(count + 1)}>Count: {count}</button>
      
      {/* ChildWithMemo only re-renders if 'name' changes */}
      <ChildWithMemo name={name} />
      
      {/* RegularChild re-renders every time Parent re-renders */}
      <RegularChild name={name} />
    </div>
  );
}

const ChildWithMemo = React.memo(({ name }) => {
  console.log('ChildWithMemo rendered');
  return <p>{name}</p>;
});

function RegularChild({ name }) {
  console.log('RegularChild rendered');
  return <p>{name}</p>;
}
```

**When to Use:**
- Pure components (same props = same output)
- Prevent unnecessary re-renders
- Don't overuse - measure performance first!

**Performance Warning:**
```jsx
// ❌ Creating new object every render defeats memoization
<Child user={{ name: 'Alice' }} />

// ✅ Memoize the value
const user = useMemo(() => ({ name: 'Alice' }), []);
<Child user={user} />
```

---

### **27. What is lazy loading and code splitting in React?**

**Answer:**
Lazy loading loads components only when needed to improve initial load time.

```jsx
import { lazy, Suspense } from 'react';

// Lazy load component
const HeavyComponent = lazy(() => import('./HeavyComponent'));

function App() {
  const [showHeavy, setShowHeavy] = useState(false);
  
  return (
    <div>
      <button onClick={() => setShowHeavy(true)}>Load Component</button>
      
      {/* Suspend rendering until HeavyComponent loads */}
      <Suspense fallback={<p>Loading...</p>}>
        {showHeavy && <HeavyComponent />}
      </Suspense>
    </div>
  );
}
```

**Route-based Code Splitting:**
```jsx
import { lazy, Suspense } from 'react';
import { BrowserRouter, Routes, Route } from 'react-router-dom';

const Home = lazy(() => import('./pages/Home'));
const About = lazy(() => import('./pages/About'));
const Contact = lazy(() => import('./pages/Contact'));

function App() {
  return (
    <BrowserRouter>
      <Suspense fallback={<p>Loading...</p>}>
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/about" element={<About />} />
          <Route path="/contact" element={<Contact />} />
        </Routes>
      </Suspense>
    </BrowserRouter>
  );
}
```

**Benefits:**
- Smaller initial bundle
- Faster initial load
- Better performance on slow networks

---

## **ADVANCED TOPICS (8 Questions)**

### **28. What are Higher-Order Components (HOC)?**

**Answer:**
HOC is a **pattern where a function takes a component and returns a new enhanced component**.

```jsx
function withTheme(Component) {
  return function WithThemeComponent(props) {
    const [theme, setTheme] = useState('light');
    
    return <Component {...props} theme={theme} setTheme={setTheme} />;
  };
}

// Usage
function MyButton({ theme, setTheme }) {
  return (
    <button style={{ background: theme === 'dark' ? '#333' : '#fff' }}>
      {theme}
    </button>
  );
}

const EnhancedButton = withTheme(MyButton);
```

**Another Example - withAuth (for private routes):**
```jsx
function withAuth(Component) {
  return function WithAuthComponent(props) {
    const [isAuth, setIsAuth] = useState(false);
    
    if (!isAuth) {
      return <div>Please log in</div>;
    }
    
    return <Component {...props} isAuth={isAuth} />;
  };
}
```

**Naming Convention:** `withFeatureName`

**Modern Alternative - Custom Hooks:**
```jsx
// Instead of HOC, use custom hook
function useTheme() {
  const [theme, setTheme] = useState('light');
  return { theme, setTheme };
}

function MyButton() {
  const { theme, setTheme } = useTheme();
  return <button>...</button>;
}
```

---

### **29. What are Error Boundaries?**

**Answer:**
Error Boundaries **catch JavaScript errors anywhere in child component tree**.

```jsx
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false, error: null };
  }
  
  static getDerivedStateFromError(error) {
    return { hasError: true, error };
  }
  
  componentDidCatch(error, errorInfo) {
    console.log('Error caught:', error);
    console.log(errorInfo);
    // Can send to error tracking service
  }
  
  render() {
    if (this.state.hasError) {
      return <h1>Something went wrong: {this.state.error.message}</h1>;
    }
    
    return this.props.children;
  }
}

// Usage
function App() {
  return (
    <ErrorBoundary>
      <MyComponent />
    </ErrorBoundary>
  );
}
```

**Error Boundaries DON'T catch:**
- Event handler errors (use try-catch)
- Async errors (use .catch())
- Server-side rendering
- Errors in the boundary itself

---

### **30. What is Server-Side Rendering (SSR)?**

**Answer:**
SSR **renders React components on the server** and sends HTML to browser (vs client-side rendering).

**Client-Side Rendering (CSR - Traditional React):**
```
Browser requests → Gets empty HTML + JS
→ Browser loads JS
→ React renders component
→ Page becomes interactive
```

**Server-Side Rendering (SSR):**
```
Browser requests → Server renders React
→ Server sends complete HTML
→ Browser displays HTML immediately (faster!)
→ Hydration: React takes over interactivity
```

**Example with Next.js (SSR framework):**
```jsx
// pages/index.js (automatically server-rendered)
export default function Home() {
  return <h1>Hello from SSR</h1>;
}

// This is rendered on server, sent as HTML to browser
```

**Benefits:**
- Better SEO (search engines see complete HTML)
- Faster initial page load
- Works without JavaScript

**Drawbacks:**
- More complex setup
- Server load
- Synchronous data fetching

---

### **31. What is Hydration?**

**Answer:**
Hydration is **attaching event listeners and state to server-rendered HTML**.

**Process:**
```
1. Server renders React to HTML
2. Browser receives HTML (fast display)
3. Browser loads JavaScript
4. React "hydrates" - attaches listeners, recreates state
5. Page becomes interactive
```

**Example:**
```jsx
// On server
ReactDOMServer.renderToString(<App />);
// Returns: <div>Hello <button>0</button></div>

// On browser
ReactDOM.hydrateRoot(document.getElementById('root'), <App />);
// Attaches click listeners, state, etc. to existing HTML
```

**Common Error:**
```
Uncaught Error: Hydration mismatch! Server rendered:
<div>1</div> but Client rendered: <div>2</div>
```

**Causes:**
- Date/time rendering (shows different value on server vs client)
- Random IDs
- Unsafe browser APIs used during render

---

## **PERFORMANCE OPTIMIZATION (5 Questions)**

### **32. How to optimize React application performance?**

**Answer:**
Key optimization techniques:

**1. Code Splitting & Lazy Loading:**
```jsx
const Component = lazy(() => import('./Component'));
```

**2. Memoization (useMemo, useCallback, React.memo):**
```jsx
const memoized = useMemo(() => expensiveCalc(), [deps]);
const callback = useCallback(() => doSomething(), [deps]);
const Memoized = React.memo(Component);
```

**3. Virtual List (for long lists):**
```jsx
// Instead of rendering 10,000 items, render only visible ones
import { FixedSizeList } from 'react-window';

<FixedSizeList height={600} itemCount={1000} itemSize={35}>
  {Row}
</FixedSizeList>
```

**4. Image Optimization:**
```jsx
// Lazy load images
<img loading="lazy" src="image.jpg" />

// Or use WebP format
<picture>
  <source srcSet="image.webp" type="image/webp" />
  <img src="image.jpg" />
</picture>
```

**5. Bundle Size Reduction:**
- Use production build: `npm run build`
- Analyze bundle: `npm install -g webpack-bundle-analyzer`
- Remove unused dependencies
- Use dynamic imports

**6. Avoid State in Wrong Place:**
```jsx
// ❌ Count is in top level, causes all children to re-render
function Parent() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <ExpensiveChild />
      <button onClick={() => setCount(count + 1)}>Count</button>
    </div>
  );
}

// ✅ Move state to component that needs it
function Parent() {
  return (
    <div>
      <ExpensiveChild />
      <Counter />
    </div>
  );
}

function Counter() {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(count + 1)}>Count</button>;
}
```

---

### **33. What is React Profiler?**

**Answer:**
React Profiler is a tool to **measure component render performance**.

**Using React DevTools Profiler:**
1. Install React DevTools browser extension
2. Open DevTools → Profiler tab
3. Start recording
4. Interact with app
5. View render times and causes

**Programmatic API:**
```jsx
import { Profiler } from 'react';

function onRenderCallback(
  id, // Component name
  phase, // 'mount' or 'update'
  actualDuration, // Time to render
  baseDuration,
  startTime,
  commitTime
) {
  console.log(`${id} (${phase}) took ${actualDuration}ms`);
}

function App() {
  return (
    <Profiler id="App" onRender={onRenderCallback}>
      <MyComponent />
    </Profiler>
  );
}
```

---

## **TESTING (3 Questions)**

### **34. How to test React components?**

**Answer:**
Common testing tools:

**1. Jest (Test Runner):**
```jsx
import { render, screen } from '@testing-library/react';
import Button from './Button';

test('renders button with correct text', () => {
  render(<Button label="Click me" />);
  const button = screen.getByRole('button', { name: /click me/i });
  expect(button).toBeInTheDocument();
});
```

**2. React Testing Library (Components):**
```jsx
import { render, screen, fireEvent } from '@testing-library/react';

test('increments count when clicked', () => {
  render(<Counter />);
  const button = screen.getByRole('button', { name: /increment/i });
  fireEvent.click(button);
  expect(screen.getByText(/count: 1/i)).toBeInTheDocument();
});
```

**3. Enzyme (Older alternative):**
```jsx
import { shallow } from 'enzyme';

test('renders without crashing', () => {
  const wrapper = shallow(<Component />);
  expect(wrapper).toHaveLength(1);
});
```

**Best Practices:**
- Test user behavior, not implementation
- Use `screen` instead of `wrapper.find()`
- Avoid testing internal state

---

## **PRACTICE PROJECTS (3 Real-World Projects)**

### **Project 1: Todo App with Local Storage**

**Features:**
- Add, edit, delete todos
- Mark as complete
- Filter (All, Active, Completed)
- Persist to localStorage

**Key Concepts:**
- useState for state management
- useEffect for localStorage
- Event handling
- Conditional rendering

---

### **Project 2: Weather App with API Integration**

**Features:**
- Search by city
- Display current weather
- 5-day forecast
- Show temperature, humidity, wind

**Key Concepts:**
- useEffect for API calls
- Handling loading/error states
- Async/await
- Error boundaries
- Custom hooks

---

### **Project 3: E-commerce Product Listing**

**Features:**
- Product grid
- Filter by category, price
- Sort (price, popularity)
- Shopping cart
- Checkout

**Key Concepts:**
- Context for global cart state
- useReducer for complex state
- Lazy loading for images
- Performance optimization
- Responsive design

---

## **FINAL INTERVIEW TIPS**

✅ **DO:**
- Think aloud - explain your reasoning
- Ask clarifying questions
- Start with simple solution, optimize if asked
- Use proper naming conventions
- Handle edge cases
- Write clean, readable code

❌ **DON'T:**
- Memorize answers - understand concepts
- Write code without thinking
- Skip error handling
- Use deprecated patterns
- Overuse Context/Redux for everything
- Forget to clean up effects

---

**Total: 50+ Questions**
**Study Time: 2-3 weeks**
**Practice Projects: 3 full-stack apps**

Good luck with your React interviews! 🚀
