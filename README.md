# 1. Tables and Data Types
# 1.1 What is a Table?
- A table = Rows + Columns
- Column → Attribute (Name, Age)
- Row → Record (One student data)
- ```js
    | student_id | name | age | course | fees  |
    | ---------- | ---- | --- | ------ | ----- |
    | 101        | Ravi | 20  | CSE    | 50000 |
    | 102        | Anu  | 21  | ECE    | 45000 |

# 1.2 Data Types
- Data type defines what type of data a column can store.
- ```js
    | Data Type | Used For             | Example          |
    | --------- | -------------------- | ---------------- |
    | INT       | Integer numbers      | 10, 25           |
    | DECIMAL   | Decimal numbers      | 10.5             |
    | VARCHAR   | Variable length text | Name             |
    | CHAR      | Fixed length text    | Gender           |
    | DATE      | Date                 | 2026-03-29       |
    | TIMESTAMP | Date + Time          | 2026-03-29 10:30 |
    | BOOLEAN   | True/False           | 1/0              |

# 1.3 Create Table Syntax
- ```js
    CREATE TABLE table_name (
        column1 datatype,
        column2 datatype,
        column3 datatype
    );
    example:
    CREATE TABLE students (
        student_id INT,
        name VARCHAR(50),
        age INT,
        course VARCHAR(20),
        fees DECIMAL(10,2),//total allowed digits are 10(before and after decimal) and 2 digits after the decimal
        admission_date DATE
    );

# 1.4 Insert Data Into Table
- ```js
    // for single row insertion.
    INSERT INTO students
    VALUES (101, 'Ravi', 20, 'CSE', 50000, '2026-03-29');
    // for multiple row insertion.
    INSERT INTO students VALUES
    (102, 'Anu', 21, 'ECE', 45000, '2026-03-20'),
    (103, 'Rahul', 22, 'EEE', 40000, '2026-03-15');

# 1.5 Select Table Data
- ```js
    SELECT * FROM students;

# 2. SELECT Statement
- SELECT is used to retrieve data from a table.
- ex :You have a students table with 10,000 students.
- You want:
- All students
- Only names
- Only CSE students
- Students with fees > 50000
- All this is done using SELECT.

# 2.2 Basic Syntax
- ```js
    // selecting specific columns
    SELECT column1, column2
    FROM table_name;

    // Select all columns
    SELECT * FROM table_name;

# 2.3 Rename Column in Output 
- ```js  
    SELECT column_name AS new_name
    FROM table_name;

# 2.5 Arithmetic Operations in SELECT
- we can use (+,-,*,/)
- ```js
    //Examples
    1.SELECT name, fees, fees + 1000 AS new_fees
    FROM students;

    2.SELECT name, salary, salary * 12 AS annual_salary
    FROM employees;

    //constant column
    3.SELECT name, salary,10000 AS bonus
    FROM employees;

# very important - Order of SQL Execution
- SQL does not execute in the order you write.
- Actual Order:
- ```js
    1.FROM/JOIN
    2.WHERE
    3.GROUP BY
    4.HAVING
    5.SELECT
    6.ORDER BY
- example :
- ```js
    When you write:
    SELECT name
    FROM students
    WHERE age > 20;

    SQL internally executes:
    FROM
    WHERE
    SELECT

# 3.WHERE Clause
- WHERE is used to filter rows (records) based on a condition.
- conditions like:
- Fees greater than 50000,Age less than 21......
- Syntax & Examples:
- ```js
    SELECT column1, column2
    FROM table_name
    WHERE condition;
    //examples
    SELECT name, fees
    FROM students
    WHERE fees > 50000;

    SELECT * 
    FROM students
    WHERE course = 'CSE';

    SELECT name, fees
    FROM students
    WHERE fees + 5000 > 55000;

# 3.1 Comparison Operators (Used in WHERE)
- ```js
    | Operator | Meaning            |
    | -------- | ------------------ |
    | =        | Equal              |
    | != or <> | Not equal          |
    | >        | Greater than       |
    | <        | Less than          |
    | >=       | Greater than equal |
    | <=       | Less than equal    |

# Short Summary
- ```js
    | Clause | Purpose        |
    | ------ | -------------- |
    | SELECT | Choose columns |
    | FROM   | Choose table   |
    | WHERE  | Filter rows    |

# 4. SQL Operators
- SQL operators are used in WHERE clause to apply conditions and perform calculations.
- Types of SQL Operators
- 1.Arithmetic Operators
- 2.Comparison Operators
- 3.Logical Operators
- 4.Special Operators (IN, BETWEEN, LIKE, IS NULL)

# 4.1 Arithmetic Operators
- Used to perform mathematical calculations(+,-,*,/).
- ```js
    //examples:
    SELECT name, salary, salary * 12 AS annual_salary
    FROM employees;

    SELECT name, salary + 5000 AS new_salary
    FROM employees;

# 4.2 Comparison Operators
- Used to compare values in WHERE clause.
- operators are in 3.1 section
- ```js 
    //example:
    //Employees with salary > 40000
    SELECT *
    FROM employees
    WHERE salary > 40000;

    //Employees not in CSE department
    SELECT *
    FROM employees
    WHERE dept <> 'CSE';

# 4.3 Logical Operators
- Used to combine multiple conditions.
- Operators:
- ```js
    | Operator | Meaning              |
    | -------- | -------------------- |
    | AND      | Both conditions true |
    | OR       | At least one true    |
    | NOT      | Reverse condition    |
- examples:
- ```js
    // CSE students with fees > 50000
    SELECT *
    FROM students
    WHERE course = 'CSE' AND fees > 50000;

    // Students from CSE or ECE
    SELECT *
    FROM students
    WHERE course = 'CSE' OR course = 'ECE';

    // Students not from CSE
    SELECT *
    FROM students
    WHERE NOT course = 'CSE';
    
    SELECT *
    FROM employees
    WHERE dept <> 'CSE';

# 4.4 Special Operators (Very Important)
- 1. IN Operator : Used instead of multiple OR conditions.
- 2. BETWEEN Operator : Used for ranges.
- 3. LIKE Operator : Used for pattern matching.
- ```js
    | Symbol | Meaning                  |
    | ------ | ------------------------ |
    | %      | Any number of characters |
    | _      | One character            |

- 4.IS NULL Operator : Used to check NULL values.
- Examples:
- ```js
    // IN operator.
    SELECT *
    FROM students
    WHERE course IN ('CSE', 'ECE', 'EEE');
    //(instead of)
    WHERE course='CSE' OR course='ECE' OR course='EEE'

    // BETWEEN operator.
    SELECT *
    FROM students
    WHERE fees BETWEEN 40000 AND 50000;

    //LIKE operator.
    1.Names starting with R
    SELECT *
    FROM students
    WHERE name LIKE 'R%';

    2.Names ending with a
    SELECT *
    FROM students
    WHERE name LIKE '%a';
    
    3.Second letter = a
    SELECT *
    FROM students
    WHERE name LIKE '_a%';

    4.Name contains letter 'a'
    SELECT *
    FROM students
    WHERE name LIKE '%a%';

    //IS NULL operator
    SELECT *
    FROM students
    WHERE fees IS NULL;

    SELECT *
    FROM students
    WHERE fees IS NOT NULL;

# SUMMARY TABLE
- ```js
    | ------------- | ----------------------- |
    | Operator Type | Operators               |
    | Arithmetic    | + - * /                 |
    | Comparison    | = > < >= <= <>          |
    | Logical       | AND OR NOT              |
    | Special       | IN BETWEEN LIKE IS NULL |

# 5. ORDER BY Clause (Sorting Data)
- ORDER BY is used to sort the result set in ascending or descending order.
- example Scenario:Show employees sorted by salary,Show students sorted by marks.
- Synatax & Examples:
- ```js
    //syntax
    SELECT column1, column2
    FROM table_name
    ORDER BY column_name ASC | DESC;

    //examples
    SELECT * 
    FROM employees
    ORDER BY salary ASC;

    //Order By Multiple Columns
    SELECT *
    FROM employees
    ORDER BY dept ASC, salary DESC;//First sort by dept then sort by salary.

    //Order By with WHERE ;
    SELECT name, salary
    FROM employees
    WHERE salary > 30000
    ORDER BY salary DESC;

# 6.Single Row Functions
- These functions operate on each row individually and return one result per row.

# 6.1 Types of Single Row Functions
- String Functions
- Number Functions
- Date Functions
- Conversion Functions

# 6.2 String Functions
- Used to manipulate text.
- Common String Functions:
- ```js
    | Function               | Description            |
    | ---------------------- | ---------------------- |
    | UPPER()                | Convert to uppercase   |
    | LOWER()                | Convert to lowercase   |
    | LENGTH()               | Length of string       |
    | SUBSTRING() / SUBSTR() | Extract part of string |
    | CONCAT()               | Combine strings        |
    | TRIM()                 | Remove spaces          |

    // concat()=> CONCAT(string1, string2, ...)
    example : 
    SELECT CONCAT(name, ' is enrolled in ', course) AS  enrollment_details 
    FROM students;

  SELECT customer_id,
       first_name || ' age is ' || age AS cust_with_age
FROM Customers;

    //SUBSTRING() / SUBSTR() => SUBSTRING(string, start_position, length).(index starts with 1)
    example:
    SELECT SUBSTRING('SQLDeveloper', 1, 3);
    //Result: 'SQL'

    //TRIM() => TRIM(string);

# 6.3 Number Functions
- ```js
    | Function           | Description          |
    | ------------------ | -------------------- |
    | ROUND()            | Round value          |
    | CEIL() / CEILING() | Next highest integer |
    | FLOOR()            | Lower integer        |
    | ABS()              | Absolute value       |
    | MOD()              | Remainder            |

# 6.4 Date Functions
- ```js
    | Function   | Description         |
    | ---------- | ------------------- |
    | NOW()      | Current date & time |
    | CURDATE()  | Current date        |
    | DATE_ADD() | Add days            |
    | DATE_SUB() | Subtract days       |
    | DATEDIFF() | Difference between dates|

# 6.5 Conversion Functions
- Used to convert data types.
- ```js
    | Function  | Description      | syntax                                 |
    | --------- | ---------------- |-------------------------------------   |
    | CAST()    | Convert datatype | CAST(expression AS data_type)          |
    | CONVERT() | Convert datatype | CONVERT(data_type, expression, [style])|
    // examples:
    -- Using CAST
    SELECT CAST(10.65 AS INT) AS Result; -- Output: 10

    -- Using CONVERT
    SELECT CONVERT(INT, 10.65) AS Result; -- Output: 10

    -- Using CONVERT with Style 103 (UK Format: dd/mm/yyyy)
    SELECT CONVERT(VARCHAR, GETDATE(), 103) AS UK_Format;

- convert is used when we want to convert the date into any other country format (like us dd/mm/yyyy or uk mm/dd/yyyy).
- In all other cases we prefer the cast funtion.

# 7. Aggregate Functions
- Aggregate functions perform calculations on multiple rows and return a single value.
- examples : Total salary of employees,Average marks of students.

# 7.1 Types of Aggregate Functions
- ```js
    | Function | Description    |
    | -------- | -------------- |
    | COUNT()  | Number of rows |
    | SUM()    | Total value    |
    | AVG()    | Average value  |
    | MAX()    | Maximum value  |
    | MIN()    | Minimum value  |

    // examples :
    SELECT COUNT(*) FROM employees; //Counts number of rows.
    SELECT COUNT(salary) FROM employees; // specific column count excluding null values.
    SELECT SUM(salary) FROM employees; // adds values of salary column.
    SELECT AVG(salary) FROM employees; // finds average.
    SELECT MAX(salary) FROM employees;
    SELECT MIN(salary) FROM employees;

- Difference between COUNT(*) and COUNT(column)
- COUNT(*) → counts all rows
- COUNT(column) → ignores NULL
- ``` js
    // where with aggregate.
    SELECT AVG(salary)
    FROM employees
    WHERE salary > 30000;

    // multiple aggregate.
    SELECT SUM(salary), AVG(salary)
    FROM employees;

    // common mistake : Error because mixing aggregate + normal column
    SELECT name, SUM(salary)
    FROM employees;

# 8.GROUP BY Clause
- GROUP BY is used to group rows that have the same values into summary rows.
- It is always used with Aggregate Functions.
- SYNTAX :
- ```js
    SELECT column, AGG_FUNCTION(column)
    FROM table_name
    GROUP BY column;
- Every column in SELECT must be in Either in GROUP BY Or inside aggregate function.Because mixing of aggregate with normal column will cause error.
- EXAMPLE:
- ```js
    // Employee data table.
    | name  | dept | salary |
    | ----- | ---- | ------ |
    | Ravi  | IT   | 30000  |
    | Anu   | HR   | 40000  |
    | Rahul | IT   | 50000  |
    | Sita  | HR   | 35000  |
    //questions
    1.Total salary per department.
    SELECT dept, SUM(salary) AS total_salary
    FROM employees
    GROUP BY dept;

    2.Average salary per department.
    SELECT dept, AVG(salary) AS average_salary
    FROM employees
    GROUP BY dept;

    3.Number of employees per department.
    SELECT dept, COUNT(*) AS number_of_employees
    FROM employees
    GROUP BY dept;

    4.Average salary per department where salary > 30000
    SELECT dept, AVG(salary)
    FROM employees
    WHERE salary > 30000
    GROUP BY dept;

# 9.HAVING Clause
- HAVING is used to filter groups (not individual rows).
- WHERE filters rows,HAVING filters groups
- Syntax & example scenario:
- ```js
    //syntax:
    SELECT column, AGG_FUNCTION(column)
    FROM table_name
    GROUP BY column
    HAVING condition;

    //example:
    refer to the above employee table.
    Q.Show only departments where total salary > 70000?
    - This is done by using "HAVING"
    SELECT dept, sum(salary)
    FROM employee
    GROUP BY dept
    HAVING sum(salary)>7000;

    //HAVING without GROUP BY
    SELECT COUNT(*) AS TotalEmployees
    FROM Employees
    HAVING COUNT(*) > 100;
    // Here, the entire Employees table is one group.
    //HAVING checks if the total employee count exceeds 100.

# 10. JOINS
- JOIN is used to combine data from multiple tables based on a related column.
- example scenerio:
- ```js
    // we have 2 tables
    1.Employees.
    | emp_id | name  | dept_id |
    | ------ | ----- | ------- |
    | 1      | Ravi  | 101     |
    | 2      | Anu   | 102     |
    | 3      | Rahul | 103     |

    2.Departments.
    | dept_id | dept_name |
    | ------- | --------- |
    | 101     | IT        |
    | 102     | HR        |
    | 104     | SALES     |

    Q. we want employee name + department name
    - This requirs the joins.

# 10.1 Types of JOINS
- INNER JOIN
- LEFT JOIN
- RIGHT JOIN
- FULL JOIN

# 10.2 INNER JOIN
- Returns only matching records from both tables
- ```js
    SELECT e.name, d.dept_name
    FROM employees e
    INNER JOIN departments d
    ON e.dept_id = d.dept_id;
    
    Result:
    | name | dept_name |
    | ---- | --------- |
    | Ravi | IT        |
    | Anu  | HR        |

# 10.3 LEFT JOIN
- Returns all records from left table + matching from right.
- ```js
    SELECT e.name, d.dept_name
    FROM employees e
    LEFT JOIN departments d
    ON e.dept_id = d.dept_id;

    // result
    | name  | dept_name |
    | ----- | --------- |
    | Ravi  | IT        |
    | Anu   | HR        |
    | Rahul | NULL      |

# 10.4 RIGHT JOIN
- Returns all records from right table + matching from left.
- ```js
    SELECT e.name, d.dept_name
    FROM employees e
    RIGHT JOIN departments d
    ON e.dept_id = d.dept_id;

    // result
    | name | dept_name |
    | ---- | --------- |
    | Ravi | IT        |
    | Anu  | HR        |
    | NULL | SALES     |

# 10.5 FULL JOIN
- Returns all records from both tables.
- ```js
    SELECT e.name, d.dept_name
    FROM employees e
    FULL JOIN departments d
    ON e.dept_id = d.dept_id;

    //result
    | name  | dept_name |
    | ----- | --------- |
    | Ravi  | IT        |
    | Anu   | HR        |
    | Rahul | NULL      |
    | NULL  | SALES     |

# short form
- ```js
    INNER → Common data
    LEFT → Left + common
    RIGHT → Right + common
    FULL → Everything

# 10.6 JOIN with WHERE
- ```js
    SELECT e.name, d.dept_name
    FROM employees e
    INNER JOIN departments d
    ON e.dept_id = d.dept_id
    WHERE d.dept_name = 'IT';

    //result
    | name | dept_name |
    | ---- | --------- |
    | Ravi | IT        |

# 10.7 Multiple JOIN Example
- ```js
    //orders
    | order_id | customer_id | product_id |
    | -------- | ----------- | ---------- |
    | 1        | 1           | 101        |

    //customers
    | customer_id | customer_name |
    | ----------- | ------------- |
    | 1           | Sai           |

    //products
    | product_id | product_name |
    | ---------- | ------------ |
    | 101        | Laptop       |

    //query
    SELECT o.order_id, c.customer_name, p.product_name
    FROM orders o
    JOIN customers c ON o.customer_id = c.customer_id
    JOIN products p ON o.product_id = p.product_id;

    //when you write just JOIN in SQL, it is shorthand for INNER JOIN.(JOIN = INNER JOIN → only rows that match in both tables are returned.)
    //output
    | order_id | customer_name | product_name |
    | -------- | ------------- | ------------ |
    | 1        | Sai           | Laptop       |











