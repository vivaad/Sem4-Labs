Certainly! Here is a structured markdown file for your SQL lab record:

# LAB4 - COMPLEX QUERIES ON SQL

## Group By

1. **Find the number of students in each course.**
```sql
select course_id, count(id) from takes group by course_id;
```

2. **Find those departments where the average number of students are greater than 10.**
```sql
select dept_name from student group by dept_name having count(id) > 3;
```

3. **Find the total number of courses in each department.**
```sql
select dept_name, count(course_id) from course group by dept_name;
```

4. **Find the names and average salaries of all departments whose average salary is greater than 42000.**
```sql
select dept_name, avg(salary) from instructor group by dept_name having avg(salary) > 42000;
```

5. **Find the enrolment of each section that was offered in Spring 2009.**
```sql
select course_id, sec_id, count(id) from takes where semester = 'Spring' and year = 2009 group by sec_id, course_id;
```

## Ordering the display of Tuples (Use ORDER BY ASC/DESC)

6. **List all the courses with prerequisite courses, then display course id in increasing order.**
```sql
select course_id, prereq_id from prereq order by course_id;
```

7. **Display the details of instructors sorting the salary in decreasing order.**
```sql
select * from instructor order by salary desc;
```

## Derived Relations

8. **Find the maximum total salary across the departments.**
```sql
with dept_sal as (select dept_name, sum(salary) as tot_sal from instructor group by dept_name)
select dept_name, tot_sal 
from dept_sal
where tot_sal = (select max(tot_sal) from dept_sal);
```

9. **Find the average instructors’ salaries of those departments where the average salary is greater than 42000.**
```sql
with dept_avg_sal as (select dept_name, avg(salary) as avg_sal 
		      from instructor 
		      group by dept_name)
select dept_name, avg_sal 
from dept_avg_sal 
where avg_sal > 42000;
```

10. **Find the sections that had the maximum enrolment in Spring 2010.**
```sql
with sec_enroll as (select course_id, sec_id, count(id) as students 
		    from takes 
		    where semester = 'Spring' and year = 2010 
		    group by sec_id, course_id)
select course_id, sec_id, students 
from sec_enroll 
where students = (select max(students) 
		  from sec_enroll);
```

11. **Find the names of all instructors who teach all students that belong to 'CSE' department.**
```sql
select name
from instructor I
where not exists(
    select id
    from student
    where dept_name='Comp. Sci.'
    minus
    select T.id
    from takes T, teaches E
    where T.course_id=E.course_id and T.sec_id=E.sec_id 
        and T.semester=E.semester and T.year=E.year 
        and E.id=I.id
);
```

12. **Find the average salary of those departments where the average salary is greater than 50000 and total number of instructors in the department are more than 5.**
```sql
// Incomplete
with avg_dept_sal as (select dept_name, avg(salary) as avg_sal from instructor group by dept_name having avg_sal > 50000)
```

## With Clause

13. **Find all departments with the maximum budget.**
```sql
// Code for this query not provided in the given context
```

14. **Find all departments where the total salary is greater than the average of the total salary at all departments.**
```sql
// Code for this query not provided in the given context
```

## Transactions (Use ROLLBACK and SAVEPOINT)

15. **Transfer all the students from CSE department to IT department.**
```sql
// Code for this query not provided in the given context
```

16. **Increase salaries of instructors whose salary is over $100,000 by 3%, and all others receive a 5% raise.**
```sql
// Code for this query not provided in the given context
```
