**Lecture 09: Storage and File Structures** 
The key properties of storage media are:
- **speed** with which data can be accessed
- **cost** of storing data
- **capacity** of storage media (raw vs. usable)
- **density**
- **volatility**
- **reliability** 

> [!faq]- **Key Metrics** for storage media
> - **Speed** with which data can be accessed
>	- **Latency per I/O operation (IOP)**: lower latency means faster response times when accessing data
>	- **Throughput**: amount of data that can be transferred per unit of time; **overall speed** of the storage system in accessing bulk data
>	- **Reads vs. Writes**: reads are faster than writes because writing involves additional steps, like ensuring data integrity
>	- **Sequential vs. Random Access:**
> 		- Sequential access reads or writes data in a contiguous block (e.g., reading a whole file in order). It's faster because data is accessed continuously without seeking.
> 		- Random access involves reading or writing data at arbitrary locations, which takes longer due to additional time needed to locate each piece of data.
> 	- **Empty vs. Full**:
> 		- Storage devices may operate **faster when they are empty** or have plenty of free space because there's less fragmentation, leading to more efficient access.
> 		- When storage is **nearly full**, performance can degrade as the system may need to search for free blocks or deal with fragmentation, increasing access times.
> - Cost (e.g., $ per GB, Joules per bit stored or accessed) 
> - Capacity (raw vs. usable) 
> - Density (e.g., bits per square inch) 
> - Volatility 
> 	- Volatile media: loses content when power is switched off E.g., CPU registers, cache memory, main memory 
> 	- Non-volatile media: content persists when power is switched off E.g., hard drives (HD), solid-state drives (SSD), battery-backed memory 
> - Reliability 
> 	- Mean time between failures (MTBF): measure of how reliable a storage device is.; represents the average time (usually in hours or years) that a storage device is expected to operate without failing.
> 	- Number of write cycles until wear-out: total number of times data can be written to a storage device before it starts to degrade and fail.

The important forms of **physical storage media** and some key points about them:
- CPU Registers and Cache 
	- **volatile**, SRAM-based, managed by processor with small capacity size for L1/L2/L3 cache
- Main memory
	- **volatile**, SDRAM-based, managed by OS or application with low latency and higher capacity (enough to store a database)
- Flash Memory
	- Used in SSD and USB drives with low latency (10-100 $\micro s$) and larger capacities (100 GB to 1 TB)
		- The drawback of this technology is:
			- cells must be erased before they can be re-written
			- cells can wear out after 10K - 1M write/erase cycles
		- The solution is to introduce a flash translation layer which remaps logical addresses to physical addresses to mask erase latency and work out pages; perform wear levelling and sparing to increase longevity
- Conventional (magnetic) hard disk
	- mature technology that is less expensive than flash and the most popular medium for **reliable long-term storage of data**
		- much slower for random I/O than for sequential I/O
		- susceptible to mechanical vibrations and shocks
		- Latency is in order of a few ms, capacities in order of hundred GB's up to several TB's
- Optical Disks (CD, DVD, BlueRay)
	- Least expensive, mostly read-only
		- Latency on the order of 100ms, capacities up to 100GB
		- used to store DBMS binaries and data sets, record backups

![[storage_hierarchy.png|500]]

> [!Error] Understand HDD Internals (sparse notes in [[part09 - Storage.pdf|Lecture 9]])

**Cache, main memory and flash memory** use solid state technology; More on SSD Internals:
- Like a magnetic hard disk, SDD provide "sector" read and write ops to a file system
	- Internally, SSD maps "sectors" to "pages" i.e. logical -> physical mappings
- SSD can write 1 page at a time with a caveat: 
	- Once written, a page can not be directly overwritten; instead, it has to erase the entire block of pages and rewritten 
	- Erasing a block is MUCH slower than read/write page op; also, overwriting the same flash cell repeatedly leads to wear-out
	- FTL, **flash translation layer**: remaps pages and blocks to enable efficient overwriting and wear levelling

> [!note] Conventional Block I/O Devices
> Secondary storage devices like magnetic/optical disk are block devices
> - Block is a contiguous sequence of sectors from a single track
> 	- It represents a unit of storage alloc and data transfer
> - Block sizes range from 512 bytes to few Kb's
> 	- Block size is key; 
> 		- ==too small and there are more transfers from disk?==
> 		- too large and there is wasted space due to partial filled blocks (think internal fragmentation)

The most important topic is **RAID** i.e. Redundant Arrays of Inexpensive/Independent Disks
- A disk organization technique where multiple physical disks provide the illusion of a single reliable + performant disk

There are two improvements with RAID:
1. Improvement in **reliability** through **redundancy**
	- **Redundancy** -> We store extra information which can be used to rebuild any information lost in case of failure
	- There are two ways to integrate redundancy:
		- **mirroring**: duplicate every disk
			- One "logical" disk is tied to two physical disks. 
			- We write information to both disks, but perform reads from either disk; If there's a failure in one, data will be available on other;
				- True data loss = both disks fail (but this is a low probability scenario)
		- **parity bits**: store additional bits that can detect and correct errors
	- **Reliability**; we can measure how (in)frequently failures occur to measure how reliable it is
		- **mean time to data loss**: depends on MBTF and mean time to repair
			- **QUESTION:** Given MTBF of 100,000 hours, mean time to repair of 10 hours, 
			  mean time to data loss of $500*10^6$ hours (or $57,000$ years) for a mirrored pair of disks (assuming independent failures)

> [!note] Why have redundancy?
> > "reliability through redundancy, ensuring survival of data if a (small enough) subset of disks fails"
> 
> As we add more disks in parallel to work together, the chance of one component out of these N disks failing is **greater than** the chance of one disk failing.
> - **QUESTION:** a system with 100 disks, each with a mean time between failures (MTBF) of 100,000 hours (approx. 11 years), will have a system MTBF of 1000 hours (approx. 42 days)

 2. Improvement in **performance** through **parallelism**
	- Parallelism has two goals in disk systems:
		- Increase **throughput** by distributing small I/O requests across multiple disks
		- Reduce **response time** by parallelizing large I/O requests
	- There are two techniques for parallelizing I/O:
		- **striping**: Write data across multiple disks to improve throughputs 
			- **block-level striping**: with n disks, block $i$ of a file goes to disk number $(i \text{ mod } n) + 1$ 
				- requests for different blocks run in parallel if blocks are in different disks
				- request for long sequence of blocks can use all disks in parallel

> [!note] Key Terms in RAID
> Storage:
> - Raw capacity: total amount of physical storage in RAID
> - Effective/usable capacity: how much "application" data can be stored in RAID (redundancy eats up space from raw capacity)
> 
> Performance
> - IOPS (I/O operations per second): how many small random read/writes can RAID perform in 1s
> 	- Raw IOPS: how many small reads/writes are actually performed on disks using RAID
> - Throughput: how many bytes/s can be read/write from RAID
> 	- Higher for sequential I/O, compared to random

**RAID Levels**: schemes for providing redundancy at lower cost using disk striping with mirroring/parity bits
1. RAID Level 1+0 | **RAID 10**: mirrored disks with block striping
	- There are two copies of all data which is relatively expensive to maintain that level of redundancy
		- It has the best write performance (i.e good for update-heavy workloads) and supports reading in parallel from both mirrors
	- When mirror fails, recovery is simple: copy from mirror
	- Example of RAID 10 Read/Write in Slide 17/18
2. RAID Level 5 | **RAID 5**: block-interleaved distributed parity
	- Partitions data and parity among $N+1$ disks where $N \geq 2$ 
		- Example: With 5 disks, parity block for $\text{n}^\text{th}$ set of blocks is on disk $\text{(n mod 5) + 1}$; data blocks on other 4 blocks
	- Recovery is slower than RAID 10; read $N$ remaining disks
	- More cost effective; good for reads and large writes; ==small writes pay a penalty since they must read-modify-write data to update parity==
	- Example of RAID 5 Read/Write in Slide 20/21

**File Structures**
> [!note] Key Terms
> - Database is a collection of **files** (representing relations) (DB has many tables)
> - File is a sequence of **records** (representing tuples) (Tables have many relation instances)
> 	- Also called pages; just a sequence of blocks on I/O block device
> - Record is a sequence of **fields** (representing attributes) (Relation instances have many columns)

Case I. Fixed Length Record
- Assume record size is fixed (so, each entry in table takes fixed space)
- Each file has records of one type (all entries in tables follow a single relation schema)
- Different files are used for different relations

The approach to perform CRUD operations:
- Store record $i$ from byte $\text{n * (i - 1)}$ where n = size of record
	- Access records with same procedure; don't let record sizes be larger than $n$
- If we want to delete record $i$, the wrong way to do it is:
	- Shift records up to claim free space (expensive)
	- Move record n to i; last record saved to freed position (destroys sort order)
- Instead, link all free records in a **free list**
	- ==Store the address of the first deleted record in the file header.==
	- ==The i-th deleted record records a pointer to the (i+1)-st deleted record.==

Case II. Variable Length Record
- Record size is "variable" because:
	- storing multiple record types in a file
	- record types that allow variable lengths for one or more fields
	- record types that allow repeating fields
- Attributes have a fixed order; variable length attributes maintain a offset, length; then have the actual data  stored after fixed length attributes;
	- Null values: 000 (null bitmap)
- Slotted page structure
	- **organize records in a block** by keeping track of header with
		- number of record entries
		- end of free space in block
		- location and size of record
	- Pointers point to the entry for the record in header;
	- Records can be moved around as long as header information is updated

When tracking records in files, there are three organization methods:
- Heap
	- record can be stored anywhere in the file where there is space
- Sequential
	- store records **sequentially**, based on value of **search key of record**
		- deletion uses "pointer chains"
		- insertion requires to locate the position where record can be inserted
			- if there is free space, insert there
			- if no free space, record in overflow block
			- update pointer chain?
		- reorganize file to restore sequential order??
- Index-organized table
	- records are stored using dictionary structure e.g. hash map (unordered), B-tree (ordered)
- Multi-table Clustering File Organization
	- records of several different relations stored in the same file; this allows related records to be stored on same block and minimizes I/O costs

> [!tip]- Data Dictionary Storage
> Stores metadata such as:
> - relations
> 	- names
> 	- names, types and lengths of attr.
> 	- names, definitions of views
> 	- integrity constraints
> - user and accounting info.
> - statistical + descriptive data
> - physical file org. info

> [!note] Storage Access
> Recall, file is partitioned into fixed-size units called blocks (units of storage allocation + data transfer). To reduce \#block transfers from disk to memory, store max. blocks in main memory
> - Buffer: portion of main memory available to store copies of disk blocks
> - Buffer pool: collection of buffers used by database
> - Buffer pool manager: ==subsystem responsible for allocating buffer space in main memory, loading blocks from disk into the buffer pool, evicting blocks as needed to create space in the buffer pool, and writing back dirty (i.e., modified) blocks to disk. Similar to virtual memory manager (VMM) but optimized specifically for the database (e.g., in terms of eviction policy).==

**Lecture 10: Indexing and Hashing**
*Motivation*
- A query will return a subset of records in database
	- point query: search over a specified attribute value
	- range query: search over a range of attribute values
- simple file structures have a weakness
	- hash table
		- while insertion is quick, search requires a scan
	- sequential
		- binary search can be performed over single attribute value
			- however, still might require random I/O
		- all other queries need a scan
		- use of overflow blocks also degrade performance
- index is a data structure that speeds up lookup of records by specific search keys
	- performance is boosted two ways!
		- organize data in ways that benefit specific queries
		- smaller than data files they refer to
			- buffer pool manager is stored in memory to avoid expensive I/O operations
			- even on disk, search performed using few I/O operations

> [!note]- How to design the physical schema?
> - Assume there is a logical schema
> - Choose a structure that is: index-structured, heap, sequential
> - We add indices for:
>	- queries that use "WHERE" clause
>	- queries that use "JOIN" clause
>- Choose index type: hash or B+ tree

**Key Terms**
- Search key: an attribute or a set of attributes used to look up records
- Index: collection of records called **index entries** of the form ![](https://cdn.hackernoon.com/images/-ku93pfu.png)
	- **hash index**: search keys that are distributed nearly uniformly across buckets using a hash function
	- **ordered index**: search keys that are stored in sorted order 
		- index-sequential file: ordered-sequential file + primary index
		- primary index: index whose search key aligns with sorted order
			- also known as clustered index
			- search key usually equals to primary key
		- secondary index: index whose search key has a different order than sequential order
			- also known an non-clustered index

> [!note] Primary vs. Secondary Index
> - indices enable faster search
> - updating indices incurs overhead 
> 	- after modifications, update all index on table
> - sequential scan with primary index is efficient if there are few overflow blocks
> - sequential scan with secondary index is expensive because each record access may need a new block from disk

- **Dense index**: one index record for every values of the search key in the file
- **Sparse index:** contains index records for some values of the search key in the file
	- Sparse index uses **less space** and **less maintenance overhead** for insertions and deletions
	- Sparse index are slower for locating individual records

**B+ trees** are an alternative to index-sequential file. **Motivation** -
- With index-sequential file, there is a **degradation problem** where searching becomes expensive due to overflow blocks
	- so, file need to be reorganized periodically
- the advantage of B+ tree index files is it reorganizes itself with small, local changes during insertions and deletions
- the disadvantage is computation and space overheads;

B+ trees have the following properties:
- all paths from root to leaf have equal length
- large branching factor means a shallow height
	- with $K$ key-data pairs and $n$ child pointers per internal node, $\text{height} \geq log_{n/2}(K)$ 
	- insertions and deletions run in time proportional to height
	- internal levels easily buffered in main memory, so B+ tree operations need one random I/O
- each node that is "not a root" is at least half full
- internal nodes only store **separator keys** and **pointers** to other nodes
	- keys are "variable length strings" so we can use **prefix compression**
		- save space by storing only the necessary part of a key;
- all data values are stored in leaf nodes which are chained together using sibling pointers
- data values are "pointers" to records in a file (represented as record numbers, or values of primary key)
	- nodes that are close together logically may not be together physically
		- tree traversals may require random I/O's
		- in-order walk through leaf nodes of B+ tree can be slower than scanning a sequential file

> [!note] Index-organized tables
> Index stores the rows of the table rather than pointers to the rows; 
> - pros: avoid having to traverse a pointer from the index to the file when performing a row lookup by primary key
> - cons: full traversal of the index structure need a scan of the entire table which may need more random I/O's than scanning a sequential file
>   
>   See **InnoDB**.

**See example on Multiple-key indices**.

**Lecture 11: Query Processing and Optimization**
Query processing involves the following steps:
1. Parsing and translation 
2. Optimization
	- equivalent relational algebra expressions for the query
	- possible evaluation plans for each candidate RA expression
	- cost of each candidate evaluation plan
3. Evaluation
   - evaluation plan is an **annotated expression** that specifies the detailed evaluation strategy for a given query

![500](https://images.javatpoint.com/dbms/images/query-processing-in-dbms.png)

> [!note] Engineer's Dilemma
> - Adding indexes can speed up some queries drastically
> - However, indexing slows down insertions and updates;
> 	- Looking up an index repeatedly during join is not faster than scanning inner relation
> 	- DBMS might create most important index automatically 
> 	- difficult to outsmart a good query optimizer, which has access to detailed statistics about tables

**Index extension** is when DBMS automatically appends the primary key to each secondary index entry
- Advantage: 
	- possible to physically relocate table rows without having to update all secondary indexes
	- efficient evaluation of queries that refer to both primary key and non-key attributes
		- **Covered query**: a query that can be evaluated using indexes only, without accessing the tables.  
		- **Covering index** (with respect to a covered query): an index that is used to evaluate the covered query.
- Disadvantage:
	- retrieve a record with additional primary index lookup
	- secondary index becomes larger and less likely to remain buffered in main memory
		- the smaller the index, the more likely it is to remain buffered in main memory and lower cost of accessing that index
		- to reduce the size of index:
			- technique 1: shorten the primary key; create a shorter fixed-length surrogate key by adding an auto-increment ID attribute
			- technique 2: index only a prefix of a column


