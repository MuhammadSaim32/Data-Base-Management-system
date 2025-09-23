
## How to implement Atomicity and Durability in Transactions

### **Shadow-Copy Scheme**

A method of making a duplicate (shadow copy) of the database to safely apply updates, ensuring either all changes are applied or none.

#### **Step-by-Step Process**

- **Single active transaction** assumed at a time.
- **db-pointer** on disk points to the current DB copy.
- Transaction T starts → **creates a full copy** (`DB_new`) of the DB.
- Updates applied **only to `DB_new`**; `DB_old` untouched.
- **Abort:** delete `DB_new` 
- **Commit:**
    - Write all `DB_new` pages to disk.
    - Update **db-pointer** to `DB_new` (commit point).
    - Delete `DB_old`.
- **Atomicity:**
    - If failure occurs before db-pointer update → DB_old intact.
    - Abort = delete new copy → all-or-nothing guarantee.
        
- **Durability:**
    - Commit = db-pointer update.
    - If crash occurs **before** pointer update → DB_old seen on restart.
    - If crash occurs **after** pointer update → DB_new seen on restart.
#### **Important Points**

- **Atomic db-pointer write:**
    - Disk writes are **atomic at sector/block level**, not byte-by-byte.
    - Pointer stored in **single sector/block** → guarantees atomic commit.
- **Inefficiency:** copying full DB for each transaction is slow and space-consuming.
   - Sector = **single page of a notebook ( disk )** .
   - Block = **group of pages** (OS usually handles a few pages together).



#### ==Other ones==

- How to implement Atomicity and Durability in Transactions ( love baber notes + handwritten notes ).

### Transaction Management vs. Recovery Management

- **Transaction Management:** This part makes sure that a transaction is done correctly while the database is running. It ensures that a transaction is either fully completed or completely canceled. 
    
- **Recovery Management:** It's needed for unexpected problems like a system crash or power failure. Its job is to fix the database after a crash and make sure no completed transactions are lost and no incomplete ones are saved.

**In short, the transaction manager keeps things right during normal work, while the recovery manager fixes things after a disaster.**



### Checkpoint Recovery (DBMS)

- **Checkpoint** = a marker in the log that says: _“All transactions before this are safely written to disk.”_    
- Used to **speed up crash recovery**.
- On recovery:
    1. Start from **last checkpoint** (no need to scan full log).
    2. **UNDO** → uncommitted transactions after checkpoint.
    3. **REDO** → committed transactions after checkpoint.

In short: **Checkpoint = savepoint in DB; recovery starts from it → Undo uncommitted + Redo committed.**

checkpoints are used in both deferred & immediate log methods to mark a safe state and make recovery faster.