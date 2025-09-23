# Normlization
### . Trivial FD (obvious ones)

A **trivial functional dependency** means the dependency is **always true**, because the thing on the right side is already included in the left side.

Formula:

X→Y is trivial if Y⊆X
### 3. Easy Examples

- **Example 1:**  
    (StudentID, Name) → Name 
    (Because `Name` is already inside `(StudentID, Name)`)
    
- **Example 2:**  
    (A, B) → A 
    (Because A is part of (A, B))
    
- **Example 3:**  
    RollNo → RollNo 
    (An attribute always determines itself.

###  Non-Trivial FD 

If the right side is **not already in the left side**, it’s **non-trivial**.

- Example: StudentID → Name (non-trivial, because Name is not part of StudentID).

# Armstrong’s Axioms (Rules of FD)

**Armstrong’s Axioms** are a set of inference rules (Reflexivity, Augmentation, Transitivity) used to derive all valid functional dependencies in a relational database.

## **1. Reflexivity Rule**

> If ‘A’ is a set of attributes and ‘B’ is a subset of ‘A’. Then, A → B holds.

 Meaning: Any set of attributes always determines its own subset.

**Line 2 (same in other words):**

> If A ⊇ B then A → B.

 Example:

- A = {RollNo, Name}
- B = {Name} (subset of A)
- So {RollNo, Name} → {Name} is always true (trivial FD).
## **2. Augmentation Rule**

> If B can be determined from A, then adding an attribute to this functional dependency won’t change anything.

Meaning: If you know **A → B**, then you can safely add extra attributes to both sides, and the dependency still holds.

**Line 2:**

> If A → B holds, then AX → BX holds too, where X is a set of attributes.

 Example:

- Suppose A = {RollNo}, B = {Name}
- We know RollNo → Name.
- Add attribute `Dept` (X).
- Then {RollNo, Dept} → {Name, Dept} also holds.
## **3. Transitivity Rule**

> If A determines B and B determines C, we can say that A determines C.

 Meaning: FD works like a chain.

> If A → B and B → C then A → C.

 Example:

- RollNo → Name
- Name → Address
- So RollNo → Address (by transitivity).

**Summary in simple words**

- **Reflexivity:** A set determines its own subsets.
- **Augmentation:** If A → B, then adding extra attributes still keeps the FD true.
- **Transitivity:** If A → B and B → C, then A → C.
### Example Relation

We have a relation:  
**Student(RollNo, Name, Dept, Address)**

Given FDs (functional dependencies):

1. **RollNo → Name**
2. **Name → Address**
### Step-by-Step Derivation (Inference)

**Step 1. Start with known FDs:**

- RollNo → Name
- Name → Address

**Step 2. Apply Transitivity**

- From RollNo → Name, and Name → Address
- We can infer: **RollNo → Address** 

**Step 3. Apply Augmentation**

- From RollNo → Name
- Add Dept on both sides → {RollNo, Dept} → {Name, Dept} 


**Step 4. Apply Reflexivity** 

- Any set determines its own subset
- Example: {RollNo, Name} → Name 


###  Final Inferred FDs

From just the two given FDs, we can infer:

- RollNo → Name (given)
- Name → Address (given)
- RollNo → Address (by Transitivity)
- {RollNo, Dept} → {Name, Dept} (by Augmentation)
- {RollNo, Name} → Name (by Reflexivity)

That’s how **inference** works: starting with given dependencies and using Armstrong’s rules to **derive new ones**.


##  **Full Functional Dependency**

**Definition:**  
A functional dependency **X → Y** is **full** if you cannot remove any attribute from **X** without breaking the dependency.

 Meaning:  
All attributes in the left-hand side are **necessary** to determine the right-hand side.

 **Example:**  

Relation: **R(StudentID, CourseID, Grade)**

- FD: **(StudentID, CourseID) → Grade**
- Here, `Grade` depends on **both** `StudentID` and `CourseID` together.
- You cannot remove either one — if you remove `CourseID`, you can’t determine `Grade`.
- So this is a **Full FD**.
## 2. **Partial Functional Dependency**

**Definition:**  
A functional dependency **X → Y** is **partial** if some attribute(s) can be removed from **X** and the dependency still holds.

Meaning:  
Only part of the left-hand side is enough to determine the right-hand side.

 **Example:**  
Same relation: **R(StudentID, CourseID, StudentName, Grade)**

- FD: **(StudentID, CourseID) → StudentName**
- But notice: **StudentID → StudentName** already holds.
- That means `CourseID` was unnecessary.
- So this is a **Partial FD**.

### Easy Way to Remember

- **Full FD:** All LHS attributes are required.
- **Partial FD:** Some attributes in LHS are extra (you can drop them).

 **One-line definitions for notes:**

- **Full FD:** A dependency where every attribute on the LHS is necessary to determine RHS.
- **Partial FD:** A dependency where some attribute(s) on the LHS can be removed without affecting the dependency.


## BCNF
“We must not derive a prime attribute from any prime or non-prime attribute. Note: Trivial dependencies like A → A are allowed.