# 🔹 Super Key
A super key is any set of attributes that uniquely identifies a row in a table.
It may contain extra, unnecessary attributes.

# 🔹 Candidate Key
A candidate key is a minimal super key —
i.e., it uniquely identifies a row and has no unnecessary attributes.
A table can have multiple candidate keys.

# 🔹 Primary Key
A primary key is the chosen candidate key to uniquely identify rows.
Must be unique
Cannot be NULL
Only one primary key per table

# 🔹 Foreign Key
A foreign key is an attribute in one table that references a candidate key (usually the primary key) of another table to establish a relationship.

# 🔹 Composite Key
A composite key is a key made up of two or more columns used together to uniquely identify a row.
Example:
(order_id, product_id) uniquely identifies a row in order_items table.

## 🔥 Ultra-short summary 

- Super Key → Unique (extra attributes allowed)

- Candidate Key → Minimal super key

- Primary Key → Chosen candidate key

- Foreign Key → Refers to primary/candidate key in another table

- Composite Key → Key with multiple columns


<img width="1008" height="311" alt="image" src="https://github.com/user-attachments/assets/3dc3ee1a-de0c-481f-8087-4c18651f818e" />

## 1️⃣ Super Key Example

- A super key is any combination of attributes that uniquely identifies a row.
- ✔ Valid super keys (because they identify a student uniquely):

- {roll_no}
- {email}
- {phone}
- {roll_no, name} → still unique, but name is extra
- {email, phone} → extra columns but still unique
- {roll_no, course} → extra column

👉 Super key can have extra unnecessary attributes.

## 2️⃣ Candidate Key Example

- A candidate key is a minimal super key
- → meaning no extra attributes.

From above table, minimal unique identifiers are:
✔ Candidate keys:

- {roll_no}
- {email}
- {phone}

⚠ These are “candidates” from which one will be chosen as Primary Key.

## 3️⃣ Primary Key Example

Choose one candidate key as the main key.

- Primary Key = {roll_no}
- Unique
- Not null
- Chosen for identification

## 4️⃣ Composite Key Example

Use two or more columns together to uniquely identify a row.
Example table: CourseRegistration

student_id	course_id
101	          501
101	          502
102	          501

Here:
- student_id alone is NOT unique
- course_id alone is NOT unique

But together they are unique
- ✔ Composite Key = {student_id, course_id}

## 5️⃣ Foreign Key Example

Table: Students
roll_no  	name
101	      Nidhi
102	      Arjun

Table: Marks
mark_id  	roll_no	  subject  	marks
1	        101	      DBMS	    90
2       	102     	Java	    88

Here:
- Students.roll_no is Primary Key
- Marks.roll_no is Foreign Key referring to Students table
- ✔ Foreign Key = Marks.roll_no → Students.roll_no

🔥 Final Recap 
Key Type	Example
- Super Key	{roll_no}, {roll_no, name}, {email}
- Candidate Key	{roll_no}, {email}, {phone}
- Primary Key	{roll_no}
- Composite Key	{student_id, course_id}
- Foreign Key	Marks.roll_no → Students.roll_no
  
