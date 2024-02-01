
# FastAPI Cheat Sheet

## Setup and Installation

```bash
# Install FastAPI
pip install fastapi

# Install an ASGI server, such as uvicorn
pip install uvicorn
```

## Basic App Structure

```python
# main.py
from fastapi import FastAPI

app = FastAPI()

@app.get('/')
def read_root():
    return {"Hello": "World"}
```

## Running the App

```bash
# Run the app with uvicorn
uvicorn main:app --reload
```

- `main`: the file `main.py` (the Python "module").
- `app`: the object created inside of `main.py` with the line `app = FastAPI()`.
- `--reload`: make the server restart after code changes. Only use for development.

## Path Parameters

```python
@app.get('/items/{item_id}')
def read_item(item_id: int):
    return {"item_id": item_id}
```

## Query Parameters

```python
@app.get('/items/')
def read_item(skip: int = 0, limit: int = 10):
    return fake_items_db[skip : skip + limit]
```

## Request Body

```python
from pydantic import BaseModel

class Item(BaseModel):
    name: str
    description: str = None
    price: float
    tax: float = None

@app.post('/items/')
def create_item(item: Item):
    return item
```

## Response Model

```python
class ItemOut(BaseModel):
    name: str
    price: float

@app.post('/items/', response_model=ItemOut)
def create_item(item: Item):
    return item
```

## Path and Query Parameters

```python
@app.get('/users/{user_id}/items/{item_id}')
def read_user_item(user_id: int, item_id: str, q: str = None):
    return {"user_id": user_id, "item_id": item_id, "q": q}
```

## Dependency Injection

```python
from fastapi import Depends

def get_db():
    db = DBSession()
    try:
        yield db
    finally:
        db.close()

@app.get('/items/')
def read_items(db = Depends(get_db)):
    # use db here
```

## OAuth2 with Password and Bearer

```python
from fastapi.security import OAuth2PasswordBearer

oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

@app.post('/token')
def token():
    return {"access_token": "your_token", "token_type": "bearer"}

@app.get('/users/me')
def read_users_me(token: str = Depends(oauth2_scheme)):
    return {"token": token}
```

## Background Tasks

```python
from fastapi import BackgroundTasks

def write_log(message: str):
    with open("log.txt", mode="a") as log:
        log.write(message)

@app.post('/send-notification/{email}')
def send_notification(email: str, background_tasks: BackgroundTasks):
    background_tasks.add_task(write_log, f"notification sent to {email}")
    return {"message": "Notification sent in the background"}
```

## Middleware

```python
from fastapi import FastAPI
from starlette.middleware.cors import CORSMiddleware

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)
```

