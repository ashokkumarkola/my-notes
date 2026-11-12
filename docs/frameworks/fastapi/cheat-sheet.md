# FastAPI Cheat Sheet

## Setup + run

```bash
pip install "fastapi[standard]"
fastapi dev main.py                     # dev, auto-reload
fastapi run main.py                     # production
uvicorn main:app --reload --port 8000   # alternative
```

Auto docs: `/docs` (Swagger UI) · `/redoc` · `/openapi.json`.

## App + routes

```python
from fastapi import FastAPI

app = FastAPI(title="My API")

@app.get("/")
def root():
    return {"status": "ok"}
```

Decorators: `@app.get` `@app.post` `@app.put` `@app.patch` `@app.delete`.

## Params

```python
@app.get("/users/{user_id}")                     # path param
def get_user(user_id: int, active: bool = True, q: str | None = None):  # query params
    return {"id": user_id, "active": active, "q": q}
```

`GET /users/5?active=false&q=ash`. Types validated automatically → 422 on bad input.

## Request body (Pydantic)

```python
from pydantic import BaseModel, EmailStr, Field

class UserIn(BaseModel):
    name: str = Field(min_length=1)
    email: EmailStr

class UserOut(BaseModel):
    id: int
    name: str

@app.post("/users", response_model=UserOut, status_code=201)
def create_user(user: UserIn):
    return {"id": 1, **user.model_dump()}
```

## Errors

```python
from fastapi import HTTPException, status

raise HTTPException(status_code=status.HTTP_404_NOT_FOUND, detail="User not found")
```

## Dependencies

```python
from typing import Annotated
from fastapi import Depends, Header

def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()

def get_token(authorization: Annotated[str, Header()]): ...

@app.get("/items")
def items(db: Annotated[Session, Depends(get_db)]): ...
```

## Routers (split files)

```python
# routers/users.py
from fastapi import APIRouter
router = APIRouter(prefix="/users", tags=["users"])

@router.get("/")
def list_users(): ...

# main.py
app.include_router(users.router)
```

## Async

```python
@app.get("/data")
async def data():
    return await fetch_async()
```

Use `async def` only with async libraries (httpx, asyncpg). Blocking libs → plain `def`.

## CORS

```python
from fastapi.middleware.cors import CORSMiddleware
app.add_middleware(CORSMiddleware, allow_origins=["http://localhost:5173"],
                   allow_methods=["*"], allow_headers=["*"])
```

## Test

```python
from fastapi.testclient import TestClient
client = TestClient(app)
assert client.get("/").status_code == 200
```
