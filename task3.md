## 1. For each employee, display the employee’s last name, and calculate the number of months between today and the date the employee was hired. Label the column MONTHS_WORKED. Order your results by the number of months employed. Round the number of months up to the closest whole number.

```
select last_name, extract(year from age(current_date, hire_date))*12 + extract(month from age(current_date, hire_date)) as "MONTHS WORKED" from employees order by "MONTHS WORKED";

```

## 2. Write a query that produces the following for each employee: <employee last name> earns <salary> monthly but wants <3 times salary>. Label the column Dream Salaries.

```
SELECT concat(last_name,' earns ',round(salary), ' monthly but wants ',round(3\*salary)) "Dream Salaries" from employees;

```

## 3. Create a query to display the last name and salary for all employees. Format the salary to be 15 characters long, left-padded with $. Label the column SALARY.

```

select concat(lpad(cast(round(salary) as Varchar),15,'$'),last_name) "SALARY" from employees;

```

## 4. Display the last name, hire date, and day of the week on which the employee started. Label the column DAY. Order the results by the day of the week starting with Monday.

```

select last_name,hire_date,extract( isodow from hire_date) as dayofweek,
to_char( hire_date, 'Day') as day from employees order by dayofweek;

```

## 5. Create a query that displays the employees’ last names and manager_id. If an employee does not have a manager, put 1. Label the column MANAGER_ID.

```

select last_name,coalesce(manager_id,1) "MANAGER ID" from employees;

```

## 6. Create a query that displays the employees’ last names and indicates the amounts of their annual salaries with asterisks. Each asterisk signifies a thousand dollars. Sort the data in descending order of salary. Label the column EMPLOYEES_AND_THEIR_SALARIES.

```

select last_name,concat(round(salary*12/1000), repeat('*',cast(length(cast(round(salary\*12/1000) as varchar))as int))) from employees;

```

## 7. write a query that displays the grade of all employees based on the value of the job title, as per the following data:

        JOB		           GRADE
    "President"			    A
    "Stock Manager"		    B
    "Programmer"			C
    "Sales Representative"	D
    "Stock Clerk"			E
    None of the above		0

```

select last_name,job_title, case job_title
when 'President' then 'A'
when 'Stock Manager' then 'B'
when 'Programmer' then 'C'
when 'Sales Representative' then 'D'
when 'Stock Clerk' then 'E'
else '0'
END "GRADE"
from employees inner join jobs
on employees.job_id = jobs.job_id

```

```

```
