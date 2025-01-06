

**50 practical SQL questions**

---

### **Basic SQL Questions (1-10)**

1. **Create a Table**:  
   Create a table `Employees` with columns `EmployeeID`, `Name`, `Department`, and `Salary`.  
   ```sql
   CREATE TABLE Employees (
       EmployeeID VARCHAR(255), 
       Name VARCHAR(255), 
       Department VARCHAR(255), 
       Salary INT
   );
   ```

2. **Insert Data**:  
   Insert five records into the `Employees` table.  
   ```sql
   INSERT INTO Employees(EmployeeID, Name, Department, Salary) 
   VALUES 
       ('1', 'AMAL KRISHNA', 'Development', 50000),
       ('2', 'John Doe', 'Marketing', 45000),
       ('3', 'Jane Smith', 'HR', 60000),
       ('4', 'Michael Brown', 'Development', 70000),
       ('5', 'Emily Davis', 'Sales', 55000);
   ```

3. **Select Query**:  
   Write a query to select all columns from the `Employees` table.  
   ```sql
   SELECT * FROM Employees;
   ```

4. **Conditional Query**:  
   Find employees with a salary greater than 50,000.  
   ```sql
   SELECT * FROM Employees WHERE Salary > 50000;
   ```

5. **Update Data**:  
   Update the salary of an employee with `EmployeeID = 3` to 60,000.  
   ```sql
   UPDATE Employees SET Salary = 60000 WHERE EmployeeID = '3';
   ```

6. **Delete Data**:  
   Delete the record of an employee with `EmployeeID = 5`.  
   ```sql
   DELETE FROM Employees WHERE EmployeeID = '5';
   ```

7. **Aggregate Function**:  
   Find the average salary of all employees.  
   ```sql
   SELECT AVG(Salary) FROM Employees;
   ```

8. **Order By Clause**:  
   Display employees ordered by their salaries in descending order.  
   ```sql
   SELECT * FROM Employees ORDER BY Salary DESC;
   ```

9. **GROUP BY Clause**:  
   Group employees by department and find the count of employees in each department.  
   ```sql
   SELECT Department, COUNT(*) FROM Employees GROUP BY Department;
   ```

10. **HAVING Clause**:  
    Show departments where the average salary exceeds 40,000.  
    ```sql
    SELECT Department, AVG(Salary) FROM Employees 
    GROUP BY Department HAVING AVG(Salary) > 40000;
    ```

---

### **Intermediate SQL Questions (11-30)**

11. **Primary Key**:  
    Add a primary key to the `EmployeeID` column in the `Employees` table.  
    ```sql
    ALTER TABLE Employees ADD PRIMARY KEY (EmployeeID);
    ```

12. **Foreign Key**:  
    Create a `Departments` table and establish a foreign key relationship with the `Employees` table.  
    ```sql
    CREATE TABLE Departments (
        DepartmentID VARCHAR(255),
        DepartmentName VARCHAR(255),
        PRIMARY KEY (DepartmentID)
    );

    ALTER TABLE Employees
    ADD COLUMN DepartmentID VARCHAR(255),
    ADD CONSTRAINT FK_Department FOREIGN KEY (DepartmentID) 
    REFERENCES Departments(DepartmentID);
    ```

13. **Join Query**:  
    Retrieve all employees along with their department names using a join.  
    ```sql
    SELECT Employees.Name, Departments.DepartmentName 
    FROM Employees 
    JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID;
    ```

14. **LEFT JOIN**:  
    List all departments, including those without employees, using a left join.  
    ```sql
    SELECT Departments.DepartmentName, Employees.Name 
    FROM Departments
    LEFT JOIN Employees ON Departments.DepartmentID = Employees.DepartmentID;
    ```

15. **UNION**:  
    Combine results of two queries: one retrieving employees with a salary > 50,000 and another retrieving employees with a salary < 30,000.  
    ```sql
    SELECT Name FROM Employees WHERE Salary > 50000
    UNION
    SELECT Name FROM Employees WHERE Salary < 30000;
    ```

16. **Subquery**:  
    Find employees earning more than the average salary.  
    ```sql
    SELECT * FROM Employees 
    WHERE Salary > (SELECT AVG(Salary) FROM Employees);
    ```

17. **IN Operator**:  
    Find employees who belong to the departments `HR` and `Sales`.  
    ```sql
    SELECT * FROM Employees 
    WHERE Department IN ('HR', 'Sales');
    ```

18. **ANY/ALL Operator**:  
    Find employees whose salary is greater than all salaries in the `HR` department.  
    ```sql
    SELECT * FROM Employees 
    WHERE Salary > ALL (SELECT Salary FROM Employees WHERE Department = 'HR');
    ```

19. **CASE Statement**:  
    Write a query to categorize employees' salaries as `High`, `Medium`, or `Low`.  
    ```sql
    SELECT Name, 
        CASE
            WHEN Salary > 70000 THEN 'High'
            WHEN Salary BETWEEN 40000 AND 70000 THEN 'Medium'
            ELSE 'Low'
        END AS SalaryCategory
    FROM Employees;
    ```

20. **Self Join**:  
    Find pairs of employees working in the same department.  
    ```sql
    SELECT E1.Name AS Employee1, E2.Name AS Employee2
    FROM Employees E1, Employees E2
    WHERE E1.Department = E2.Department AND E1.EmployeeID != E2.EmployeeID;
    ```

21. **View**:  
    Create a view that shows employees' names and their department names.  
    ```sql
    CREATE VIEW EmployeeDepartmentView AS
    SELECT Employees.Name AS EmployeeName, Departments.DepartmentName 
    AS DepartmentName
    FROM Employees
    JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID;
    ```

22. **Delete Column**:  
    Remove the `Age` column from the `Employees` table.  
    ```sql
    ALTER TABLE Employees
    DROP COLUMN Age;
    ```

23. **Add Column**:  
    Add a column `JoiningDate` to the `Employees` table.  
    ```sql
    ALTER TABLE Employees
    ADD COLUMN JoiningDate DATE;
    ```

24. **Check Constraint**:  
    Add a constraint to ensure salaries cannot be less than 20,000.  
    ```sql
    ALTER TABLE Employees
    ADD CONSTRAINT Salary_Min_Check CHECK (Salary >= 20000);
    ```

25. **Unique Constraint**:  
    Add a constraint to ensure employee names are unique.  
    ```sql
    ALTER TABLE Employees
    ADD CONSTRAINT Unique_EmployeeName UNIQUE (Name);
    ```

---

### **Intermediate SQL Questions (26-30)**

26. **Indexes**:  
    Create an index on the `Salary` column.  
    ```sql
    CREATE INDEX idx_salary ON Employees (Salary);
    ```

27. **Transactions**:  
    Write a transaction to update salaries and roll it back.  
    ```sql
    BEGIN;

    UPDATE Employees SET Salary = Salary + 5000 WHERE Department = 'Development';

    ROLLBACK; -- Or COMMIT to save changes
    ```

28. **Triggers**:  
    Create a trigger to log changes whenever an employee's salary is updated.  
    ```sql
    CREATE TABLE SalaryChangeLog (
        EmployeeID VARCHAR(255),
        OldSalary INT,
        NewSalary INT,
        ChangeDate TIMESTAMP DEFAULT CURRENT_TIMESTAMP
    );

    CREATE TRIGGER LogSalaryChange
    AFTER UPDATE ON Employees
    FOR EACH ROW
    BEGIN
        INSERT INTO SalaryChangeLog (EmployeeID, OldSalary, NewSalary)
        VALUES (OLD.EmployeeID, OLD.Salary, NEW.Salary);
    END;
    ```

29. **Stored Procedure**:  
    Write a stored procedure to retrieve employees based on a salary range.  
    ```sql
    CREATE PROCEDURE GetEmployeesBySalaryRange(minSalary INT, maxSalary INT)
    AS
    BEGIN
        SELECT * FROM Employees
        WHERE Salary BETWEEN minSalary AND maxSalary;
    END;
    ```

30. **Common Table Expression (CTE)**:  
    Write a CTE to find employees with the top 3 salaries.  
    ```sql
    WITH TopSalaries AS (
        SELECT Name, Salary, RANK() OVER (ORDER BY Salary DESC) AS Rank
        FROM Employees
    )
    SELECT * FROM TopSalaries WHERE Rank <= 3;
    ```

---

### **Advanced SQL Questions (31-50)**

31. **Window Functions**:  
    Use a window function to calculate the running total of salaries.  
    ```sql
    SELECT Name, Salary, 
           SUM(Salary) OVER (ORDER BY EmployeeID) AS RunningTotal
    FROM Employees;
    ```

32. **Rank Function**:  
    Rank employees by their salary within each department.  
    ```sql
    SELECT Name, Department, Salary,
           RANK() OVER (PARTITION BY Department ORDER BY Salary DESC) AS Rank
    FROM Employees;
    ```

33. **Partitioning**:  
    Find the average salary partitioned by department.  
    ```sql
    SELECT Department, AVG(Salary) OVER (PARTITION BY Department) AS AverageSalary
    FROM Employees;
    ```

34. **Correlated Subquery**:  
    Write a query to find employees who earn more than the average salary of their department.  
    ```sql
    SELECT Name, Department, Salary
    FROM Employees E
    WHERE Salary > (
        SELECT AVG(Salary)
        FROM Employees
        WHERE Department = E.Department
    );
    ```

35. **EXISTS Clause**:  
    Write a query to find departments that have employees earning over 70,000.  
    ```sql
    SELECT Department
    FROM Departments D
    WHERE EXISTS (
        SELECT 1
        FROM Employees E
        WHERE E.Department = D.DepartmentID
        AND E.Salary > 70000
    );
    ```

36. **NOT EXISTS Clause**:  
    Find departments with no employees.  
    ```sql
    SELECT DepartmentName
    FROM Departments D
    WHERE NOT EXISTS (
        SELECT 1 FROM Employees E
        WHERE E.DepartmentID = D.DepartmentID
    );
    ```

37. **Materialized View**:  
    Create a materialized view for employees' salary details.  
    ```sql
    CREATE MATERIALIZED VIEW EmployeeSalaryDetails AS
    SELECT Name, Department, Salary
    FROM Employees;
    ```

38. **Clustered Index**:  
    Explain and create a clustered index on the `EmployeeID` column.  
    A clustered index sorts the data in the table by the index key. Only one clustered index is allowed per table.
    ```sql
    CREATE CLUSTERED INDEX idx_employeeid ON Employees (EmployeeID);
    ```

39. **Union vs Union All**:  
    Demonstrate the difference between `UNION` and `UNION ALL`.  
    - `UNION` eliminates duplicate rows.
    - `UNION ALL` keeps all rows, including duplicates.

    Example of `UNION`:  
    ```sql
    SELECT Name FROM Employees WHERE Salary > 50000
    UNION
    SELECT Name FROM Employees WHERE Department = 'Sales';
    ```

    Example of `UNION ALL`:  
    ```sql
    SELECT Name FROM Employees WHERE Salary > 50000
    UNION ALL
    SELECT Name FROM Employees WHERE Department = 'Sales';
    ```

40. **Scalar Function**:  
    Write a scalar function to calculate the annual salary of an employee.  
    ```sql
    CREATE FUNCTION CalculateAnnualSalary(Salary INT)
    RETURNS INT
    AS
    BEGIN
        RETURN Salary * 12;
    END;
    ```

41. **Aggregate Function**:  
    Use `GROUP BY` and `HAVING` with aggregate functions like `COUNT`, `MAX`, and `MIN`.  
    ```sql
    SELECT Department, COUNT(*), MAX(Salary), MIN(Salary)
    FROM Employees
    GROUP BY Department
    HAVING COUNT(*) > 1;
    ```

42. **Normalization**:  
    Normalize a table to 3NF and explain the process.  
    - **1NF**: Ensure that each column contains atomic values.
    - **2NF**: Remove partial dependencies (every non-key attribute must be fully dependent on the primary key).
    - **3NF**: Remove transitive dependencies (non-key attributes should not depend on other non-key attributes).

    Example:
    - Initial table:
      | EmployeeID | Name  | Department | DepartmentLocation |
      |------------|-------|------------|---------------------|
    - After normalization, split into two tables:
      - `Employees (EmployeeID, Name, DepartmentID)`
      - `Departments (DepartmentID, Department, Location)`

43. **Denormalization**:  
    Demonstrate when denormalization might be beneficial.  
    Denormalization can be useful for read-heavy systems to improve query performance by reducing the need for joins.

44. **Composite Key**:  
    Create a composite key using two columns.  
    ```sql
    CREATE TABLE EmployeeProject (
        EmployeeID VARCHAR(255),
        ProjectID VARCHAR(255),
        PRIMARY KEY (EmployeeID, ProjectID)
    );
    ```

45. **Recursive Query**:  
    Write a recursive CTE to generate a series of numbers from 1 to 10.  
    ```sql
    WITH RECURSIVE NumberSeries AS (
        SELECT 1 AS Number
        UNION ALL
        SELECT Number + 1
        FROM NumberSeries
        WHERE Number < 10
    )
    SELECT * FROM NumberSeries;
    ```

46. **Pivot Table**:  
    Create a pivot table to summarize employee count by department and salary range.  
    ```sql
    SELECT Department, 
           CASE 
               WHEN Salary BETWEEN 0 AND 40000 THEN '0-40k'
               WHEN Salary BETWEEN 40001 AND 80000 THEN '40k-80k'
               ELSE 'Above 80k'
           END AS SalaryRange,
           COUNT(*) AS EmployeeCount
    FROM Employees
    GROUP BY Department, SalaryRange;
    ```

47. **JSON Data**:  
    Store and retrieve JSON data from a table in PostgreSQL.  
    ```sql
    CREATE TABLE EmployeeData (
        EmployeeID INT,
        EmployeeInfo JSON
    );

    INSERT INTO EmployeeData (EmployeeID, EmployeeInfo)
    VALUES (1, '{"Name": "John", "Age": 30, "Department": "Development"}');

    SELECT * FROM EmployeeData WHERE EmployeeInfo->>'Department' = 'Development';
    ```

48. **Full-Text Search**:  
    Implement full-text search in PostgreSQL.  
    ```sql
    CREATE INDEX idx_ft_text ON Employees 
    USING gin(to_tsvector('english', Name));

    SELECT * FROM Employees 
    WHERE to_tsvector('english', Name) @@ to_tsquery('english', 'John');
    ```

49. **Backup and Restore**:  
    Perform a database backup and restore operation.  
    - Backup:  
    ```bash
    pg_dump mydb > mydb_backup.sql
    ```
    - Restore:  
    ```bash
    psql mydb < mydb_backup.sql
    ```

50. **Query Optimization**:  
    Explain and optimize a query to improve performance.  
    - Example optimization: Use indexes, avoid SELECT *, use joins instead of subqueries when possible, and avoid redundant calculations.
    ```sql
    EXPLAIN ANALYZE 
    SELECT Name, Salary FROM Employees WHERE Department = 'Development';
    ```

---