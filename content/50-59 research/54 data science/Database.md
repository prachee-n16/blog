##### Drawbacks of File Systems
Why file systems over DBMS?
- First, file systems lead to data redundancy and inconsistency
	- you could have multiple data formats, and duplication across various files
	- Databases can provide a single, consistent format that uses keys to avoid duplications
- File system cannot answer queries directly
	- SQL solves this problem for databases
- File systems do not enforce integrity
	- If account balances have to be greater than 0, this needs to buried in program code rather than being stated
- Updates in file systems are not atomic
	- if two users try to update a file and a failure occurs, it might leave data in an inconsistent state with partial updates
- File systems offer limited support for concurrent access by multiple users
	- Concurrent access is important for performance
- File systems do not provide sufficient security
	- If there's certain data that should be masked, it will difficult to control this access 
##### Levels of abstraction
There are different layers in the database:
1. Physical level: describes how a record is stored
   It deals with file formats; what encoding am I using for integers? Is it comma-separated or tab-separated?
   e.g. Order by ID, stored in .csv files
2. Logical level: describes the structure of data stored in database and relationship among data
   This independence has to do with fields that an object has; e.g. a professor has an ID, name and department
3. View level: Provides a virtual structure imposed by database designer (access privileges)
   e.g. a student can see an professor's teaching evaluations, but only HR can see their salary
![](https://static.javatpoint.com/dbms/images/data-abstraction-in-dbms2.png)