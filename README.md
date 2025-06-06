# SQLite Project

This project uses SQLite as the lightweight, serverless database engine. It’s ideal for embedded and local storage in mobile or desktop applications. Below are the setup instructions, schema examples, commands, and best practices.

## 📦 Requirements

* SQLite3 installed (comes preinstalled on many systems)
* SQLite CLI or GUI tools (e.g., DB Browser for SQLite)

## 📁 Project Structure

```
project/
│
├── db/
│   ├── init.sql              # Initial database setup script
│   ├── schema.sql            # Table definitions
│   └── seed.sql              # Sample data
│
├── app.db                   # SQLite database file
├── README.md                # Documentation
└── your_code_files_here/
```

## 🏗️ Database Setup

### 1. Create a New Database

```bash
sqlite3 app.db
```

### 2. Load Schema

```bash
sqlite3 app.db < db/schema.sql
```

### 3. (Optional) Seed Data

```bash
sqlite3 app.db < db/seed.sql
```

## 🗃️ Example Schema

```sql
CREATE TABLE users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT,
    email TEXT UNIQUE,
    password TEXT,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

## 🛠️ CRUD Operations

* Insert:

  ```sql
  INSERT INTO users (name, email, password) VALUES ('John Doe', 'john@example.com', '12345');
  ```
* Select:

  ```sql
  SELECT * FROM users;
  ```
* Update:

  ```sql
  UPDATE users SET name = 'Jane Doe' WHERE id = 1;
  ```
* Delete:

  ```sql
  DELETE FROM users WHERE id = 1;
  ```

## 🧩 Joins

```sql
SELECT users.name, orders.amount
FROM users
JOIN orders ON users.id = orders.user_id;
```

## 📌 Common Commands

* Show tables:

  ```sql
  .tables
  ```
* Describe table:

  ```sql
  PRAGMA table_info(users);
  ```
* Export database:

  ```sql
  .output backup.sql
  .dump
  .exit
  ```
* Import SQL file:

  ```bash
  sqlite3 app.db < file.sql
  ```

## 🔄 Triggers & Views

### Trigger Example

```sql
CREATE TRIGGER set_created_at
BEFORE INSERT ON users
FOR EACH ROW
BEGIN
  UPDATE users SET created_at = CURRENT_TIMESTAMP WHERE id = NEW.id;
END;
```

### View Example

```sql
CREATE VIEW user_summary AS
SELECT id, name, email FROM users;
```

## ⚙️ Transactions

```sql
BEGIN TRANSACTION;
UPDATE users SET name = 'Alice';
COMMIT;
-- or ROLLBACK;
```

## 📈 Performance Tips

* Use indexes:

  ```sql
  CREATE INDEX idx_email ON users(email);
  ```
* Keep schema simple for mobile apps
* Use WAL mode for better concurrency:

  ```sql
  PRAGMA journal_mode=WAL;
  ```

## 🔒 Security Notes

* SQLite is file-based—protect the `.db` file using file permissions
* Encrypt the database if needed (e.g., SQLCipher)
* Always validate and sanitize user input

## 💾 Backup & Restore

* Backup:

  ```bash
  sqlite3 app.db ".backup backup.db"
  ```
* Restore:

  ```bash
  cp backup.db app.db
  ```

## 📚 References

* [SQLite Official Documentation](https://sqlite.org/docs.html)
* [DB Browser for SQLite](https://sqlitebrowser.org/)

## 📞 Contact

For any issues or contributions, please open an issue or submit a pull request.
