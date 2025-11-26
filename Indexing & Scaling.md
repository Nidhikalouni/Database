# What is Indexing in a Database?
- Indexing is a technique used to speed up data retrieval in a database.
- It works like an index in a book— instead of scanning every page, you jump directly to the page where the information exists
- Before indexing we have to understand some imp question like
- how the table data is stored in db ? => table data is stored in data pages a data pages is usually of 8kb it consist of 3 parts
🧩 How Table Data Is Stored in a Database (Before Indexing)

Before understanding indexing, we must understand how DBMS stores table data.
## ✅ 1. Data Pages
A data page is the smallest unit of storage inside the database (commonly 8 KB).
Each data page contains:
### Header
Contains metadata like free space, page ID, number of rows, etc.
### Data Records
Actual rows of the table.
### Offset Array
A list of pointers at the end of the page.
Each pointer points to the starting position of a row inside the page.
This helps DBMS quickly reach rows without scanning the whole page.

## ✅ 2. Data Blocks
Data pages are stored inside data blocks (also called disk blocks).
Size: 4 KB to 32 KB
A data block can contain one or multiple data pages
DBMS cannot control the physical placement of blocks on disk.
They are managed by the OS + storage hardware.
Because of this, DBMS maintains a mapping table:
(Data Page Number) → (Physical Data Block)
This map helps the DBMS know where each page exists on disk.

#### 🧠 Why Indexing Is Needed?

Without indexing, the DBMS must perform a Full Table Scan (FTS):
- Read every data page
- Look at every row
- Check the condition
- Slow for large tables

To avoid this, DBMS uses indexes.

##### 🌳 Indexing Uses B+ Tree Data Structure
<img width="654" height="507" alt="image" src="https://github.com/user-attachments/assets/c7609a52-8c6e-43d3-b3ef-b62d3f9f2f62" />

## Types of Indexing in DBMS
Indexes in a database are mainly of two types:
- Clustered Index
- Non-Clustered Index
Both use B+ Tree internally, but they work differently.

#### CLUSTERED INDEXING
<img width="1533" height="815" alt="image" src="https://github.com/user-attachments/assets/20281641-f508-49d3-ba26-577f0fd62aab" />
A clustered index is an index in which the actual table data is physically stored in the same order as the index key.
- Only ONE clustered index is allowed per table
- Because the table data itself is arranged according to the clustered key
- The leaf nodes of the B+ Tree contain the actual data pages
  
###### 📌 Why is it called “Clustered”?
Because data rows are clustered (arranged) according to the index key.

#### ✅ Clustered Index B+Tree Structure 

#### 📌 1. Root Node
- Stores: Keys + pointers to intermediate nodes
- Purpose:
Helps DBMS quickly navigate down the tree toward the correct key range.

#### 📌 2. Intermediate (Internal) Nodes
- Stores: Keys + pointers to leaf nodes
- Purpose:
Acts like a routing map — narrows the search path.

#### 📌 3. Leaf Nodes 
- Stores: Actual table data rows
- Purpose:
In a clustered index, the leaf nodes are the data pages themselves.
This means:
- ✔ The table is physically sorted by the clustered index key
- ✔ Leaf nodes contain full rows (all columns)
- ✔ No separate heap storage exists for table data
  
#### NON-CLUSTERED INDEXING  
A non-clustered index is a separate indexing structure in the database that stores the indexed column values in sorted order, along with pointers that point to the actual data rows stored in the table.
It does not change the physical order of the table data.

### 🧠 Non-Clustered Index B+ Tree Structure

#### 📌 Root Node
- Stores: Keys + pointers to intermediate nodes
- Purpose: Navigate to correct branch
  
#### 📌 Intermediate Nodes
- Stores: Keys + pointers to leaf nodes
- Purpose: Routing levels just like clustered index
  
 #### 📌 Leaf Nodes (MOST IMPORTANT DIFFERENCE)
Leaf nodes store:
- ❌ NOT actual data rows
- ✔ Only key + pointer to data row/page
