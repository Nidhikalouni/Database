# What is Database Normalization?
Database Normalization is the process of organizing data in a database into well-structured tables to reduce redundancy, eliminate anomalies* (insertion, update, deletion), and ensure data is stored logically and efficiently.
It breaks large, unorganized tables into smaller related tables and defines clear relationships between them.
#### Its main goals are:
- Avoid data duplication
- Avoid update, insert, and delete anomalies
- Ensure data integrity
- Make queries more efficient and consistent
* Anomalies -> Update or any other anomaly happens when the same data is stored in multiple places and updating one place requires updating all other places. Normalization avoids update anomalies by storing data only once and linking tables with keys.

## DB Table
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
## 1NF (First Normal Form)
A table is in 1NF if:
- All values are atomic/ Each column contain atomic(individual) values
  → No multiple values, no repeating groups in a single column.(Example: You cannot store "Math, Science, English" in one cell.)
- Each record is unique
  → Table must have a primary key.
- Each column contains only one type of data
  → No mixing of data types in a column.
## 2NF (Second Normal Form)
