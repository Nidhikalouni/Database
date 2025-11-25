# What is Database Normalization?
Database Normalization is the process of organizing data in a database into well-structured tables to reduce redundancy, eliminate anomalies* (insertion, update, deletion), and ensure data is stored logically and efficiently.
It breaks large, unorganized tables into smaller related tables and defines clear relationships between them.
#### Its main goals are:
- Avoid data duplication
- Avoid update, insert, and delete anomalies
- Ensure data integrity
- Make queries more efficient and consistent
* Anomalies -> Update or any other anomaly happens when the same data is stored in multiple places and updating one place requires updating all other places. Normalization avoids update anomalies by storing data only once and linking tables with keys.
## 1NF (First Normal Form)
A table is in 1NF if:
- All values are atomic/ Each column contain atomic(individual) values
  → No multiple values, no repeating groups in a single column.(Example: You cannot store "Math, Science, English" in one cell.)
- Each record is unique
  → Table must have a primary key.
- Each column contains only one type of data
  → No mixing of data types in a column.
