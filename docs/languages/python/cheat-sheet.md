# Python Cheat Sheet

## Setup

```bash
python3 --version
python3 -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install requests
pip install -r requirements.txt
pip freeze > requirements.txt
python3 script.py
python3 -m http.server 8000        # quick file server
```

## Data types

| Type | Example | Mutable |
|---|---|---|
| `int`, `float` | `1`, `3.14` | No |
| `str` | `"hi"` | No |
| `bool` | `True`, `False` | No |
| `None` | `None` | — |
| `list` | `[1, 2]` | Yes |
| `tuple` | `(1, 2)` | No |
| `dict` | `{"a": 1}` | Yes |
| `set` | `{1, 2}` | Yes |

## Syntax

```python
name = "Ashoka"
print(f"Hi {name}, {2 + 3}")

if x > 0:
    ...
elif x == 0:
    ...
else:
    ...

for i in range(5): ...
for i, v in enumerate(items): ...
for k, v in d.items(): ...
while cond: ...

squares = [x * x for x in range(10) if x % 2 == 0]
lookup = {k: v for k, v in pairs}
```

## Strings + lists + dicts

```python
s.strip(); s.split(","); ",".join(lst); s.replace("a", "b"); s.lower()
s[0]; s[-1]; s[1:4]; s[::-1]

lst.append(x); lst.extend([1, 2]); lst.pop(); lst.sort(); sorted(lst, key=len)
len(lst); sum(lst); min(lst); max(lst)

d.get("k", default); d.keys(); d.values(); d.items(); d.pop("k")
```

## Functions

```python
def add(a: int, b: int = 0) -> int:
    return a + b

def f(*args, **kwargs): ...
square = lambda x: x * x
```

## Classes

```python
from dataclasses import dataclass

class Animal:
    def __init__(self, name: str):
        self.name = name
    def speak(self) -> str:
        return "..."

class Dog(Animal):
    def speak(self) -> str:
        return "Woof"

@dataclass
class User:
    id: int
    name: str
```

## Errors + files

```python
try:
    risky()
except ValueError as e:
    print(e)
finally:
    cleanup()

raise ValueError("bad input")

with open("f.txt") as f:
    text = f.read()
with open("f.txt", "w") as f:
    f.write("hi")
```

## Modules

```python
import json, os
from pathlib import Path
json.loads(s); json.dumps(obj, indent=2)
os.environ.get("KEY")
Path("dir").mkdir(parents=True, exist_ok=True)

if __name__ == "__main__":
    main()
```

## Useful stdlib

| Module | Use |
|---|---|
| `pathlib` | Paths, files |
| `json` | JSON |
| `datetime` | Dates |
| `collections` | `Counter`, `defaultdict`, `deque` |
| `itertools` | Iteration helpers |
| `logging` | Logs |
| `subprocess` | Run shell commands |
| `asyncio` | Async I/O |
| `re` | Regex |
