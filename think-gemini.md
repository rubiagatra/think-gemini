# Let's think like seniors using Gemini

Build an API to create, read, update, and delete tasks. Each task has a title, description, and status.

## Let's use FastAPI

```bash
uv add "fastapi[standard]" pydantic
```

---

## Let's Once again as a Junior
```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()
tasks = []

class Task(BaseModel):
    title: str
    description: str
    status: str

@app.post("/tasks")
def create_task(task: Task):
    tasks.append(task.model_dump())
    return task

@app.get("/tasks")
def get_tasks():
    return tasks

@app.put("/tasks/{task_id}")
def update_task(task_id: int, task: Task):
    tasks[task_id] = task.model_dump()
    return task

@app.delete("/tasks/{task_id}")
def delete_task(task_id: int):
    tasks.pop(task_id)
    return {"message": "deleted"}
```

---

##  Run the Server
```bash
uv run fastapi dev main.py
```

## Let's Try

```bash
curl -X POST "http://localhost:8000/tasks" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Buy groceries",
    "description": "Milk, eggs, bread",
    "status": "pending"
  }'

curl -X GET "http://localhost:8000/tasks"

curl -X POST "http://localhost:8000/tasks" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Write documentation",
    "description": "API docs",
    "status": "in_progress"
  }'

curl -X PUT "http://localhost:8000/tasks/0" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Buy groceries - UPDATED",
    "description": "Milk, eggs, bread, chicken",
    "status": "completed"
  }'

curl -X DELETE "http://localhost:8000/tasks/0"

```

---

## Before we start, Using AI for Learning

- Ask AI for an initial version and then refactor it to match your expectations.
- Write the initial version yourself and ask AI to review and improve it.
- Write the critical parts and ask AI to do the rest.
- Write an outline of the code and ask AI to fill the missing parts.

```bash
Get your hands dirty. Write the code. It's what you are good at.
You are a software engineer. Don't become a prompt refiner.

```



---

## Using Gemini

```bash
"I need to build a REST API for task management using FastAPI. Each task has title, description, and status. I need CRUD operations. What should I consider before starting?"

```
