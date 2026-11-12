# JavaScript Cheat Sheet

## Run

```bash
node --version
node app.js
node                                # REPL
npm init -y
npm install pkg
```

## Variables + types

```javascript
const a = 1;          // cannot reassign
let b = 2;            // block scoped
// avoid var

typeof x              // "number" "string" "boolean" "object" "undefined" "function"
x === y               // strict equal, always prefer over ==
x ?? "default"        // null/undefined fallback
obj?.user?.name       // optional chaining
```

## Functions

```javascript
function add(a, b = 0) { return a + b; }
const add2 = (a, b) => a + b;
const sum = (...nums) => nums.reduce((s, n) => s + n, 0);
```

## Arrays

```javascript
arr.push(x); arr.pop(); arr.shift(); arr.unshift(x)
arr.map(x => x * 2)
arr.filter(x => x > 1)
arr.reduce((acc, x) => acc + x, 0)
arr.find(x => x.id === 1)
arr.some(x => x > 1); arr.every(x => x > 0)
arr.includes(3)
arr.slice(1, 3)                 // copy part
arr.toSorted((a, b) => a - b)   // sorted copy
[...a, ...b]                    // merge
```

## Objects

```javascript
const user = { name: "a", age: 20 };
const { name, ...rest } = user;
const copy = { ...user, age: 21 };
Object.keys(user); Object.values(user); Object.entries(user)
JSON.stringify(user); JSON.parse(str)
```

## Classes

```javascript
class Animal {
  #secret = 1;                     // private field
  constructor(name) { this.name = name; }
  speak() { return "..."; }
}
class Dog extends Animal {
  speak() { return "Woof"; }
}
```

## Async

```javascript
const res = await fetch("/api/users");
if (!res.ok) throw new Error(res.status);
const data = await res.json();

try { await work(); } catch (e) { console.error(e); }

await Promise.all([p1, p2]);       // parallel, fail fast
await Promise.allSettled([p1, p2]);
setTimeout(() => {}, 1000);
```

## Modules (ESM)

```javascript
// math.js
export const add = (a, b) => a + b;
export default function main() {}

// app.js
import main, { add } from "./math.js";
```

Node ESM: `"type": "module"` in `package.json`.

## Truthy / falsy

Falsy: `false` `0` `""` `null` `undefined` `NaN`. Everything else truthy (incl. `[]`, `{}`).
