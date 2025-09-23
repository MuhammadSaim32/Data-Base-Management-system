# Associative Entity

An associative entity (or bridge entity or intersection entity ) is ==a special type of entity used in relational databases and entity-relationship (ER) diagrams to handle many-to-many relationships between other entities, particularly when the relationship itself has attributes or a distinct meaning==. It acts as a linking table, storing a composite primary key derived from the primary keys of the entities it connects, along with any specific attributes of the relationship, such as a date or description. 

### When to Use

- **M:N relationships cannot be directly stored** in RDBMS (violates 1NF).
- When the **relationship has its own attributes** (e.g., date, grade, quantity

Example

Consider a many-to-many relationship between `Students` and `Courses`: 

- **Entities:** `Student` and `Course`. 

- **Many-to-Many Relationship:** A student can take many courses, and a course can have many students. 

- **Problem:** You want to track the enrollment date for each student in each course. The enrollment date is an attribute of the relationship between `Student` and `Course`, not just the student or the course alone. 

- **Solution:** Introduce an associative entity called `Enrollment`. 
    
    - The `Enrollment` entity would have a composite primary key made up of the `StudentID` and `CourseID`. 
    
    - It would also store the `EnrollmentDate` and other relevant details. 

#### ==Other ones==

- it series dbms (3rd edition ).
- ER diagram only from above references it series.