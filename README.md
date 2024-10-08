
---

## Part 13: Form Handling

### `useRef`
- `useRef` is used to directly access a DOM element in a React component.

**Example:**

```javascript
import React, { useRef } from 'react';

function MyComponent() {
  const inputRef = useRef();

  const focusInput = () => {
    inputRef.current.focus();
  };

  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={focusInput}>Focus Input</button>
    </div>
  );
}
```

### Controlled Components
- Controlled components use `useState` to manage form data and handle changes through `onChange` events.

**Example:**

```javascript
import React, { useState } from 'react';

function FormComponent() {
  const [name, setName] = useState('');

  const handleChange = (e) => {
    setName(e.target.value);
  };

  return (
    <form>
      <input type="text" value={name} onChange={handleChange} />
      <p>{name}</p>
    </form>
  );
}
```

### Using React Hook Form
- React Hook Form simplifies form handling with easy validation and submission.

**Example:**

```javascript
import React from 'react';
import { useForm } from 'react-hook-form';

function HookFormComponent() {
  const { register, handleSubmit } = useForm();
  const onSubmit = (data) => console.log(data);

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register('firstName')} placeholder="First Name" />
      <input {...register('lastName')} placeholder="Last Name" />
      <button type="submit">Submit</button>
    </form>
  );
}
```

---

## Practice 14: Sending Data from Child to Parent
- This practice helps to improve logic and understand how to send data from child components to parent components via functions.

### Example
- You can pass a function as a prop from the parent to the child, which the child can then call to send data back to the parent.

**Example:**

```javascript
import React, { useState } from 'react';

function ParentComponent() {
  const [data, setData] = useState('');

  const handleData = (childData) => {
    setData(childData);
  };

  return (
    <div>
      <ChildComponent onSendData={handleData} />
      <p>Data from Child: {data}</p>
    </div>
  );
}

function ChildComponent({ onSendData }) {
  const sendDataToParent = () => {
    onSendData('Hello Parent!');
  };

  return <button onClick={sendDataToParent}>Send Data</button>;
}
```

---

## Part 15: Routing in React

### Using React Router
- React Router is implemented with `react-router-dom`.
- Wrap the main component with `BrowserRouter`, imported from `react-router-dom`.
- Routing is implemented using `Routes` and `Route` tags.

**Example:**

```javascript
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import Home from './Home';
import About from './About';

function App() {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </Router>
  );
}
```

### Adding Links in Navigation
- Use `Link` instead of anchor tags for navigation.
- `NavLink` can be used for toggling active states.

**Example:**

```javascript
import { NavLink } from 'react-router-dom';

function Navbar() {
  return (
    <nav>
      <NavLink to="/" style={({ isActive }) => ({ color: isActive ? 'red' : 'blue' })}>Home</NavLink>
      <NavLink to="/about" className={({ isActive }) => isActive ? 'active' : ''}>About</NavLink>
    </nav>
  );
}
```

---

## Part 16: Dynamic Routing

### Dynamic Routing
- Dynamic routing is achieved by specifying a path with a parameter, such as `/user/:id`.
- Access the parameter in the component using `useParams()`.

**Example:**

```javascript
import { useParams } from 'react-router-dom';

function UserDetails() {
  const { id } = useParams();
  return <h2>User ID: {id}</h2>;
}
```

### Child Routing
- Child routing involves nesting routes. The `Outlet` component is used to render the child components.

**Example:**

```javascript
import { Routes, Route, Outlet } from 'react-router-dom';

function User() {
  return (
    <div>
      <h2>User Component</h2>
      <Outlet />
    </div>
  );
}

function UserDetails() {
  return <h2>User Details</h2>;
}

function App() {
  return (
    <Routes>
      <Route path="/users" element={<User />}>
        <Route path=":name" element={<UserDetails />} />
      </Route>
    </Routes>
  );
}
```

### Navigating Back
- Use `useNavigate` to navigate back or to a specific route.

**Example:**

```javascript
import { useNavigate } from 'react-router-dom';

function BackButton() {
  let navigate = useNavigate();

  const goBackHandler = () => {
    navigate(-1); // Move backward by 1 step
  };

  return <button onClick={goBackHandler}>Go Back</button>;
}
```

#
