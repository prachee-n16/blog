Shape or structure of the [[Database]].
- Physical schema: Design at physical level (storage, file formats, indexes)
	- **Physical Data Independence**: Modifying the physical schema without changing logical schema
	  Ex 1. Adding an index to speed up query retrieval WITHOUT affecting other queries
	  Ex 2. Frequently accessed table is moved to faster disk WITHOUT affecting other queries
- Logical schema: Design at logical level (data types, relations, rows, columns)
	- **Logical Data Independence:** the ability to modify the logical schema without changing the application program.
	  Ex 1. New table or column is added to schema without affecting queries defined over current tables and views

**Structure of a Modern DB** (see logical and physical layers interleaved to form DBMS)
![[Structure of a modern database.png]]

additional notes:
*LAMP*: Linux, Apache, MySQL,PHP is the old web-stack!
