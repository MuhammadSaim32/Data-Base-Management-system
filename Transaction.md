# **Transaction**

A **transaction** is a sequence of one or more operations on data that are treated as a **single logical unit of work** — meaning they must **all succeed together (commit)** or **all fail together (rollback)**.

**Logical** → it may contain **many physical operations** (like multiple SQL queries, file writes, etc.), but conceptually they belong to **one meaningful task**.

 **Work** → refers to the actual actions done (updates, inserts, deletes, etc.)

 **Unit** → emphasizes that those actions are grouped and treated as **one indivisible package**.

**Rolled back** -> means undoing all changes made in a transaction, returning the system to its state before the transaction began.

## ACID Properties

### **Atomicity**

- **Meaning**: All operations in a transaction succeed **together** or **fail together**.
- **Example**: Transfer $100 from A to B → either both debit and credit happen, or neither does.
#### Why “atomic”?
- From Greek _atomos_ → “uncuttable.”
- In computing: can’t be broken into smaller meaningful parts.
### **Consistency** 

Consistency = **agreement or alignment with rules, standards, or expectations**.

- **Meaning**: The database moves from one **valid state** to another.
- **Example**: After a bank transfer, total money in system stays the same.

### **Isolation**

Isolation ensures that **concurrent transactions do not interfere with each other**, so the database behaves as if each transaction is executed **alone**.

**Key Points:**

- Transactions run **independently** even if happening at the same time.
- Prevents **lost updates, dirty reads, and inconsistencies**.
- Makes sure intermediate results of a transaction are **not visible to others** until committed.

**Example:**

- Alice transfers $100 from Account A → B
- Bob transfers $50 from Account A → C at the same time
- **Without isolation:** Final balance may be wrong (lost update)
- **With isolation:** Transactions are treated sequentially → correct balance is maintained

**Simple Definition:**
 Isolation = transactions appear **independent**; concurrent operations don’t affect each other
 
In **parallel execution**, **isolation is primarily achieved using locks**.
### **Durability**

**Durability = persistence of data**

- **Meaning**: Once a transaction is **committed**, its changes persist even if system crashes.
- **Example**: Money transfer is recorded permanently in the database after commit.

# **BASE (NoSQL)**

- **Meaning** → **Basically Available, Soft state, Eventually consistent**.    
- **Use** → In NoSQL DBMSs (Cassandra, DynamoDB, MongoDB cluster).
- **Why** → Focus on **availability & scalability** (sacrifices strict consistency).

### Components:

1. **Basically Available** → System always responds.
2. **Soft state** → Data may be temporarily inconsistent.
3. **Eventual consistency** → All replicas become consistent later.

### Difference vs ACID

- **ACID** = Strong, strict, reliable (banks).
- **BASE** = Flexible, scalable, eventually consistent (big data, web apps).
#### ==Other ones==

- Transaction states ( love baber notes ).
- it series dbms (3rd edition + handwritten notes) .