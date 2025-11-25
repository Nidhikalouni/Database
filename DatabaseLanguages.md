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
