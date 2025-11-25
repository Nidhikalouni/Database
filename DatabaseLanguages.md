# Database Languages (DBMS Languages)

Database languages are used to create, modify, access, and control a database in a DBMS.
They are mainly divided into 4 types:

## 1. DDL – Data Definition Language
Used to define the structure of the database (tables, schema).
Common DDL Commands   Command	Description
- CREATE -> Creates a new database/table
- ALTER	 -> Modifies a table (add/remove column)
- DROP  ->	Deletes a table/database
- TRUNCATE  ->	Removes all rows from a table, but keeps structure

## 2. DML – Data Manipulation Language
Used to insert, update, delete, and retrieve data in tables.
Common DML Commands   Command	Description
- INSERT	Insert new records
- UPDATE	Modify existing records
- DELETE	Remove records
- SELECT	Retrieve data (sometimes categorized as DQL)
  
## 3. DQL – Data Query Language
Used only for querying the database.
Command	Description
- SELECT	Retrieves data from tables
Note: Many books include SELECT inside DML, but conceptually DQL is separate.

## 4. DCL – Data Control Language
Used to control access and permissions.
Command	Description
- GRANT	Give permission to users
- REVOKE	Remove user permissions

## 5. TCL – Transaction Control Language
Used to control transactions in a database.
Common TCL Commands Command	Description
- COMMIT	Save changes permanently
- ROLLBACK	Undo changes
- SAVEPOINT	Create a save checkpoint
- SET TRANSACTION	Set transaction properties
## Summary Table
Category	Purpose	Commands

DDL	Define structure	CREATE, ALTER, DROP, TRUNCATE

DML	Manipulate data	INSERT, UPDATE, DELETE

DQL	Query data	SELECT

DCL	Control access	GRANT, REVOKE

TCL	Manage transactions	COMMIT, ROLLBACK, SAVEPOINT

### ✅ DELETE vs TRUNCATE vs DROP
##### 1. DELETE
- Removes rows (records) from a table.
- You can delete specific rows using WHERE.
- Table structure remains.
- Slow because it logs each deleted row.
- Can be rolled back (transaction safe).

Example:
```sql 
DELETE FROM Students WHERE id = 5;
```

#### 2. TRUNCATE
- Removes all rows from a table.
- You cannot delete specific rows.
- Faster than DELETE (minimal logging).
- No WHERE clause.
- Table structure remains, only data deleted.
- Cannot be rolled back in some DBMS (DDL operation).

Example:
```sql
TRUNCATE TABLE Students;
```

#### 3. DROP
- Deletes the entire table from the database.
- Removes data + structure + indexes + constraints.
- Very dangerous — cannot be rolled back easily.
- After DROP, the table no longer exists.

Example:
```sql
DROP TABLE Students;
```
