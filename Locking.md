# 🔐 Locking in Database
Locking is a mechanism used by database systems to control concurrent access to data so that multiple users/transactions can read/write safely without conflicts.
- It ensures:
  - Data integrity
  - No dirty writes
  - Proper isolation between transactions

## 🎯 Why Do We Need Locks?

When multiple transactions access the same data at the same time, issues may occur like:
- Dirty Read
- Dirty Write
- Lost Update
- Non-repeatable Read

- Locks prevent these issues.

🔑 Types of Locks
### 1️⃣ Shared Lock (S-Lock)

- Applied during read operations.
- Multiple transactions can hold shared locks simultaneously.
- But no write is allowed while S-lock exists.
- 👉 "You can read, and others can also read, but nobody can write."

Example:
```sql
SELECT * FROM users WHERE id=10;
```

### 2️⃣ Exclusive Lock (X-Lock)

- Applied during write operations (INSERT/UPDATE/DELETE).
- Only one transaction can hold it.
- No other transaction can read or write the locked data.
- 👉 "I’m writing—nobody else can read or write this row."

Example:
```sql
UPDATE users SET age=25 WHERE id=10;
```
