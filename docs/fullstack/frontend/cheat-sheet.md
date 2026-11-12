# Frontend Cheat Sheet

## HTML skeleton

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Page</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <script src="app.js" defer></script>
</body>
</html>
```

Semantic tags: `header` `nav` `main` `section` `article` `aside` `footer`.

## CSS selectors

| Selector | Matches |
|---|---|
| `p` | Tag |
| `.card` | Class |
| `#app` | Id |
| `div p` | Descendant |
| `div > p` | Direct child |
| `a:hover` | State |
| `li:nth-child(2)` | Position |
| `[type="text"]` | Attribute |

## CSS layout

```css
.row  { display: flex; justify-content: space-between; align-items: center; gap: 1rem; }
.grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 1rem; }
.box  { box-sizing: border-box; margin: 0 auto; padding: 1rem; max-width: 960px; }
@media (max-width: 600px) { .grid { grid-template-columns: 1fr; } }
```

Units: `px` fixed · `rem` root font · `%` parent · `vw/vh` viewport.

## JavaScript essentials

```javascript
const x = 1; let y = 2;                       // no var
const add = (a, b) => a + b;
const { name, age } = user;                   // destructure
const copy = { ...user, age: 30 };            // spread
const s = `Hi ${name}`;                       // template string

arr.map(x => x * 2);
arr.filter(x => x > 1);
arr.reduce((sum, x) => sum + x, 0);
arr.find(x => x.id === 1);

document.querySelector('#app');
el.addEventListener('click', e => {});

const res = await fetch('/api/users');
const data = await res.json();
```

## npm

```bash
npm init -y
npm install pkg            # npm i pkg
npm install -D pkg         # dev dependency
npm uninstall pkg
npm run dev                # script from package.json
npm ci                     # clean install from lockfile
npx pkg                    # run without installing
npm create vite@latest my-app -- --template react
```

## Ecosystem

| Need | Options |
|---|---|
| Framework | React, Vue, Angular, Svelte |
| Meta-framework | Next.js, Nuxt |
| Build tool | Vite |
| Styling | Tailwind CSS, CSS Modules |
| Types | TypeScript |
