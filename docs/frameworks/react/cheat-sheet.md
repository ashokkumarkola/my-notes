# React Cheat Sheet

## Setup

```bash
npm create vite@latest my-app -- --template react      # or react-ts
cd my-app
npm install
npm run dev
npm run build
```

## Component + props

```jsx
function Greeting({ name, children }) {
  return <h1>Hello {name} {children}</h1>;
}

<Greeting name="Ashoka">!</Greeting>
```

JSX rules: one root (or `<>...</>`), `className` not `class`, `{}` for JS.

## State

```jsx
import { useState } from "react";

const [count, setCount] = useState(0);
setCount(c => c + 1);                       // update from previous
setUser(u => ({ ...u, name: "b" }));        // never mutate
```

## Effects

```jsx
import { useEffect } from "react";

useEffect(() => {
  const id = setInterval(tick, 1000);
  return () => clearInterval(id);           // cleanup
}, []);                                     // [] = run once on mount
```

| Deps | Runs |
|---|---|
| none | Every render |
| `[]` | Once on mount |
| `[a, b]` | When `a` or `b` change |

## Hooks

| Hook | Use |
|---|---|
| `useState` | Local state |
| `useEffect` | Side effects: fetch, timers, subscriptions |
| `useRef` | DOM ref, mutable value without re-render |
| `useMemo` | Cache computed value |
| `useCallback` | Cache function |
| `useContext` | Read shared context |
| `useReducer` | Complex state logic |

## Lists + conditions

```jsx
{items.map(item => <li key={item.id}>{item.name}</li>)}   // key required, stable
{isLoading && <Spinner />}
{user ? <Profile /> : <Login />}
```

## Events + forms

```jsx
<button onClick={() => setOpen(true)}>Open</button>

const [email, setEmail] = useState("");
<form onSubmit={e => { e.preventDefault(); save(email); }}>
  <input value={email} onChange={e => setEmail(e.target.value)} />
</form>
```

## Fetch data

```jsx
useEffect(() => {
  let ignore = false;
  fetch("/api/users").then(r => r.json()).then(d => { if (!ignore) setUsers(d); });
  return () => { ignore = true; };
}, []);
```

Real apps: TanStack Query for server state.

## Ecosystem

| Need | Option |
|---|---|
| Routing | React Router |
| Server state | TanStack Query |
| Global state | Context, Zustand, Redux Toolkit |
| Forms | React Hook Form + Zod |
| Styling | Tailwind CSS |
| Full-stack | Next.js |
