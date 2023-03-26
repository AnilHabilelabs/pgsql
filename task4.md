## 1.Write a query to display the last name, department number, and department name for all employees.

```
select last_name,department_id,department_name from employees natural join departments;
```

### OR

```
select last_name,d.department_id,department_name from employees e inner join departments d on e.department_id=d.department_id
```

## 2. Create a unique listing of all jobs that are in department 8. Include the location of the department in the output.

```
select distinct job_title,city from employees e inner join jobs j on e.job_id = j.job_id
inner join departments d on e.department_id = d.department_id
inner join locations l on d.location_id = l.location_id where e.department_id = 8;
```

## 3. Write a query to display the employee last name, department name, location ID, and city of all employees.

```
select last_name,department_name,d.location_id,city from employees e inner join
departments d on e.department_id=d.department_id inner join locations l on d.location_id = l.location_id;
```

## 4. Display the employee last name and department name for all employees who have an a (lowercase) in their last names.

```
select last_name,department_name from employees e join departments d on
d.department_id = e.department_id where last_name like '%a%';
```

## 5. Write a query to display the last name, job, department number, and department name for all employees who work in Toronto.

```
select last_name,job_title,e.department_id,department_name from employees e join departments d on
e.department_id = d.department_id join jobs j on e.job_id = j.job_id where location_id = 1800;
```

### OR

```
select last_name,job_title,e.department_id,department_name from employees e join departments d on
e.department_id = d.department_id join jobs j on e.job_id = j.job_id join locations l on
d.location_id = l.location_id where city = 'Toronto';
```

## 6. Display the employee last name and employee number along with their manager’s last name and manager number. Label the columns Employee, Emp#, Manager, and Mgr#, respectively.

```
select e.last_name "Employee",e.employee_id "Emp#",m.last_name "Manager",e.manager_id "Mgr#" from employees e inner join employees m
on m.employee_id = e.manager_id;
```

## 7. Modify the query of #6 to display all employees including King, who has no manager.

```
select e.last_name "Employee",e.employee_id "Emp#",m.last_name "Manager",e.manager_id "Mgr#"
from employees e left outer join employees m on m.employee_id = e.manager_id;
```

## 8. Create a query that displays employee last names, department numbers, and all the employees who work in the same department as a given employee. Give each column an appropriate label.

```
select e1.last_name,e1.department_id from employees e1 join
employees e2 on e1.department_id = e2.department_id where e1.employee_id = e2.employee_id;
```

## 10. Create a query to display the name and hire date of any employee hired after employee Daniel.

```
select last_name,hire_date from employees where hire_date >
(select hire_date from employees where first_name='Daniel');
```

## 11. Display the names and hire dates for all employees who were hired before their managers, along with their manager’s names and hire dates. Label the columns Employee, Emp Hired, Manager, and Mgr Hired, respectively.

```
select e.last_name "Employee", e.hire_date "Emp Hired",m.last_name "Manager",m.hire_date "Mgr Hired" from employees e join employees m
on e.manager_id = m.employee_id where m.hire_date > e.hire_date;
```

## 12. Determine the validity of the following three statements. Circle either True or False.

- a. Group functions work across many rows to produce one result. -TRUE
- b. Group functions include nulls in calculations. - FALSE
- c. The WHERE clause restricts rows prior to inclusion in a group calculation. -TRUE

## 13. Display the highest, lowest, sum, and average salary of all employees. Label the columns Maximum, Minimum, Sum, and Average, respectively. Round your results to the nearest whole number.

```
select round(max(salary)) "Maximum", round(min(salary)) "Minimum",
round(sum(salary)) "Sum", round(avg(salary)) "Average" from employees;
```

## 14. Modify the query in #13 to display the minimum, maximum, sum, and average salary for each job type.

```
select round(max(salary)) "Maximum", round(min(salary)) "Minimum",
round(sum(salary)) "Sum", round(avg(salary)) "Average",job_title from employees e
join jobs j on e.job_id = j.job_id group by job_title;
```

## 15. Write a query to display the number of people with the same job.

```
select count(j.job_id) "Employee count",job_title from employees e join jobs j on
e.job_id = j.job_id group by j.job_id;
```

## 16. Determine the number of managers without listing them. Label the column Number of Managers. Hint: Use the MANAGER_ID column to determine the number of managers.

```
select count(manager_id) from employees;
```

## 17. Write a query that displays the difference between the highest and lowest salaries. Label the column DIFFERENCE.

```
select concat(round(max(salary)),'-',round(min(salary)),' = ', round(max(salary))-round(min(salary)))
"DIFFERENCE" from employees;
```

## 18. Display the manager number and the salary of the lowest paid employee for that manager Exclude anyone whose manager is not known. Exclude any groups where the minimum salary is $6,000 or less. Sort the output in descending order of salary.

```
select m.manager_id, min(e.salary) as "SALARY" from employees e inner join employees m
on e.employee_id = m.manager_id where e.salary >=6000 group by m.manager_id order by "SALARY" ;
```

## 19. Write a query to display each department’s name, location, number of employees, and the average salary for all employees in that department. Label the columns Name, Location, Number of People, and Salary, respectively. Round the average salary to two decimal places.

```
select d.department_name,l.city "location",count(e.employee_id) "Number of People",round(avg(e.salary)) "average salary" from employees e join
departments d on e.department_id = d.department_id inner join locations l on
l.location_id = d.location_id group by d.department_id,l.city;
```

## 20. Create a query to display the job, the salary for that job based on department number, and the total salary for that job, for departments 2, 5, 8, and 9, giving each column an appropriate heading.

```
select job_title,salary,sum(salary) over (partition by job_title),department_id from employees natural join jobs
where department_id in(2,5,8,9) group by job_title,department_id,salary ;
```

## 21. Write a script to display the employee last name, job, and department name for a given location. The search condition should allow for case-insensitive searches of the department location.

> WITHOUT FUNCTION

```
SELECT e.last_name, j.job_title, d.department_name
FROM employees e
JOIN jobs j ON e.job_id = j.job_id
JOIN departments d ON e.department_id = d.department_id
JOIN locations l ON d.location_id = l.location_id
WHERE LOWER(l.city) = LOWER('Toronto');
```

> WITH FUNCTION

```
DROP FUNCTION IF EXISTS get_employee_info_by_location(text);

create or replace function get_employee_info_by_location(location_name text)
returns table (last_name TEXT, job_title TEXT, department_name TEXT)
AS $$
begin
    return query
    select e.last_name::text, j.job_title::text, d.department_name::text
    from employees e
    join jobs j ON e.job_id = j.job_id
    join departments d ON e.department_id = d.department_id
    join locations l ON d.location_id = l.location_id
    where lower(l.city) = lower(location_name);
end;
$$ LANGUAGE PLPGSQL;


SELECT * FROM get_employee_info_by_location('Toronto');
```

## 22. create a report containing the department name, employee last name, hire date, salary, and each employee’s annual salary for all employees in a given location. Label the columns DEPARTMENT NAME, EMPLOYEE NAME, START DATE, SALARY, and ANNUAL SALARY, placing the labels on multiple lines

```

DROP FUNCTION IF EXISTS get_emp_info_by_location(text);

create or replace function get_emp_info_by_location(location text)
returns table(
	department_name text,
	last_name text,
	start_date date,
	salary numeric(10,2),
	annual_salary numeric(10,2)
)
as $$ BEGIN return query
    select d.department_name, e.last_name,e.salary,e.salary*12
    FROM employees e join departments d on e.department_id = d.departments_id
    join location l on d.location_id = l.location_id
    where lower(l.city) = lower(location);
    END;
$$ LANGUAGE PLPGSQL;


SELECT * FROM get_employee_info_by_location('Toronto');
```
