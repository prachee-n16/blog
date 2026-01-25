### SELECT
- **Syntax**:
  ```sql
  SELECT column1, column2, ...
  FROM table_name
  WHERE condition;
  ```
- **Description**: Retrieves specific columns from a table based on an optional condition.
- **Example**:
  ```sql
  SELECT name, salary 
  FROM instructor 
  WHERE dept_name = 'Physics';
  ```
- **Notes**: Use `DISTINCT` to remove duplicates, or `*` to select all columns.

---

### WHERE
- **Syntax**:
  ```sql
  SELECT column1, column2, ...
  FROM table_name
  WHERE condition;
  ```
- **Description**: Filters rows based on a specified condition.
- **Example**:
  ```sql
  SELECT name 
  FROM instructor 
  WHERE salary > 50000;
  ```

---

### GROUP BY
- **Syntax**:
  ```sql
  SELECT column_name(s), aggregate_function(column_name)
  FROM table_name
  WHERE condition
  GROUP BY column_name(s);
  ```
- **Description**: Groups rows that have the same values into summary rows, often used with aggregate functions.
- **Example**:
  ```sql
  SELECT dept_name, AVG(salary)
  FROM instructor
  GROUP BY dept_name;
  ```

---

### HAVING
- **Syntax**:
  ```sql
  SELECT column_name(s), aggregate_function(column_name)
  FROM table_name
  GROUP BY column_name(s)
  HAVING condition;
  ```
- **Description**: Filters groups based on a condition, similar to `WHERE` but used after grouping.
- **Example**:
  ```sql
  SELECT dept_name, AVG(salary)
  FROM instructor
  GROUP BY dept_name
  HAVING AVG(salary) > 42000;
  ```

---

### ORDER BY
- **Syntax**:
  ```sql
  SELECT column1, column2, ...
  FROM table_name
  ORDER BY column_name [ASC|DESC];
  ```
- **Description**: Orders the result set by one or more columns in ascending (`ASC`) or descending (`DESC`) order.
- **Example**:
  ```sql
  SELECT name, salary
  FROM instructor
  ORDER BY salary DESC;
  ```

---

### JOIN (INNER JOIN)
- **Syntax**:
  ```sql
  SELECT column_name(s)
  FROM table1
  INNER JOIN table2
  ON table1.column_name = table2.column_name;
  ```
- **Description**: Combines rows from two or more tables based on a related column between them.
- **Example**:
  ```sql
  SELECT instructor.name, teaches.course_id
  FROM instructor
  INNER JOIN teaches
  ON instructor.ID = teaches.ID;
  ```

---

### NATURAL JOIN
- **Syntax**:
  ```sql
  SELECT column_name(s)
  FROM table1
  NATURAL JOIN table2;
  ```
- **Description**: Performs a join based on columns with the same name and automatically eliminates one set of duplicate columns.
- **Example**:
  ```sql
  SELECT *
  FROM instructor
  NATURAL JOIN teaches;
  ```

---

### UNION
- **Syntax**:
  ```sql
  SELECT column_name(s) FROM table1
  UNION
  SELECT column_name(s) FROM table2;
  ```
- **Description**: Combines the result sets of two or more `SELECT` queries, removing duplicates.
- **Example**:
  ```sql
  SELECT course_id FROM section WHERE semester = 'Fall'
  UNION
  SELECT course_id FROM section WHERE semester = 'Spring';
  ```

---

### UNION ALL
- **Syntax**:
  ```sql
  SELECT column_name(s) FROM table1
  UNION ALL
  SELECT column_name(s) FROM table2;
  ```
- **Description**: Combines the result sets of two or more `SELECT` queries, including duplicates.
- **Example**:
  ```sql
  SELECT course_id FROM section WHERE semester = 'Fall'
  UNION ALL
  SELECT course_id FROM section WHERE semester = 'Spring';
  ```

---

### INTERSECT
- **Syntax**:
  ```sql
  SELECT column_name(s) FROM table1
  INTERSECT
  SELECT column_name(s) FROM table2;
  ```
- **Description**: Returns only the rows that are common between the result sets of two or more `SELECT` queries.
- **Example**:
  ```sql
  SELECT course_id FROM section WHERE semester = 'Fall'
  INTERSECT
  SELECT course_id FROM section WHERE semester = 'Spring';
  ```

---

### EXCEPT
- **Syntax**:
  ```sql
  SELECT column_name(s) FROM table1
  EXCEPT
  SELECT column_name(s) FROM table2;
  ```
- **Description**: Returns rows from the first `SELECT` query that are not present in the second `SELECT` query.
- **Example**:
  ```sql
  SELECT course_id FROM section WHERE semester = 'Fall'
  EXCEPT
  SELECT course_id FROM section WHERE semester = 'Spring';
  ```

---

### COUNT
- **Syntax**:
  ```sql
  SELECT COUNT(column_name)
  FROM table_name
  WHERE condition;
  ```
- **Description**: Returns the number of rows that match a specified condition.
- **Example**:
  ```sql
  SELECT COUNT(*)
  FROM instructor;
  ```

---

### AVG
- **Syntax**:
  ```sql
  SELECT AVG(column_name)
  FROM table_name
  WHERE condition;
  ```
- **Description**: Returns the average value of a numeric column.
- **Example**:
  ```sql
  SELECT AVG(salary)
  FROM instructor
  WHERE dept_name = 'Physics';
  ```

---

### SUM
- **Syntax**:
  ```sql
  SELECT SUM(column_name)
  FROM table_name
  WHERE condition;
  ```
- **Description**: Returns the total sum of a numeric column.
- **Example**:
  ```sql
  SELECT SUM(salary)
  FROM instructor
  WHERE dept_name = 'Physics';
  ```

---

### MIN
- **Syntax**:
  ```sql
  SELECT MIN(column_name)
  FROM table_name
  WHERE condition;
  ```
- **Description**: Returns the smallest value of a column.
- **Example**:
  ```sql
  SELECT MIN(salary)
  FROM instructor;
  ```

---

### MAX
- **Syntax**:
  ```sql
  SELECT MAX(column_name)
  FROM table_name
  WHERE condition;
  ```
- **Description**: Returns the largest value of a column.
- **Example**:
  ```sql
  SELECT MAX(salary)
  FROM instructor;
  ```

---

### CREATE TABLE
- **Syntax**:
  ```sql
  CREATE TABLE table_name (
    column1 datatype constraint,
    column2 datatype constraint,
    ...
  );
  ```
- **Description**: Defines a new table with the specified columns, data types, and constraints.
- **Example**:
  ```sql
  CREATE TABLE instructor (
    ID CHAR(5),
    name VARCHAR(20),
    dept_name VARCHAR(20),
    salary NUMERIC(8, 2)
  );
  ```

---

### DROP TABLE
- **Syntax**:
  ```sql
  DROP TABLE table_name;
  ```
- **Description**: Deletes a table and all its data from the database.
- **Example**:
  ```sql
  DROP TABLE student;
  ```

---

### ALTER TABLE
- **Syntax**:
  ```sql
  ALTER TABLE table_name
  ADD column_name datatype;
  
  ALTER TABLE table_name
  DROP column_name;
  ```
- **Description**: Modifies an existing table by adding or dropping columns.
- **Example**:
  ```sql
  ALTER TABLE instructor
  ADD email VARCHAR(50);
  
  ALTER TABLE instructor
  DROP email;
  ```

---

### INSERT INTO
- **Syntax**:
  ```sql
  INSERT INTO table_name (column1, column2, ...)
  VALUES (value1, value2, ...);
  ```
- **Description**: Adds a new row to a table with specified values for the columns.
- **Example**:
  ```sql
  INSERT INTO course
  VALUES ('ECE-356', 'Databases', 'ECE', 0.5);
  ```

---

### UPDATE
- **Syntax**:
  ```sql
  UPDATE table_name
  SET column1 = value1, column2 = value2, ...
  WHERE condition;
  ```
- **Description**: Modifies existing records in a table.
- **Example**:
  ```sql
  UPDATE instructor
  SET salary = salary * 1.03
  WHERE salary < 80000;
  ```

---

### DELETE
- **Syntax**:
  ```sql
  DELETE FROM table_name
  WHERE condition;
  ```
- **Description**: Removes rows from a table that match a given condition.
- **Example**:
  ```sql
  DELETE FROM instructor
  WHERE dept_name = 'Math';
  ```

---

### INNER JOIN
- **Syntax**:
  ```sql
  SELECT columns
  FROM table1
  INNER JOIN table2
  ON table1.column = table2.column;
  ```
- **Description**: Combines rows from two tables based on a related column.
- **Example**:
  ```sql
  SELECT course.course_id, prereq.prereq_id
  FROM course
  INNER JOIN prereq
  ON course.course_id = prereq.course_id;
  ```

---

### OUTER JOIN
- **Syntax**:
  ```sql
  SELECT columns
  FROM table1
  LEFT/RIGHT/FULL OUTER JOIN table2
  ON table1.column = table2.column;
  ```
- **Description**: Combines rows from two tables, including non-matching rows from one or both tables.
- **Example**:
  ```sql
  SELECT *
  FROM course
  LEFT OUTER JOIN prereq
  ON course.course_id = prereq.course_id;
  ```

---

### CREATE VIEW
- **Syntax**:
  ```sql
  CREATE VIEW view_name AS
  SELECT columns
  FROM table_name
  WHERE condition;
  ```
- **Description**: Defines a virtual table based on a SQL query.
- **Example**:
  ```sql
  CREATE VIEW faculty AS
  SELECT ID, name, dept_name
  FROM instructor;
  ```

---

### AUTO-INCREMENT
- **Syntax**:
  ```sql
  CREATE TABLE table_name (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    column2 datatype,
    ...
  );
  ```
- **Description**: Automatically generates a unique value for a primary key field.
- **Example**:
  ```sql
  CREATE TABLE instructor_auto (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(20),
    dept_name VARCHAR(20),
    salary NUMERIC(8,2)
  );
  ```

---

### STORED PROCEDURE
- **Syntax**:
  ```sql
  DELIMITER $$
  CREATE PROCEDURE procedure_name (parameters)
  BEGIN
    SQL statements;
  END $$
  ```
- **Description**: A stored procedure is a subroutine available to applications that access a relational database.
- **Example**:
  ```sql
  DELIMITER $$
  CREATE PROCEDURE ProcTopSalary(IN dept_name VARCHAR(20))
  BEGIN
    SELECT MAX(salary) FROM instructor
    WHERE instructor.dept_name = dept_name;
  END $$
  ```

---

### TRIGGER
- **Syntax**:
  ```sql
  CREATE TRIGGER trigger_name
  BEFORE/AFTER INSERT/UPDATE/DELETE
  ON table_name
  FOR EACH ROW
  BEGIN
    SQL statements;
  END;
  ```
- **Description**: A trigger is a stored procedure that is automatically executed when an event occurs in the database.
- **Example**:
  ```sql
  CREATE TRIGGER SalaryTrigger
  BEFORE UPDATE ON instructor
  FOR EACH ROW
  BEGIN
    IF NEW.salary > OLD.salary * 1.10 THEN
      SIGNAL SQLSTATE '45000'
      SET MESSAGE_TEXT = 'increase higher than 10%';
    END IF;
  END;
  ```