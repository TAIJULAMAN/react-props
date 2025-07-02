# Passing Props to a Component

**Props (short for “properties”)** are inputs passed from one component (usually a parent) to another (usually a child).

They are used to make components **dynamic, reusable, and customizable**.

```jsx
function App() {
  return <Person name="aman" age={29} />;
}

function Person(props) {
  return <h1>Hello, {props.name}! You are {props.age} years old.</h1>;
}
```

### Destructuring Props

```jsx
function Person({ name, age }) {
  return <h1>Hello, {name}! You are {age} years old.</h1>;
}
```

## Types of Props

```jsx
<Component
  text="Hello"
  number={42}
  isLoggedIn={true}
  user={{ name: "aman" }}
  list={["JS", "React"]}
  onClick={() => alert("Clicked!")}
/>

```

Props are read only, You **cannot** mutate props inside a component.To change values, use **state** or **context** instead.:

```jsx
function Example({ count }) {
  // ❌ count = 10; // Not allowed
}
```

## children – Passing Nested Content

```jsx
function Card({ children }) {
  return <div className="card">{children}</div>;
}

<Card>
  <h2>Hello</h2>
  <p>This is inside the card</p>
</Card>

```

## Default Value

```jsx
function Button({ label = "Click Me" }) {
  return <button>{label}</button>;
}
```

## Spread Operator in Props

```jsx
const user = { name: "Shah", age: 25 };

<Profile {...user} />
```

### Overriding Spread Props

```jsx
const user = { name: "Shah", age: 25 };
<Profile {...user} age={30} />  // age will be 30
```

### Example:

```jsx
const buttonProps = {
  type: "submit",
  className: "btn",
  disabled: false,
};
<Button {...buttonProps} onClick={handleClick}>Save</Button>
```

## Summary Table

## Prop Validation with `PropTypes`

**`PropTypes`** is a utility for validating props passed to a component.

```bash
npm install prop-types
```

### Example:

```jsx
import PropTypes from "prop-types";

function UserCard({ name, age, isAdmin }) {
  return (
    <div>
      <h2>{name} ({age})</h2>
      <p>{isAdmin ? "Admin" : "User"}</p>
    </div>
  );
}

UserCard.propTypes = {
  name: PropTypes.string.isRequired,
  age: PropTypes.number.isRequired,
  isAdmin: PropTypes.bool,
};

```

---

### Common Properties Type

| Type | Validator |
| --- | --- |
| string | `PropTypes.string` |
| number | `PropTypes.number` |
| bool | `PropTypes.bool` |
| array | `PropTypes.array` |
| object | `PropTypes.object` |
| func | `PropTypes.func` |
| node (any renderable content) | `PropTypes.node` |
| element (React element only) | `PropTypes.element` |
| one of options | `PropTypes.oneOf(['A', 'B'])` |
| custom shape | `PropTypes.shape({ ... })` |

## Conditional Rendering with Props

Conditional rendering means showing different UI based on a prop value.

### Boolean Prop

```jsx
function Banner({ show }) {
  return show ? <div className="banner">Welcome!</div> : null;
}
```

### Role-Based Rendering

```jsx
function Dashboard({ role }) {
  return (
    <>
      {role === "admin" && <AdminPanel />}
      {role === "user" && <UserHome />}
    </>
  );
}
```

### Loading State

```jsx
function Button({ isLoading, children }) {
  return (
    <button disabled={isLoading}>
      {isLoading ? "Loading..." : children}
    </button>
  );
}
```

## Forwarding Props with `React.forwardRef`

`forwardRef` allows a parent component to pass a `ref` directly to a child DOM element or component.

```jsx
import React, { forwardRef } from "react";

const CustomInput = forwardRef((props, ref) => {
  return <input ref={ref} {...props} />;
});

function App() {
  const inputRef = React.useRef();

  const focusInput = () => {
    inputRef.current?.focus();
  };

  return (
    <>
      <CustomInput ref={inputRef} placeholder="Type here" />
      <button onClick={focusInput}>Focus Input</button>
    </>
  );
}
```

### Use of `forwardRef` :

- Creating custom form components
- Integrating with 3rd party libraries
- Reusable components where parent needs control (e.g. modals, tooltips)

# Summary Table

| Concept | Description |
| --- | --- |
| Props | Data passed from parent to child |
| Read-only | Cannot be changed inside the child |
| Destructuring | Clean syntax to extract props |
| Spread `...` | Pass object as multiple props |
| `props.children` | Nest content inside a component |
| Filtering | Remove unwanted props before spreading |