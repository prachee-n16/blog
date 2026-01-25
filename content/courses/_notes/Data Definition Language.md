**Domain Types**
- `char(n)` --> Fixed length character string, with user-specified length n.  
- `varchar(n)` --> Variable length character string, with user-specified maximum length n.  
- `int.` --> Integer (a machine-dependent finite subset of the integers).  
- `smallint` --> Small integer (a machine-dependent subset of int).  
- `numeric(p,d).` --> Fixed point number, with user-specified precision of p significant digits, with d digits to the right of decimal point. 
- `real, double precision` --> Floating point and double-precision floating point numbers, with machine-dependent precision.  
- `float(n).` --> Floating point number, with user-specified precision of at least n digits.  
- `date, time.` --> Calendar date (YYYY-MM-DD format), and time of day (hh:mm:ss format).  

**Integrity Constraints**
- `not null`: disallows null values  
- `primary key`: ensures uniqueness  
- `unique`: ensures uniqueness (e.g. superkey)
- `foreign key`: defines a foreign key in the child (referencing) table that points to a referenced key in a parent (referenced) table r  
- `default V`: makes `V` the default value for an attribute

