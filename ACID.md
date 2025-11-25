# ACID Properties in DBMS
ACID stands for:
1️⃣ A — Atomicity
2️⃣ C — Consistency
3️⃣ I — Isolation
4️⃣ D — Durability
These four properties ensure reliable, safe, and predictable transactions in a database.

#  What is a Transaction?

A transaction is a single logical unit of work performed on a database.
It can consist of one or multiple SQL statements, but they must execute as one complete operation.

👉 Either ALL steps succeed, or NONE do.

## 1. Atomicity — "All or Nothing"
A transaction must complete entirely or not happen at all.
If any part fails → the whole transaction is rolled back.
✔ Example:
Sending money from A to B:
Deduct ₹100 from A’s account
Add ₹100 to B’s account
If adding to B fails → deduction from A must be undone.
➡ Guarantees no partial transactions.

## 2. Consistency — "Valid State → Valid State"
After a transaction, the database must remain in a valid, correct state.
Rules (constraints, triggers, foreign keys) must not be violated.
✔ Example:
User’s email must be unique
Balance cannot go negative
Foreign key must refer to an existing row
A transaction should not corrupt the database.

## 3. Isolation — "Transactions Do Not Interfere"
Multiple transactions running at the same time must behave as if they run one by one, sequentially.
➡ Prevents issues like:
Dirty reads
Unrepeatable reads
Phantom reads
✔ Example:
Two users booking the last movie ticket at the same time → both should NOT get the same seat.
Isolation levels:
Read Uncommitted
Read Committed
Repeatable Read
Serializable (highest)

## 4. Durability — "Once Committed, Always Saved"
When a transaction is committed, the data must remain saved even if:
Power fails
Server crashes
System shuts down
DB ensures this using:
Logs
Backups
Write-ahead logs (WAL)
✔ Example:
If your payment succeeds → the order must not disappear even after a crash.
