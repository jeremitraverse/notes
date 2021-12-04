# PARALLEL AND DISTRIBUTED DB

## PARALLEL VS DISTRIBUTED DB
Parallel databases are on the same site but distributed databases aren't on
the same site

## DISTRIBUTED DATABASES
- Pros
  - Get the data closer to the end user to increase query speeds
  - More crash resilient
  - Scalable
- Cons
  - Sync data
  - Make the distribution transparent to the end user
    - Can cause latency
  - Evaluate distributed queries, some need data that might be on different data center

### Architecture
- **Homogeneous DBSM**
  - Multiple database sites that runs the same BDSM
  - Increase the performance & fiability since we have a better coupling between our sites
- **Multi DBSM**
  - Each site is autonomous
  - Helps with the need of having two different SQL dialect
  - Need of specialized queries for each sites
- **Federated DBMS**
  - Makes an interface to interact seamlessly with multiple DBMS 
  - Cons
    - Integretion of certain schema might be hard
    - Can be complicated to reconstruct a view composed from two SQL dialects
    - Can reduce performance

### Distributed data duplication
- Master table that has the information. Master table is duplicated on X tables that are may or may 
  not be on different data center.
- Access to data might be faster
- Redondancy
- Master table must be sync, either in a sync or async way, with the sub tables
- Two types of distributed duplication
  - Synchronous replication
    - Node are guarantee to be serialized
    - Transaction is commited only when all the sites are up to date
  - Asynchronous replication
    - Update is applied to main database
    - Then, in a async way, update the local database

### Distributed data fragmentation
- Master table is divided in X table that are on different data center
  - Horizontal fragmentation
    - Data is fragmented
      - Keep local information (by Country)
  - Vertical fragmentation
    - Columns are fragmented
      - Keep relevent columns per site (by subject)

### Two-phase commit
- First phase
  - Coordonator site ask to site that must participate to the query if they operation was a 
  success.
- Second phase
  - If the coordonator receives yes from all the participants sites, it sends another
  message to the participants sites to commit the changes. If one site doesn't respond,
  the operation is cancelled and we make a rollback.
- Following the atomicity principle (ACID)


### Distributed queries optimization
- Local optimization is made following the principle to reduce the read and writes
  to disk
- Distributed optimization is made following the principle to reduce the amount of 
  site to site calls

### Global optimization without parallelisation
- Optimization is needed when we join tables. With distributed databases, we want to 
  optimize the amount of data that we send from sites to sites.
- Always transfer the smallest db first

#### Half-join strategy 
- First, transfer only the columns, from the biggest table to the other, that are 
  required for the join (PK ...)
- Then transfer the rest of the columns afterward 
- Let's say that we have two tables T1 that holds 100 Actors and T2 that holds 100K 
  MovieRoles. Instead of sending all the MovieRoles to the site that stores T1, we only
  send the data that can be join to the T1 entries.

### Distributed database with Oracle

#### Database Links

- Allows local user to have access to another database without being a user of that DB

#### Synonym
- Can create a synonym to avoid apps to know the data's location
  - Keeps the same request even if the links changes

#### Materialize view
- Used for data duplication
- Handles synchronization between main and local tables

### Parallelisation
- Looking to exploite intrasite parallelism
- Disk and processing unit parallellism

#### Disk parallellism
- **Mirror disks**
  - Duplication data onto multiple disk
    - More crash resilient
- Code detector and error corrector
- Striping
  - Cut down a table and divide the data into different databases

#### Inter-operator parallelism
- Let's say that we have T1 U T2 U T3 U T4
  - We can join in parallel T1 to T2 and T3 to T4 then the two results

#### Parallel table fragmentation 
- Cutting down big table in smaller table
- Largely used in data warehouses
- Allows intra-operation parallelism
- Two types of partitionning
  - **Value based intervals partitionning**
    - Accelerate value and value intervals based selections on the partitionning key
      i.e. transaction year
  - **Key hashing partitionning**
    - i.e primary key hashing
    - Uniforme distribution of the lines in the partitions
    - Only accelerate selections by value on the partitionning key
