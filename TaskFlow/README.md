# TaskFlow: Task Management REST API (FastAPI + MySQL)

ITW III course project. A task management REST API built with **FastAPI** and **MySQL** (through the SQLAlchemy ORM) that runs on localhost. Users register, log in with **JWT** tokens, and manage their own tasks. The Jupyter notebook creates the database tables, fills them with generated data, starts the server, tests every endpoint and draws analytics charts.

**Base project:** [isaac0yen/Python-CRUD](https://github.com/isaac0yen/Python-CRUD) (FastAPI + SQLAlchemy + SQLite task manager). This project keeps its overall structure and extends it (see "What was added" below).

## Features
- Full CRUD on tasks (create, read, update, delete)
- User registration and login with **JWT** authentication and **bcrypt** password hashing
- Each user can only see and change their own tasks
- Search, filters (status, priority, category, due date) and pagination
- Analytics endpoints: overdue tasks, completion rate by category, tasks per user (uses `GROUP BY` and `JOIN`)
- Input validation with Pydantic and proper HTTP status codes
- About 900 tasks of test data generated with Faker
- Endpoint tests and charts (Pandas + Matplotlib) inside the notebook

## What was added to the base project
| Part | Base project | TaskFlow |
|---|---|---|
| Database | SQLite | MySQL |
| Tables | `tasks` only | `users` + `tasks` with a foreign key and indexes |
| Login | None | JWT + bcrypt |
| Access control | Everyone sees all tasks | Each user sees only their own tasks |
| Task list | Basic filters | Filters, title search, pagination |
| Analytics | None | 3 endpoints + charts |
| Test data | Entered by hand | Faker-generated seed data |
| Testing | None | Endpoint tests in the notebook |

## API endpoints
| Method | Address | Description | Login |
|---|---|---|---|
| POST | `/register` | Create a user | No |
| POST | `/login` | Get a JWT token | No |
| POST | `/tasks` | Create a task | Yes |
| GET | `/tasks` | List own tasks (filters, search, pagination) | Yes |
| GET | `/tasks/{id}` | Read one task | Yes |
| PUT | `/tasks/{id}` | Update a task | Yes |
| DELETE | `/tasks/{id}` | Delete a task | Yes |
| GET | `/analytics/overdue` | Overdue unfinished tasks | Yes |
| GET | `/analytics/completion-by-category` | Completion rate per category | Yes |
| GET | `/analytics/tasks-per-user` | Task count per user | Yes |

## How to run
1. Install Python 3.10+ and MySQL Server.
2. Create the database in MySQL:
   ```sql
   CREATE DATABASE taskflow_db;
   ```
3. Install the libraries:
   ```bash
   pip install -r requirements.txt
   ```
4. Open `TaskFlow_Project.ipynb` and, in the database connection cell, replace `your_mysql_password` with your MySQL password. Do not commit your real password. You can also set the environment variables `TASKFLOW_DB_USER` and `TASKFLOW_DB_PASSWORD` instead. A password that contains `@` must be written as `%40` in this notebook.
5. Run all cells in order. The API starts on `http://127.0.0.1:8000`, and the interactive Swagger page is at `http://127.0.0.1:8000/docs` (demo login: `demo` / `demo123`).

## Folder contents
| File | Description |
|---|---|
| `TaskFlow_Project.ipynb` | Full implementation, tests and charts |
| `TaskFlow_Project_Report.pdf` | Project report |
| `requirements.txt` | Python libraries and versions used |

## Tech stack
Python, FastAPI, Uvicorn, SQLAlchemy, PyMySQL, MySQL, Pydantic, python-jose (JWT), passlib + bcrypt, Faker, Requests, Pandas, Matplotlib.
