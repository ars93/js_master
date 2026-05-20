# 4.1 Components & JSX

## Functional Components

```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}!</h1>;
}

const name = "John";
const element = <Welcome name={name} />;
```

## JSX Syntax

```javascript
const element = (
  <div className="container">
    <h1>Welcome</h1>
    <p>This is JSX</p>
    <img src="image.jpg" alt="description" />
  </div>
);
```

## Props

```javascript
function User({ name, age, email }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>Age: {age}</p>
      <p>Email: {email}</p>
    </div>
  );
}

export default User;
```

## Component Composition

```javascript
function App() {
  const users = [
    { id: 1, name: "John", age: 25 },
    { id: 2, name: "Jane", age: 30 }
  ];
  
  return (
    <div>
      {users.map(user => (
        <User key={user.id} name={user.name} age={user.age} />
      ))}
    </div>
  );
}
```

---

**Next:** [02-hooks.md](./02-hooks.md)