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
select job_title,hire_date "start date" from employees inner join jobs on employees.job_id = jobs.job_id 
where hire_date between'1998-02-20' and '1998-05-01' order by hire_date;
```