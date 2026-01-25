Redundancy in a database leads to:
1. Update anomalies: a repeated value may be changed in one place but not in another place
2. Insertion anomalies: in order to insert one value, it becomes necessary to insert some unrelated value.
3. Deletion anomalies: deleting one type of information leads to the loss of an another unrelated type of information

*Motivation*

| Pros                                                                                                          | Cons                                           |
| ------------------------------------------------------------------------------------------------------------- | ---------------------------------------------- |
| computation and memory/storage becoming less expensive                                                        | additional processing needed to compute joins  |
| joins and referential integrity checks can be quite fast  <br>(e.g., if tables are small or indexes are used) | additional space needed for tables and indexes |
| dealing with anomalies may require  <br>human intervention, which is slow and costly                          | must enforce referential integrity constraints |

There are two forms of "repetition" of data:
- The value domains of some attributes are not atomic. One value might encode multiple pieces of information.
- Attribute values in different tuples are related by [[Functional Dependencies]]: one subset of attributes functionally determines the values of another subset.

The solution is to:
1. Break up value domains to create atomic domains as in [[1NF]]
2. Decompose relations to avoid specific types of FDs.
