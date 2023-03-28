## 1. Create a table MY\_ EMPLOYEE with columns id, last_name,first_name,user_id,salary.

```
create table MY_EMPLOYEE (id serial primary key not null,
						  first_name varchar(20),
						  last_name varchar(20),
						  user_id varchar(20),
						  salary NUMERIC(10, 2));

```

## 2. Add the rows of data to the MY_EMPLOYEE table from the following sample data. Concatenate the first letter of the first name and the first seven characters of the last name to produce the userid.

```
insert into my_employee(first_name,last_name,user_id,salary)
values('anil','karela',concat(substring('anil',1,1),
							  substring('karela',1,7)),2000),
	  ('anil','karela',concat(substring('anil',1,1),
							  substring('karela',1,7)),2000),
	  ('anshul','gadia',concat(substring('anshul',1,1),
							  substring('gadia',1,7)),2000),
	  ('jatin','kumar',concat(substring('jatin',1,1),
							  substring('kumar',1,7)),2000),
	  ('vaibhav','bansal',concat(substring('vaibhav',1,1),
							  substring('bansal',1,7)),2000);
```

## 3. Confirm your addition to the table.

```
Confirm your addition to the table.
```

## 4. Make the data additions permanent.

```
commit
```

## 5. Change the last name of employee 6 to Drexler.

```
update my_employee set last_name = 'Drexler' where id = 6;
```

## 6. Change the last name of employee 103 to Drexler.

```
update my_employee set salary = 1000 where salary <900;
```

## 7. Verify your changes to the table.

```
select * from my_employee;
```

## 8. Delete anil kumar from the MY_EMPLOYEE table.

```
delete from my_employee where first_name = 'anil';
```

## 9. Confirm your changes to the table.

```
select * from my_employee;
```

## 10.Commit all pending changes.

```
commit
```

# 11.Modify the MY_EMPLOYEES table to allow for longer employee last names. Confirm your modification.

```
alter table my_employee alter column last_name varchar(50);
```

> we can check the schemas of the table and new longer length of last_name using this

```
SELECT column_name, data_type, character_maximum_length
FROM information_schema.columns
WHERE table_name = 'my_employee' AND column_name = 'last_name';
```

## 12.Create the MY_EMPLOYEES2 table based on the structure of the EMPLOYEES table. Include only the EMPLOYEE_ID, FIRST_NAME, LAST_NAME, SALARY, and DEPARTMENT_ID columns. Name the columns in your new table ID, FIRST_NAME, LAST_NAME, SALARY , and DEPT_ID, respectively.

```
create table MY_EMPLOYEES2 as
select id "EMPLOYEE_ID",first_name "FIRST_NAME",last_name "LAST_NAME",
user_id "USER_ID",salary "SALARY" from my_employee;
```
