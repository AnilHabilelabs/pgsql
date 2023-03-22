## 1. Create a query to display the data of employees joined after 2009-02-28.

```
select * from employees where hire_date > '2009-02-28';
```

## 2. Create a query to display the last name and salary of employees earning more than $12,000.

```
select last_name,salary from employees where salary > 12000 ;
```

## 3. Create a query to display the employee last name and department number for employee number 176.

```
select last_name,department_id from employees where employee_id = 176 ;
```

## 4. Display the last name and department number of all employees in departments 20 and 50 in alphabetical order by name.

```
select last_name,department_id from employees where department_id between 20 and 50 order by first_name;
```

## 5. Display the employee job title and hire date of employees hired between February 20, 1998, and May 1, 1998. Order the query in ascending order by start date.

```
select job_title,hire_date "start date" from employees
inner join jobs on
employees.job_id = jobs.job_id
where hire_date between'1998-02-20' and '1998-05-01' order by hire_date;
```

## 6. Display the job title and and hire date of every employee who was hired in 1994.

```
select job_title,hire_date "start date" from employees
inner join jobs on employees.job_id = jobs.job_id
where hire_date between'1994-01-01' and '1994-12-31' order by hire_date;
```

## 7.Display the last name and job title of all employees who do not have a manager.

```
select last_name,job_title from employees inner join jobs on employees.job_id = jobs.job_id
where manager_id is null;
```

## 8. Display the last name, salary for all employees . Sort data in descending order of salary.

```
select last_name,salary from employees order by salary desc;

```

## 9.Display the last names of all employees where the third letter of the name is an a.

```
select last_name from employees where last_name like '\_\_a%';
```

## 10. Display the last name of all employees who have an a and an e in their last name.

```
select last_name from employees where last_name like '%a%e%' or last_name like '%e%a%';
```

## 11. Display the last name, job, and salary for all employees whose salary is not equal to $2,500, $3,500, or $7,000.

```
select last_name,job_title,salary from employees inner join jobs on employees.job_id=jobs.job_id
where salary not in(2500,3500,7000);
```

## 12. Write a query to display the current date. Label the column Date.

```
select current_date "Date";
```

## 13. 13. For each employee, display the employee number, last_name, salary, and salary increased by 15% and expressed as a whole number. Label the column New Salary.

```
select employee_id,last_name,salary, cast(salary+15*salary/100 as integer)  as "New Salary" from employees;
```

## 14.Write a query that displays the employee’s last names with the first letter capitalized and all other letters lowercase and the length of the name for all employees whose name starts with J, A, or M. Give each column an appropriate label. Sort the results by the employees’ last names.

```
select last_name, initcap(first_name) as "first_name",length(concat(first_name,last_name)) "Name Length" from employees
where last_name like 'J%' or last_name like 'A%' or last_name like 'M%' order by last_name;
```
