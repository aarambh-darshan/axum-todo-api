# 🚀 Axum Todo API

[![Rust](https://img.shields.io/badge/rust-v1.75%2B-orange.svg)](https://www.rust-lang.org/)
[![Axum](https://img.shields.io/badge/axum-v0.7-blue.svg)](https://docs.rs/axum/latest/axum/)
[![SQLx](https://img.shields.io/badge/sqlx-v0.7-green.svg)](https://docs.rs/sqlx/latest/sqlx/)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

A high-performance, asynchronous REST API for managing todo items, built with **Axum**, **SQLx**, and **PostgreSQL**.

---

## 📑 Table of Contents
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Architecture](#-project-architecture)
- [Getting Started](#-getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Database Setup](#database-setup)
- [API Documentation](#-api-documentation)
- [Postman Collection](#-postman-collection)
- [Author](#-author)

---

## ✨ Features

- **Full CRUD Operations**: Create, Read, Update, and Delete todos.
- **Filtering**: List todos with an optional `completed` status filter.
- **Safety First**: Compile-time verified SQL queries using `sqlx`.
- **Async Power**: Fully asynchronous database operations with PostgreSQL.
- **Robust Error Handling**: Standardized JSON error responses.
- **Modern Standards**: CORS enabled and structured tracing for logging.

## 🛠 Tech Stack

| Tool | Description |
| :--- | :--- |
| **Rust** | The safest and fastest language for systems and web. |
| **Axum** | Ergnomic and modular web framework from the Tokio team. |
| **SQLx** | Modern SQL toolkit with compile-time checked queries. |
| **PostgreSQL** | Robust and reliable relational database. |
| **Tokio** | Industry-standard async runtime for Rust. |
| **Serde** | Powerful framework for serializing and deserializing data. |

---

## 🏛 Project Architecture

The project follows a clean repository-pattern architecture to separate concerns:

```bash
src/
├── main.rs          # Entry point: Server setup, Routing, and Layers
├── models.rs        # Data Transfer Objects (DTOs) and Database Models
├── handlers.rs      # Business logic: Request extraction and response mapping
├── repository.rs    # Data Access: SQL queries and database interaction
├── db.rs           # Infrastructure: Connection pooling and configuration
└── error.rs        # Error handling: Unified error types and HTTP mapping
```

---

## 🚀 Getting Started

### Prerequisites

- **Rust**: `v1.75` or higher ([Install Rust](https://www.rust-lang.org/tools/install))
- **PostgreSQL**: A running instance ([Docker recommended](https://hub.docker.com/_/postgres))
- **SQLx CLI** (Optional but recommended):
  ```bash
  cargo install sqlx-cli --no-default-features --features postgres
  ```

### Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/aarambh-darshan/axum-todo-api.git
   cd axum-todo-api
   ```

2. **Configure Environment**:
   Create a `.env` file in the root directory:
   ```env
   DATABASE_URL=postgres://your_user:your_password@localhost:5432/your_db
   PORT=3000
   ```

### Database Setup

Run the migration script to create the `todos` table:
```bash
# Using sqlx-cli (if installed)
sqlx migrate run

# Or manually via psql
psql $DATABASE_URL -f migrations/001_init.sql
```

---

## 📖 API Documentation

### 📌 Todo Object
```json
{
  "id": "uuid",
  "title": "string",
  "description": "string | null",
  "completed": "boolean",
  "created_at": "datetime",
  "updated_at": "datetime"
}
```

### Endpoints

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `POST` | `/todos` | **Create** a new todo |
| `GET` | `/todos` | **List** all todos (filter: `?completed=true`) |
| `GET` | `/todos/{id}` | **Get** a specific todo details |
| `PATCH` | `/todos/{id}` | **Update** title, description, or status |
| `PATCH` | `/todos/{id}/complete` | **Mark** a todo as completed |
| `DELETE` | `/todos/{id}` | **Delete** a todo |

---

## 📮 Postman Collection

For a more interactive way to test the API, you can use the included Postman collection.

### How to use:

1. **Import the collection**:
   - Open Postman.
   - Click the **Import** button.
   - Select the file [Axum_Todo_API.postman_collection.json](Axum_Todo_API.postman_collection.json) from the project root.

2. **Set up Environment**:
   - The collection uses a `baseUrl` variable.
   - By default, it is set to `http://localhost:3000`.
   - You can create a new Environment in Postman or edit the Collection's variables to change the port or host if needed.

3. **Run Requests**:
   - All CRUD operations are pre-configured.
   - Ensure the server is running (`cargo run`) before sending requests.

---

## 🧪 Usage Examples (Curl)

### 1. Create a Todo
```bash
curl -X POST http://localhost:3000/todos \
  -H "Content-Type: application/json" \
  -d '{"title": "Learn Rust", "description": "Master Axum and SQLx"}'
```

### 2. Update a Todo
```bash
curl -X PATCH http://localhost:3000/todos/{uuid} \
  -H "Content-Type: application/json" \
  -d '{"title": "Updated Title"}'
```

### 3. Error Case (404 Not Found)
```bash
curl -v http://localhost:3000/todos/00000000-0000-0000-0000-000000000000
# Response: 404 Not Found
# Body: {"status":"fail","message":"Todo not found"}
```

---

## 👨‍💻 Author

Created by **[Darshan Vichhi](https://github.com/aarambh-darshan)**

Feel free to reach out for collaborations or feedback!

---

## 📄 License

Distributed under the **MIT License**. See `LICENSE` for more information.