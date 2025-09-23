
# **Partitioning & Sharding in Databases**

## What is Partitioning?

- **Partitioning** = Splitting a large table into **smaller parts (partitions)** for performance, scalability, and manageability.
- Logically still one table, but physically divided.
## Types of Partitioning
### Horizontal Partitioning (Row-based)

- Split by **rows**.
- Each partition has **same columns**, but different sets of rows.
- **Subtypes:**
1. **Range Partitioning**
    - Rows divided by continuous ranges of values.
    - Example: Orders 2020–21, 2022–23, 2024–25.
2. **List Partitioning**
    - Rows divided by categories (predefined values).
    - Example: Customers from Pakistan, India in one partition; USA, Canada in another.
3. **Hash Partitioning**
    - Rows assigned using a hash function for **even distribution**.
    - Example: `user_id % 3` decides which partition/shard a row belongs to.
### Vertical Partitioning (Column-based)

- Split by **columns (attributes)**.
- Each partition has **different columns**, joined by a common key.

Example: Students(id, name, GPA) in one partition; Students(id, address, phone, photo) in another.

**No subtypes** (like range/list/hash).  
Useful when some columns are large (images, blobs) or rarely accessed.
###  Hybrid Partitioning

- Sometimes both **horizontal + vertical** partitioning are combined.  
     Example: Split a "Users" table vertically into (profile info vs. photos), then horizontally shard the profile info by user_id.
    
##  What is Sharding?

- **Sharding = Horizontal Partitioning across multiple servers.**
- Each shard = a partition stored on a different **server/node**.
- Enables **horizontal scaling** (add more servers to handle more data).

##  When to Use What?

- **Vertical Partitioning** → When some columns are huge/rarely used.
- **Horizontal Partitioning** → When rows are too many for one server.
    
    - **Range** → Time-series.
    - **List** → Categorical data.    
    - **Hash** → Balanced load distribution.
- **Sharding** → When one server can’t handle all data or queries.
## Pros & Cons

### Advantages

- Faster queries (less data scanned).
- Better performance & load distribution.
### Disadvantages

- **Complex joins (especially across shards)** → (If data you need is split across multiple shards/partitions, the DB must gather from each and merge, which slows down queries and increases network cost).
- **Range/List → can cause imbalance** → (If most data falls in one range or category, that shard/partition becomes overloaded = hotspot, while others stay idle).
- **Hash → not good for range queries** → (Because hashing scatters rows randomly, finding “IDs between 1–100” means scanning all partitions/shards, not just one).
- **Sharding → adds routing & consistency complexity** → (You need extra logic to know which shard holds which data, and keeping all shards in sync is harder → risk of replication lag, stale reads, or inconsistency).



# What is a Hash Function (Simple Words)

- A **hash function** = a small math formula (or algorithm) that takes an input (like `user_id`) and outputs a number.
- That number decides **which partition/shard** the data should go into.
- You drop `user_id` inside → it spits out a number → you put the row into the corresponding “bucket” (partition/shard).
# Simplest Hash Function → **Modulo (%)**

Formula:

`partition_number = value % N`

Where:

- `value` = column we want to hash (e.g., `user_id`)
- `N` = total number of partitions/shards

 Example: We have **3 shards** (Shard 0, Shard 1, Shard 2).

`partition = user_id % 3`

- If `user_id = 7` → `7 % 3 = 1` → goes to **Shard 1**
- If `user_id = 10` → `10 % 3 = 1` → goes to **Shard 1**
- If `user_id = 14` → `14 % 3 = 2` → goes to **Shard 2**
- If `user_id = 21` → `21 % 3 = 0` → goes to **Shard 0**

 Result: Users are **spread evenly** across shards, not all stuck in one place.
# Real-World Example

Imagine 100,000 users signing up to a website:
- Without hashing → maybe 70% of them are from Asia → Asia server gets overloaded (hotspot).
- With hashing on `user_id` → each new user gets evenly distributed across all servers → no single server is overloaded.

- **Partitioning = inside one server.**
- **Sharding = across multiple servers.**