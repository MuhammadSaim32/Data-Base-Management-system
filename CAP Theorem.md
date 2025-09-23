#  What is CAP Theorem

- CAP theorem applies to **distributed systems** (systems with many servers/nodes working together).
- It says:  
     **You cannot have Consistency, Availability, and Partition Tolerance all at the same time.**
- You can only guarantee **2 out of 3**.
##  The Three Properties

###  (C) Consistency

- All users see the **same data at the same time**.
- Example: If you deposit money in the bank, every ATM should show your new balance.
- Analogy: One **notebook** where sales are written — everyone sees the same numbers.
###  (A) Availability

- The system is **always up** and will always give a response.
- Even if some nodes are down, it still works.
### (P) Partition Tolerance

- The system can **handle network problems** (messages dropped, servers disconnected).
- It does not completely fail when servers cannot talk to each other.
- To achieve this, systems must **replicate data** across nodes.
- Example: WhatsApp Asia servers keep running even if they can’t talk to Europe servers.
- Analogy: If the shop is divided by a wall, both sides keep writing in their notebooks and later sync.

## 3. The Three Possible Combinations

### CA (Consistency + Availability, no Partition Tolerance)

- Works fine as long as there are **no network issues**.
- If a partition happens → system breaks.
- Example: **MySQL / PostgreSQL** in single-node or tightly coupled replication.
### CP (Consistency + Partition Tolerance, no Availability)

- System prefers **correct data** over staying online.
- During partition, some nodes may be **turned off** to avoid inconsistency.
- Example: **MongoDB, HBase, Bigtable.**
- Used in: **Banking systems** (correct balance > always working).
### AP (Availability + Partition Tolerance, no Consistency)

- System prefers **being up** over correct data.
- During partition, nodes keep running but may return **outdated data**.
- Later, they sync (eventual consistency).
- Example: **Cassandra, DynamoDB.**
- Used in: **Social Media, Messaging apps** (better to stay online than perfectly accurate).
- IN Cassandra There is **no single primary node** (unlike MongoDB, which has one primary per replica set).
- All nodes are **equal (peer-to-peer)**.
- **every node can accept reads/writes**, no single leader bottleneck.

## 4. Why Pure CA is “Not Practical”

- Because **network partitions always happen** in real distributed systems.
- CA only works in:
    
    - **Single-node setups** (one server, like local MySQL).
    - Or servers in the same rack with almost zero chance of partition.
#### ==Other ones==

- CAP  ( love baber notes ).
