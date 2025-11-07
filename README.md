# FastAPI-Py Backend API

A modern, production-ready backend built with **FastAPI**, **SQLAlchemy**, and **PostgreSQL** — featuring secure **JWT authentication**, modular route structure, and environment-based configuration.

---

## Overview

This project is a RESTful backend API designed with scalability and clarity in mind.  
It provides endpoints for **user authentication**, **posts**, **votes**, and more — following best practices of modern Python development.

### **Key Highlights**
- Secure JWT-based login and registration  
- SQLAlchemy ORM models and Alembic migrations  
- Configurable via `.env` file (Pydantic `BaseSettings`)  
- Clean modular router system (`app/routers`)  
- Auto-generated docs via Swagger UI (`/docs`)  
- PostgreSQL backend (configurable)

---

## 🏗 Project Structure

```
fastapi-py/
├── app/
│   ├── main.py              # Entry point
│   ├── config.py            # Environment configuration
│   ├── database.py          # Database engine and session
│   ├── models.py            # SQLAlchemy models
│   ├── oauth2.py            # JWT and authentication logic
│   ├── routers/             # API route handlers
│   │   ├── post.py
│   │   ├── user.py
│   │   ├── auth.py
│   │   └── vote.py
│   ├── schemas.py           # Pydantic schemas
│   └── utils.py             # Helper functions
├── alembic/                 # Database migrations
├── .env                     # Environment variables (not committed)
├── requirements.txt         # Python dependencies
├── docker-compose.yml       # Docker setup (optional)
├── Dockerfile               # Docker image (optional)
└── README.md
```

---

## Installation & Setup

### Prerequisites
- Python **3.10+**
- PostgreSQL database running locally or via Docker
- (Optional) Docker Desktop if you prefer a containerised setup

---

### Local Development Setup

Clone the repository:
```bash
git clone https://github.com/rupesh110/fastapi-py.git
cd fastapi-py
```

Create and activate a virtual environment:
```bash
python -m venv venv
.\env\Scripts\activate    # (Windows)
# or
source venv/bin/activate   # (macOS/Linux)
```

Install dependencies:
```bash
pip install -r requirements.txt
```

Create a `.env` file in the project root:
```env
# Database Configuration
DATABASE_HOSTNAME=localhost
DATABASE_PORT=5432
DATABASE_USERNAME=postgres
DATABASE_PASSWORD=postgres
DATABASE_NAME=fastapi

# JWT and Security
SECRET_KEY=supersecretkey
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30
```

Make sure PostgreSQL is running locally and matches your `.env` settings.

---

### Run the Application

Start the development server:
```bash
fastapi dev app/main.py
```

or using Uvicorn directly:
```bash
uvicorn app.main:app --reload
```

Then open your browser and navigate to:  
[http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

---

## 🐳 Run with Docker (Optional)

You can also run everything (FastAPI + PostgreSQL) in Docker:

```bash
docker-compose up --build
```

This will:
- Start PostgreSQL as a service  
- Build and run the FastAPI backend  
- Automatically load environment variables from your `.env` file  

Once started, visit your API at:  
👉 [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

---

## Example Endpoints

### Auth
| Method | Endpoint | Description |
|--------|-----------|-------------|
| POST | `/auth/register` | Register new user |
| POST | `/auth/login` | Login & receive JWT token |

### Users
| Method | Endpoint | Description |
|--------|-----------|-------------|
| GET | `/users` | Get all users |
| GET | `/users/{id}` | Get user by ID |

### Posts
| Method | Endpoint | Description |
|--------|-----------|-------------|
| GET | `/posts` | Get all posts |
| POST | `/posts` | Create a new post *(requires auth)* |
| PUT | `/posts/{id}` | Update post *(requires auth)* |
| DELETE | `/posts/{id}` | Delete post *(requires auth)* |

### Votes
| Method | Endpoint | Description |
|--------|-----------|-------------|
| POST | `/vote` | Like/Unlike a post *(requires auth)* |

---

## Tech Stack

| Technology | Purpose |
|-------------|----------|
| **FastAPI** | Modern async Python web framework |
| **SQLAlchemy** | ORM for database management |
| **PostgreSQL** | Relational database |
| **Alembic** | Database migrations |
| **Pydantic** | Data validation and settings |
| **python-jose** | JWT authentication |
| **Passlib (bcrypt)** | Secure password hashing |
| **Uvicorn** | ASGI server for local development |

---

## Example Auth Flow

1. **Register** a new user → `POST /auth/register`  
2. **Login** with credentials → `POST /auth/login`  
   - Returns a JWT access token  
3. **Use token** to access protected endpoints  
   - Add to request header:  
     ```
     Authorization: Bearer <your_token>
     ```

---

## Common Commands

| Command | Description |
|----------|-------------|
| `fastapi dev app/main.py` | Start development server |
| `uvicorn app.main:app --reload` | Run FastAPI manually |
| `docker-compose up --build` | Run API and DB via Docker |
| `alembic upgrade head` | Apply DB migrations |

---

## API Documentation

Once the server is running, you can explore:
- **Swagger UI:** [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)
- **ReDoc:** [http://127.0.0.1:8000/redoc](http://127.0.0.1:8000/redoc)

---

## License

This project is licensed under the **MIT License**.  
Feel free to use, modify, and distribute.

---

> Built using [FastAPI](https://fastapi.tiangolo.com/)
