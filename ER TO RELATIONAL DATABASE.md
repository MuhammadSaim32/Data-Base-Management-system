# ER TO RELATIONAL DATABASE

### **Method-1: Table for higher-level + lower-level entities**

**Step 1:** Create a table for the **higher-level entity** (superclass).

- This table contains **common attributes** shared by all lower-level entities.

**Step 2:** For each **lower-level entity set (subclass)**:

- Create a table for the subclass.
- Include **columns for its own attributes** + **columns for the primary key of the higher-level entity** (to maintain the link).

**Example: Banking System**

- **Higher-level entity:** Account
- **Lower-level entities:** Savings-Account & Current-Account

**Tables:**

1. **account** → `(account-number, balance)` → contains common attributes.
2. **savings-account** → `(account-number, interest-rate, daily-withdrawal-limit)` → subclass attributes + link to `account`.
3. **current-account** → `(account-number, overdraft-amount, per-transaction-charges)` → subclass attributes + link to `account`.

✅ This method is **safe for all types of generalisation** (overlapping, disjoint, complete, or partial).

---

### **Method-2: Only lower-level tables (no table for higher-level)**

**Condition:** This works only if:

1. **Disjoint:** No entity belongs to more than one lower-level set. 
2. **Complete:** Every entity in the higher-level set belongs to **some lower-level set**.

**Step:**

- Don’t create a table for the higher-level entity.
- Each lower-level table includes:
    - Its own attributes
    - **All attributes of the higher-level entity**        

**Example:** Banking System (disjoint + complete)

**Tables:**

1. **savings-account** → `(account-number, balance, interest-rate, daily-withdrawal-limit)`
2. **current-account** → `(account-number, balance, overdraft-amount, per-transaction-charges)`

✅ Here, the higher-level entity’s attributes (`balance`) are included directly in lower-level tables.

---

### **Drawbacks of Method-2**

1. If **generalisation is overlapping** (an entity could belong to multiple subclasses), Method-2 **duplicates higher-level attributes**, wasting space.
    - E.g., `balance` stored in multiple tables unnecessarily.
2. If **generalisation is not complete** (some entities don’t belong to any subclass), Method-2 **cannot represent those entities**.
    - Some accounts may be left out.
💡 **Summary Tip:**

- **Method-1:** Safer → create table for superclass + subclass tables. Works for **all generalisation types**.
    
- **Method-2:** Only use for **disjoint & complete generalisation**. Saves one table but may cause **redundancy** or **incompleteness** otherwise.

### **1. Disjoint vs Overlapping**

- **Disjoint (d):**
    - An entity in the **superclass** can belong to **at most one subclass**.
    - Example:
        - Superclass: `Account`
        - Subclasses: `Savings` and `Current`
        - An account **cannot be both** savings and current.
- **Overlapping (o):**
    - An entity in the superclass **can belong to more than one subclass**        
    - Example:
        - Superclass: `Employee`
        - Subclasses: `Manager` and `Researcher`
        - An employee **can be both** manager and researcher.

### **2. Complete vs Partial**

- **Complete (total) generalisation:**
    - **Every entity** in the superclass belongs to **at least one subclass**        
    - Example:
        - All accounts must be either savings or current.
- **Partial (incomplete) generalisation:**
    - **Some entities** in the superclass **may not belong** to any subclass        
    - Example:
        - Some employees are neither manager nor researcher—they’re just general staff.

✅ **Quick memory trick:**

| Term        | Meaning                                               | Example                                    |
| ----------- | ----------------------------------------------------- | ------------------------------------------ |
| Disjoint    | Superclass entity → **one subclass only**             | Savings or Current                         |
| Overlapping | Superclass entity → **multiple subclasses**           | Employee: Manager + Researcher             |
| Complete    | All superclass entities belong to some subclass       | All accounts are either savings or current |
| Partial     | Some superclass entities don’t belong to any subclass | Some employees are just staff              |

- **Disjoint vs Overlapping:** defines **if a superclass entity can belong to multiple subclasses**.
    
- **Complete vs Partial:** defines **if every superclass entity must belong to some subclass**.
## Aggregation


A **descriptive attribute** is an **attribute of a relationship** in an ER diagram.


