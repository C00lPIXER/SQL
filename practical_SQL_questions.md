**50 practical SQL questions**

---

### **Basic SQL Questions (1-10)**

1. **Create a Table**: Create a table `Employees` with columns `EmployeeID`, `Name`, `Department`, and `Salary`.

   ```
   CREATE TABLE Employees (EmployeeID VARCHAR(255), Name VARCHAR(255), Department    VARCHAR(255), Salary INT);
   ```

2. **Insert Data**: Insert five records into the `Employees` table.

   ```
   INSERT INTO Employees(EmployeeID, Name, Department, Salary) VALUES ('E01', 'AMAL KRISHNA', 'Development', 50000)
   ```

3. **Select Query**: Write a query to select all columns from the `Employees` table.
4. **Conditional Query**: Find employees with a salary greater than 50,000.
5. **Update Data**: Update the salary of an employee with `EmployeeID = 3` to 60,000.
6. **Delete Data**: Delete the record of an employee with `EmployeeID = 5`.
7. **Aggregate Function**: Find the average salary of all employees.
8. **Order By Clause**: Display employees ordered by their salaries in descending order.
9. **GROUP BY Clause**: Group employees by department and find the count of employees in each department.
10. **HAVING Clause**: Show departments where the average salary exceeds 40,000.

---

### **Intermediate SQL Questions (11-30)**

11. **Primary Key**: Add a primary key to the `EmployeeID` column in the `Employees` table.
12. **Foreign Key**: Create a `Departments` table and establish a foreign key relationship with the `Employees` table.
13. **Join Query**: Retrieve all employees along with their department names using a join.
14. **LEFT JOIN**: List all departments, including those without employees, using a left join.
15. **UNION**: Combine results of two queries: one retrieving employees with a salary > 50,000 and another retrieving employees with a salary < 30,000.
16. **Subquery**: Find employees earning more than the average salary.
17. **IN Operator**: Find employees who belong to the departments `HR` and `Sales`.
18. **ANY/ALL Operator**: Find employees whose salary is greater than all salaries in the `HR` department.
19. **CASE Statement**: Write a query to categorize employees' salaries as `High`, `Medium`, or `Low`.
20. **Self Join**: Find pairs of employees working in the same department.
21. **View**: Create a view that shows employees' names and their department names.
22. **Delete Column**: Remove the `Age` column from the `Employees` table.
23. **Add Column**: Add a column `JoiningDate` to the `Employees` table.
24. **Check Constraint**: Add a constraint to ensure salaries cannot be less than 20,000.
25. **Unique Constraint**: Add a constraint to ensure employee names are unique.
26. **Indexes**: Create an index on the `Salary` column.
27. **Transactions**: Write a transaction to update salaries and roll it back.
28. **Triggers**: Create a trigger to log changes whenever an employee's salary is updated.
29. **Stored Procedure**: Write a stored procedure to retrieve employees based on a salary range.
30. **Common Table Expression (CTE)**: Write a CTE to find employees with the top 3 salaries.

---

### **Advanced SQL Questions (31-50)**

31. **Window Functions**: Use a window function to calculate the running total of salaries.
32. **Rank Function**: Rank employees by their salary within each department.
33. **Partitioning**: Find the average salary partitioned by department.
34. **Correlated Subquery**: Write a query to find employees who earn more than the average salary of their department.
35. **EXISTS Clause**: Write a query to find departments that have employees earning over 70,000.
36. **NOT EXISTS Clause**: Find departments with no employees.
37. **Materialized View**: Create a materialized view for employees' salary details.
38. **Clustered Index**: Explain and create a clustered index on the `EmployeeID` column.
39. **Union vs Union All**: Demonstrate the difference between UNION and UNION ALL.
40. **Scalar Function**: Write a scalar function to calculate the annual salary of an employee.
41. **Aggregate Function**: Use `GROUP BY` and `HAVING` with aggregate functions like COUNT, MAX, and MIN.
42. **Normalization**: Normalize a table to 3NF and explain the process.
43. **Denormalization**: Demonstrate when denormalization might be beneficial.
44. **Composite Key**: Create a composite key using two columns.
45. **Recursive Query**: Write a recursive CTE to generate a series of numbers from 1 to 10.
46. **Pivot Table**: Create a pivot table to summarize employee count by department and salary range.
47. **JSON Data**: Store and retrieve JSON data from a table in PostgreSQL.
48. **Full-Text Search**: Implement full-text search in PostgreSQL.
49. **Backup and Restore**: Perform a database backup and restore operation.
50. **Query Optimization**: Explain and optimize a query to improve performance.

---