## 1. SELECT last_name, job_id, salary AS Sal FROM employees;

```
return true
```

## 2. SELECT \* FROM job_grades;

```
return false because job_grades table does not exists in database
```

## 3. SELECT employee_id, last_namesal x 12ANNUAL SALARYFROM employees;

```
right query :-> SELECT employee_id, last_name, salary\*12 "ANNUAL SALERY" FROM employees;

1. there shpuld be space between SALERY and FROM
2. last_name and salery should be separated by comma,
3. the column sal does not exists it's salery .
4. for multyplying salery to 12 we dont use x we use \*.
```

## 4. Create aquery to display unique job codes from the EMPLOYEES table

```
SELECT DISTINCT job_id from employees;
```

## 5. Show the structure of the EMPLOYEES table. Create a query to display the last name, job code, hire date, and employee number for each employee,with employee number appearing first. Provide an alias STARTDATE for the HIRE_DATE column.

```
select employee_id,last_name,job_id,hire_date START_DATE from employees;
```

## 6. Display the last name concatenated with the job ID, separated by a comma and space, and name the column Employee and Title.

```
select last_name || ', ' || job_id "Employee and Title" from employees;
```

## 7. Create a query to display all the data from the EMPLOYEE table. Separate each column by acomma. Name the column THE_OUTPUT.

```
select (employee_id || ',' || first_name ||',' || last_name ||',' || email || ','
		|| phone_number || ',' || job_id || ',' ||hire_date ||',' || salary || ','
		|| job_id ||manager_id ||',' ||department_id) as "THE_OUTPUT" from employees;
```
