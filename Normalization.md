# What is Database Normalization?
Database Normalization is the process of organizing data in a database into well-structured tables to reduce redundancy, eliminate anomalies* (insertion, update, deletion), and ensure data is stored logically and efficiently.
It breaks large, unorganized tables into smaller related tables and defines clear relationships between them.
#### Its main goals are:
- Avoid data duplication
- Avoid update, insert, and delete anomalies
- Ensure data integrity
- Make queries more efficient and consistent
⭐ What are anomalies?
Anomalies happen when the same data exists in multiple places and updating in one place requires updating everywhere.
Example of update anomaly:
If a customer changes email, and email is stored in 5 rows → you must update 5 places.
Normalization removes this by storing data only once.

## Original Unnormalized Table
```sql
CREATE DATABASE BookStores;
use BookStores;
Create Table Book_Orders(
    order_id INT,
    customer_name VARCHAR(100),
    customer_email VARCHAR(100),
    customer_address VARCHAR(255),
    book_isbn VARCHAR(20),
    book_title VARCHAR(200),
    book_author VARCHAR(100),
    book_price DECIMAL(10, 2),
    order_date DATE,
    quantity INT,
    total_price DECIMAL(10, 2)
);
INSERT INTO book_orders VALUES
(1, 'John Smith', 'john@example.com', '123 Main St, Anytown', '978-0141439518', 'Pride and Prejudice', 'Jane Austen', 9.99, '2023-01-15', 1, 9.99),
(2, 'John Smith', 'john@example.com', '123 Main St, Anytown', '978-0451524935', '1984', 'George Orwell', 12.99, '2023-01-15', 2, 25.98),
(3, 'Mary Johnson', 'mary@example.com', '456 Oak Ave, Somewhere', '978-0061120084', 'To Kill a Mockingbird', 'Harper Lee', 14.99, '2023-01-20', 1, 14.99),
(4, 'Robert Brown', 'robert@example.com', '789 Pine Rd, Nowhere', '978-0141439518', 'Pride and Prejudice', 'Jane Austen', 9.99, '2023-01-25', 1, 9.99);
Select * from Book_Orders;
```
#### This table has:
- Repeated customer details
- Repeated book details
- No primary key
- Many anomalies
 

## 1NF (First Normal Form)
A table is in 1NF if:
- All values are atomic/ Each column contain atomic(individual) values
  → No multiple values, no repeating groups in a single column.(Example: You cannot store "Math, Science, English" in one cell.)
- Each record is unique
  → Table must have a primary key.
- Each column contains only one type of data
  → No mixing of data types in a column.

  - in above ex the table doesn't have a primary key we can insert same data again and again so it voilates 1nf so-
    
❌ What was wrong?
Table had no primary key → duplicates possible
Data was repeated across rows
✔️ Convert to 1NF
We make order_id + book_isbn the composite primary key.
  ```sql
  CREATE TABLE book_orders_1nf (
    order_id INT,
    book_isbn VARCHAR(20),
    customer_name VARCHAR(100),
    customer_email VARCHAR(100),
    customer_address VARCHAR(255),
    book_title VARCHAR(200),
    book_author VARCHAR(100),
    book_price DECIMAL(10, 2),
    order_date DATE,
    quantity INT,
    total_price DECIMAL(10, 2),
    PRIMARY KEY (order_id, book_isbn)
);
```

## 2NF (Second Normal Form)
A table is in 2NF if:
- It is already in 1NF, AND
- All non-key attributes depend on the entire primary key, not just part of it.
This means:
There must be no partial dependency.
Partial dependency occurs only when the primary key is composite (made of multiple columns).
- Here above their is partial dependency like customer info depend on order_id and book info depend on book_id so they depend on a part of primary key not on whole primary key only quantity and totalprice depend on primary key so it voilates the 2Nf so-
❌ What was wrong?
Our composite key is: (order_id, book_isbn)
But:
- Customer details depend only on order_id
- Book details depend only on book_isbn
This is partial dependency, so it violates 2NF.
✔️ Split into 3 tables
- Orders Table
- Book Table
- Order Items Table
```sql
CREATE TABLE orders_2nf (
    order_id INT PRIMARY KEY,
    customer_name VARCHAR(100),
    customer_email VARCHAR(100),
    customer_address VARCHAR(255),
    order_date DATE
);
```
```sql
CREATE TABLE books_2nf (
    isbn VARCHAR(20) PRIMARY KEY,
    title VARCHAR(200),
    author VARCHAR(100),
    price DECIMAL(10, 2)
);
```
```sql
CREATE TABLE order_items_2nf (
    order_id INT,
    book_isbn VARCHAR(20),
    quantity INT,
    total_price DECIMAL(10, 2),
    PRIMARY KEY (order_id, book_isbn),
    FOREIGN KEY (order_id) REFERENCES orders_2nf(order_id),
    FOREIGN KEY (book_isbn) REFERENCES books_2nf(isbn)
);
```
```sql
-- Sample data for 2NF tables
INSERT INTO orders_2nf VALUES
(1, 'John Smith', 'john@example.com', '123 Main St, Anytown', '2023-01-15'),
(2, 'Mary Johnson', 'mary@example.com', '456 Oak Ave, Somewhere', '2023-01-20'),
(3, 'Robert Brown', 'robert@example.com', '789 Pine Rd, Nowhere', '2023-01-25');
```
```sql
INSERT INTO books_2nf VALUES
('978-0141439518', 'Pride and Prejudice', 'Jane Austen', 9.99),
('978-0451524935', '1984', 'George Orwell', 12.99),
('978-0061120084', 'To Kill a Mockingbird', 'Harper Lee', 14.99);
```
```sql
INSERT INTO order_items_2nf VALUES
(1, '978-0141439518', 1, 9.99),
(1, '978-0451524935', 2, 25.98),
(2, '978-0061120084', 1, 14.99),
(3, '978-0141439518', 1, 9.99);
```

## 3NF (Normal Form)
A table is in 3NF if:
- It is already in 2NF, AND
- There are NO transitive dependencies
(i.e., non-key attributes should NOT depend on other non-key attributes).
In simple words:
⭐ Every non-key column should depend ONLY on the primary key, not on another non-key column.
- in our above ex customer email and address depend on customer name not on order id so here a non-key attribute depend on another non -key attribute so it voilates 3nf so -
  
❌ What was wrong?
In orders_2nf:
| order_id | customer_name | customer_email | customer_address |
Here:
email depends on customer_name
address also depends on customer_name
This is a transitive dependency:
```sql
order_id → customer_name → customer_email, customer_address ```
✔️ Fix by creating a Customers Table
✔️ Updated Orders Table
```sql
CREATE TABLE customers_3nf (
    customer_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100),
    address VARCHAR(255)
);
```
```sql
CREATE TABLE orders_3nf (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    FOREIGN KEY (customer_id) REFERENCES customers_3nf(customer_id)
);
```
❌ Before (Not 3NF)
order_id | book_isbn | quantity | price | total_price
Problem:
total_price = quantity * price
This depends on other non-key attributes, not on the primary key alone.
This is a transitive dependency, so it violates 3NF.
✔️ After (3NF)
order_items_3nf table
```sql

CREATE TABLE books_3nf (
    isbn VARCHAR(20) PRIMARY KEY,
    title VARCHAR(200),
    author VARCHAR(100),
    price DECIMAL(10, 2)
);
```
```sql
CREATE TABLE order_items_3nf (
    order_id INT,
    book_isbn VARCHAR(20),
    quantity INT,
    PRIMARY KEY (order_id, book_isbn),
    FOREIGN KEY (order_id) REFERENCES orders_3nf(order_id),
    FOREIGN KEY (book_isbn) REFERENCES books_3nf(isbn)
);
```
➕ Calculation should be done at query time:
```sql
SELECT 
    order_id,
    book_isbn,
    quantity,
    quantity * price AS total_price
FROM order_items_3nf
JOIN books_3nf ON order_items_3nf.book_isbn = books_3nf.isbn;
```
## BCNF(Normal Form)
A table is in BCNF if:
- It is already in 3NF, AND
- For every functional dependency (X → Y), X must be a superkey. (or every determinant is a super key)
- BCNF is a stronger version of 3NF.
- 🎯 Why BCNF is needed?
Because 3NF allows one special case of dependency:
A non-prime attribute can depend on a prime attribute,
even if that prime attribute is part of a composite key.
BCNF disallows this — BCNF is more strict.
## 4NF(Normal Form)
A table is in 4NF if:
- It is already in BCNF, AND
- It has no multi-valued dependencies (MVDs).
A Multi-Valued Dependency occurs when:
One attribute in a table determines multiple independent values of another attribute.
-🔍 Multi-Valued Dependency (MVD) means:

One attribute of a table can have multiple independent values, and
another attribute also has multiple independent values — and they do NOT depend on each other.
## 5NF ( Project-Join Normal Form (PJNF))
A table is in 5NF if:
- It is already in 4NF, AND
- It has no join dependencies that cannot be expressed using candidate keys.
In simple words:
5NF ensures a table cannot be split into smaller tables without losing data or creating wrong combinations.
All decompositions must be lossless.
