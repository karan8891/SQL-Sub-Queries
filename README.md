## SQL-Sub-Queries<br>
- Practicing the T-SQL sub-queries and making it complex to keep challenging myself to learn new.<br>

- Using SQL Server Management Studio and SQL Server for Database operations.<br>

### Part1: Queries to create tables<br>

#### Table 1 Query:<br>
Create Table EmployeeDemographics <br>
(EmployeeID int, <br>
FirstName varchar(50), <br>
LastName varchar(50), <br>
Age int, <br>
Gender varchar(50)<br>
)

<br>

#### Table 2 Query:<br>
Create Table EmployeeSalary <br>
(EmployeeID int, <br>
JobTitle varchar(50), <br>
Salary int<br>
)

<br>

#### Table 1 Insert:<br>
Insert into EmployeeDemographics VALUES<br>
(1001, 'Jim', 'Halpert', 30, 'Male'),<br>
(1002, 'Pam', 'Beasley', 30, 'Female'),<br>
(1003, 'Dwight', 'Schrute', 29, 'Male'),<br>
(1004, 'Angela', 'Martin', 31, 'Female'),<br>
(1005, 'Toby', 'Flenderson', 32, 'Male'),<br>
(1006, 'Michael', 'Scott', 35, 'Male'),<br>
(1007, 'Meredith', 'Palmer', 32, 'Female'),<br>
(1008, 'Stanley', 'Hudson', 38, 'Male'),<br>
(1009, 'Kevin', 'Malone', 31, 'Male')<br>

<br>

#### Table 2 Insert:<br>
Insert Into EmployeeSalary VALUES<br>
(1001, 'Salesman', 45000),<br>
(1002, 'Receptionist', 36000),<br>
(1003, 'Salesman', 63000),<br>
(1004, 'Accountant', 47000),<br>
(1005, 'HR', 50000),<br>
(1006, 'Regional Manager', 65000),<br>
(1007, 'Supplier Relations', 41000),<br>
(1008, 'Salesman', 48000),<br>
(1009, 'Accountant', 42000)<br>

<br>

### Part2: Queries for Sub-queries<br>

Select EmployeeID, JobTitle, Salary<br>
From EmployeeSalary<br>

<br>

#### Subquery in Select<br>

Select EmployeeID, Salary, (Select AVG(Salary) From EmployeeSalary) as AllAvgSalary<br>
From EmployeeSalary<br>

<br>

#### How to do it with Partition By<br>

Select EmployeeID, Salary, AVG(Salary) over () as AllAvgSalary<br>
From EmployeeSalary<br>

<br>

#### Why Group By doesn't work<br>

Select EmployeeID, Salary, AVG(Salary) as AllAvgSalary<br>
From EmployeeSalary<br>
Group By EmployeeID, Salary<br>
order by EmployeeID<br>

<br>

#### Subquery in From<br>

Select a.EmployeeID, AllAvgSalary<br>
From <br>
	(Select EmployeeID, Salary, AVG(Salary) over () as AllAvgSalary<br>
	 From EmployeeSalary) a<br>
Order by a.EmployeeID<br>

<br>

#### Subquery in Where<br>

Select EmployeeID, JobTitle, Salary<br>
From EmployeeSalary<br>
where EmployeeID in (<br>
	Select EmployeeID <br>
	From EmployeeDemographics<br>
	where Age > 30)<br>
  
  <br>
  
### References
- https://www.youtube.com/watch?v=m1KcNV-Zhmc&list=WL&index=5
- https://www.youtube.com/watch?v=ECuqb5Tv9qI
