# **Indexing in DBMS**

An **index** is a data structure that helps **locate records in a file quickly** without scanning the entire file.

A file or table can have **multiple indices** on **different search keys**.
## **1. File Order**

File order refers to the **sequence in which records are stored in a file**.

- A file can be **sorted by a key (primary key or any other key)** or **non-key attribute**.
- The attribute used for sorting defines the **file’s order**.

**Example:**

Students table:

| StudentID | Name | Dept |
| --------- | ---- | ---- |
| 101       | Ali  | CS   |
| 102       | Sara | EE   |
| 103       | Omar | CS   |

### Sorted by **StudentID (primary key)**

| StudentID | Name | Dept |
| --------- | ---- | ---- |
| 101       | Ali  | CS   |
| 102       | Sara | EE   |
| 103       | Omar | ME   |

- File is **sorted by key** → primary index can be created.
- Since it’s sorted by **primary key**, a **sparse primary index** is usually used (one entry per block/page).
### Sorted by **Dept (non-key attribute)**

| StudentID | Name | Dept |
| --------- | ---- | ---- |
| 101       | Ali  | CS   |
| 103       | Omar | CS   |
| 102       | Sara | EE   |

- File is **sorted by non-key attribute** → primary index can still be created.
- Since Dept is **not unique**, the index is **dense** (one entry per record).
- Useful when querying **all students of a department**    

**Key Points:**

1. File can be sorted on **key** or **non-key attribute**. 
2. **Primary index** can be created on any attribute the file is sorted by.
3. **Uniqueness is not required** for primary indexing.
4. A **primary index requires the file to have a particular sequence**, i.e., it **must be sorted** on the attribute you are indexing. Uniqueness is optional; **order is mandatory**.

## **2. Primary Index (Clustering Index)**

**Definition:**  
An index on the **key that defines the particular order of the file**.

**Key Points:**

1. File must be **sorted** on the search key.
2. Can be **dense or sparse**, depending on the attribute:
    - **Primary key** → usually sparse
    - **Non-key attribute** → dense
3. Only **one primary index** per file.
 
 **Primary index → tied to the file’s order.**   Since the file can have **only one order at a time**, there can be **only one primary index per file**.

4. **Do not confuse with primary key:**
    - Primary key → ensures **uniqueness**
    - Primary index → helps in **fast searching**, uniqueness not required
### **Types of Primary Index**

| Type       | When Used                            | Description                                   | Example / Notes                                          |
| ---------- | ------------------------------------ | --------------------------------------------- | -------------------------------------------------------- |
| **Dense**  | File sorted by **non-key** attribute | Index entry for **every record**              | Every record has a pointer. Fast search, uses more space |
| **Sparse** | File sorted by **primary key**       | Index entry for **one record per block/page** | Saves space, slightly slower search within block         |

---

## **3. Secondary Index**

**Definition:**  
An index on a **key that is NOT the sort key of the file**.

**Key Points:**

1. File is **not sorted** on this key.
2. Must be **dense**, because every record needs an entry.
3. Can be **many secondary indices** per file.

**Example:**

File sorted by `StudentID`:

| StudentID | Name | Dept |
| --------- | ---- | ---- |
| 101       | Ali  | CS   |
| 102       | Sara | EE   |
| 103       | Omar | ME   |

- Secondary index on `Name` (dense):

| Name | Pointer to Record |
| ---- | ----------------- |
| Ali  | 101               |
| Sara | 102               |
| Omar | 103               |

- Secondary index on `Dept` (dense):
    

| Dept | Pointer to Record |
| ---- | ----------------- |
| CS   | 101               |
| EE   | 102               |
| ME   | 103               |

---

## **4. Dense vs Sparse Indexing**

| Feature | Dense Index                | Sparse Index                 |
| ------- | -------------------------- | ---------------------------- |
| Entries | One for **every record**   | One per **block/page**       |
| Usage   | Primary or Secondary index | Only primary index           |
| Speed   | Very fast                  | Slightly slower (scan block) |
| Space   | More storage required      | Less storage                 |

**Important:**

- Primary index → dense (non-key) or sparse (primary key)
- Secondary index → always dense
## **5. Multiple Indices on a File**

- A file can have **multiple indices** to support searches on **different keys**.
- **Primary index:** only **one**, based on **file’s sort key**
- **Secondary indices:** can be **many**, for other search keys

**Example Table:**

| StudentID | Name | Dept |
| --------- | ---- | ---- |
| 101       | Ali  | CS   |
| 102       | Sara | EE   |
| 103       | Omar | ME   |

- Primary index → `StudentID` (sparse)
- Primary index → `Dept` (dense, file sorted by Dept)
- Secondary index → `Name` (dense)
## **6. Quick Comparison**

| Feature           | Primary Index                          | Secondary Index              |
| ----------------- | -------------------------------------- | ---------------------------- |
| Based on          | Key that **defines file order**        | Key **not used for sorting** |
| File sorted?      | Must be sorted                         | Not sorted                   |
| Dense or Sparse   | Dense (non-key) / Sparse (primary key) | Always Dense                 |
| Space Requirement | Less (sparse) / More (dense)           | More (dense only)            |
| Search Efficiency | Fast                                   | Fast                         |

---

## **7. Key Takeaways**

1. **File order** = sequence of records in the file.
2. File can be sorted by **key or non-key attribute**. 
3. **Primary index** → on file’s sort key, dense (non-key) or sparse (primary key), only one per file.
4. **Secondary index** → on any other key, always dense, multiple allowed.
5. **Dense index** = every record has an entry.
6. **Sparse index** = one entry per block.
7. **Primary key ≠ Primary index:** uniqueness vs file order.


## **Can a Secondary Index be on Key Attributes?**

Yes.
- Example: File is **sorted by StudentID** → so **primary index** is on StudentID.
- But you can also create a **secondary index on Name** (if Name is unique → it’s a key).
- That secondary index will still be **dense**, because the file isn’t sorted on Name.    


###  **Key Point**

A **secondary index can be created on both key and non-key attributes** — as long as the attribute is **not the one that defines the file’s order**.  
And in **all cases, secondary index is dense**.


**Primary index on non-key attribute (duplicates allowed)** → dense, AND this is called a **clustering index**, because groups (“clusters”) of records form under the same key 
(on internet ^)


#### ==Other ones==

- Indexing in dbms(  love baber notes + handwritten notes ).