# Cardinality

In a database relationship, cardinality is the general concept of how many instances of one entity can relate to instances of another, while ==minimum cardinality specifies the lowest number of relationships required (e.g., 0 or 1), and maximum cardinality defines the highest number of relationships possible (e.g., 1 or many)==. For example, a relationship between a Customer and an Order might have a minimum cardinality of 1:1 (each customer must have at least one order), and a maximum cardinality of 1:N (a customer can have many orders), indicating a one-to-many relationship where an order is tied to a single customer.

## Cardinality 

- **General Concept:**
The overall number of instances of one entity that can be associated with instances of another entity in a relational database.

- **Types:**
Cardinality is often expressed as 1:1 (one-to-one), 1:N (one-to-many), or M:N (many-to-many).

## Minimum Cardinality

- **Definition:**    
- The lowest number of times an instance of one entity must participate in a relationship with another entity. 
- **Meaning:**
    It determines if a relationship is optional or mandatory. 
    - **0:** The relationship is optional; an entity instance doesn't have to be involved in the relationship. 
    - **1 or more:** The relationship is mandatory; every instance of the entity must participate in  that   relationships. 
    

## Maximum Cardinality

- **Definition:**
- The highest number of times an instance of one entity can participate in a relationship with another entity. 
- **Meaning:**
	It sets the upper limit for the number of instances involved in the relationship. 
    - **1:** An instance can be related to at most one other instance of the other entity. 
    - **N (Many):** An instance can be related to any number of instances of the other entity. 
Example:customer and Order Relationship

- **Scenario:** A customer can have multiple orders, but each order must be associated with only one customer. 
- **Cardinality:** One-to-many (1:N). 
- **Minimum Cardinality:** 1 (The relationship is mandatory for an order, as it must belong to a customer). 
- **Maximum Cardinality:** N (A customer can have many orders).