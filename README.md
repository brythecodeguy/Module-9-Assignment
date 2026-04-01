# Module 9

## Module Overview

This module works with PostgreSQL in a Dockerized environment and execute raw SQL commands using pgAdmin. The goal was to understand how relational databases function by performing core SQL operations.

---

## Docker Setup

I started the application using:

docker-compose up --build

This will start:

- FastAPI application
- PostgreSQL database
- pgAdmin interface

---

## Access pgAdmin

Go to:
<http://localhost:5050>

Login (based on docker-compose):

- Email: <admin@example.com>  
- Password: admin  

---

## Database Connection

Connect to PostgreSQL using:

- Host: db  
- Username: postgres  
- Password: postgres  
- Database: fastapi_db  

---

## Example SQL Operations

### 1️: Create Tables

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) NOT NULL UNIQUE,
    email VARCHAR(100) NOT NULL UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE calculations (
    id SERIAL PRIMARY KEY,
    operation VARCHAR(20) NOT NULL,
    operand_a FLOAT NOT NULL,
    operand_b FLOAT NOT NULL,
    result FLOAT NOT NULL,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    user_id INTEGER NOT NULL,
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
```

---

### 2️: Insert Data

```sql
INSERT INTO users (username, email)
VALUES
('alice', '<alice@example.com>'),
('bob', '<bob@example.com>');

INSERT INTO calculations (operation, operand_a, operand_b, result, user_id)
VALUES
('add', 2, 3, 5, 1),
('subtract', 10, 4, 6, 1),
('multiply', 4, 5, 20, 2);
```

---

### 3️: Query Data

```sql
SELECT * FROM users;

SELECT * FROM calculations;

SELECT u.username, c.operation, c.result
FROM calculations c
JOIN users u ON c.user_id = u.id;
```

---

### 4️: Update Data

```sql
UPDATE calculations
SET result = 7
WHERE id = 2;
```

---

### 5: Delete Data

```sql
DELETE FROM calculations
WHERE id = 3;
```

---

## Documentation

- [Module9_SQL_Screenshots.pdf](./Module9_Screenshots.pdf) – SQL execution screenshots and Docker setup  
- [Module9_Reflection.pdf](./Module9_Reflection.pdf) – Reflection on the assignment  

---
