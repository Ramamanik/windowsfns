# windowsfns

Results grid
------------
Execute:
> select * from employee

+ ----------- + ------------- + -------------- + ----------- +
| emp_ID      | emp_NAME      | DEPT_NAME      | SALARY      |
+ ----------- + ------------- + -------------- + ----------- +
| 101         | Mohan         | Admin          | 4000        |
| 102         | Rajkumar      | HR             | 3000        |
| 103         | Akbar         | IT             | 4000        |
| 104         | Dorvin        | Finance        | 6500        |
| 105         | Rohit         | HR             | 3000        |
| 106         | Rajesh        | Finance        | 5000        |
| 107         | Preet         | HR             | 7000        |
| 108         | Maryam        | Admin          | 4000        |
| 109         | Sanjay        | IT             | 6500        |
| 110         | Vasudha       | IT             | 7000        |
| 111         | Melinda       | IT             | 8000        |
| 112         | Komal         | IT             | 10000       |
| 113         | Gautham       | Admin          | 2000        |
| 114         | Manisha       | HR             | 3000        |
| 115         | Chandni       | IT             | 4500        |
| 116         | Satya         | Finance        | 6500        |
| 117         | Adarsh        | HR             | 3500        |
| 118         | Tejaswi       | Finance        | 5500        |
| 119         | Cory          | HR             | 8000        |
| 120         | Monica        | Admin          | 5000        |
| 121         | Rosalin       | IT             | 6000        |
| 122         | Ibrahim       | IT             | 8000        |
| 123         | Vikram        | IT             | 8000        |
| 124         | Dheeraj       | IT             | 11000       |
+ ----------- + ------------- + -------------- + ----------- +
24 rows

Execute:
> select dept_name, max(salary) from employee
group by dept_name

+ -------------- + ---------------- +
| dept_name      | max(salary)      |
+ -------------- + ---------------- +
| Admin          | 5000             |
| HR             | 8000             |
| IT             | 11000            |
| Finance        | 6500             |
+ -------------- + ---------------- +
4 rows

Execute:
> select e.*,
max(salary) over(partition by dept_name) as max_salary
from employee e

+ ----------- + ------------- + -------------- + ----------- + --------------- +
| emp_ID      | emp_NAME      | DEPT_NAME      | SALARY      | max_salary      |
+ ----------- + ------------- + -------------- + ----------- + --------------- +
| 101         | Mohan         | Admin          | 4000        | 5000            |
| 108         | Maryam        | Admin          | 4000        | 5000            |
| 113         | Gautham       | Admin          | 2000        | 5000            |
| 120         | Monica        | Admin          | 5000        | 5000            |
| 104         | Dorvin        | Finance        | 6500        | 6500            |
| 106         | Rajesh        | Finance        | 5000        | 6500            |
| 116         | Satya         | Finance        | 6500        | 6500            |
| 118         | Tejaswi       | Finance        | 5500        | 6500            |
| 102         | Rajkumar      | HR             | 3000        | 8000            |
| 105         | Rohit         | HR             | 3000        | 8000            |
| 107         | Preet         | HR             | 7000        | 8000            |
| 114         | Manisha       | HR             | 3000        | 8000            |
| 117         | Adarsh        | HR             | 3500        | 8000            |
| 119         | Cory          | HR             | 8000        | 8000            |
| 103         | Akbar         | IT             | 4000        | 11000           |
| 109         | Sanjay        | IT             | 6500        | 11000           |
| 110         | Vasudha       | IT             | 7000        | 11000           |
| 111         | Melinda       | IT             | 8000        | 11000           |
| 112         | Komal         | IT             | 10000       | 11000           |
| 115         | Chandni       | IT             | 4500        | 11000           |
| 121         | Rosalin       | IT             | 6000        | 11000           |
| 122         | Ibrahim       | IT             | 8000        | 11000           |
| 123         | Vikram        | IT             | 8000        | 11000           |
| 124         | Dheeraj       | IT             | 11000       | 11000           |
+ ----------- + ------------- + -------------- + ----------- + --------------- +
24 rows

Execute:
> select e.*,
row_number() over(partition by dept_name) as rn
from employee e

+ ----------- + ------------- + -------------- + ----------- + ------- +
| emp_ID      | emp_NAME      | DEPT_NAME      | SALARY      | rn      |
+ ----------- + ------------- + -------------- + ----------- + ------- +
| 101         | Mohan         | Admin          | 4000        | 1       |
| 108         | Maryam        | Admin          | 4000        | 2       |
| 113         | Gautham       | Admin          | 2000        | 3       |
| 120         | Monica        | Admin          | 5000        | 4       |
| 104         | Dorvin        | Finance        | 6500        | 1       |
| 106         | Rajesh        | Finance        | 5000        | 2       |
| 116         | Satya         | Finance        | 6500        | 3       |
| 118         | Tejaswi       | Finance        | 5500        | 4       |
| 102         | Rajkumar      | HR             | 3000        | 1       |
| 105         | Rohit         | HR             | 3000        | 2       |
| 107         | Preet         | HR             | 7000        | 3       |
| 114         | Manisha       | HR             | 3000        | 4       |
| 117         | Adarsh        | HR             | 3500        | 5       |
| 119         | Cory          | HR             | 8000        | 6       |
| 103         | Akbar         | IT             | 4000        | 1       |
| 109         | Sanjay        | IT             | 6500        | 2       |
| 110         | Vasudha       | IT             | 7000        | 3       |
| 111         | Melinda       | IT             | 8000        | 4       |
| 112         | Komal         | IT             | 10000       | 5       |
| 115         | Chandni       | IT             | 4500        | 6       |
| 121         | Rosalin       | IT             | 6000        | 7       |
| 122         | Ibrahim       | IT             | 8000        | 8       |
| 123         | Vikram        | IT             | 8000        | 9       |
| 124         | Dheeraj       | IT             | 11000       | 10      |
+ ----------- + ------------- + -------------- + ----------- + ------- +
24 rows

Execute:
> with cte as (
           select *,row_number() over(partition by dept_name order by emp_id) as rn from employee)
            select * from cte where rn<3

+ ----------- + ------------- + -------------- + ----------- + ------- +
| emp_ID      | emp_NAME      | DEPT_NAME      | SALARY      | rn      |
+ ----------- + ------------- + -------------- + ----------- + ------- +
| 101         | Mohan         | Admin          | 4000        | 1       |
| 108         | Maryam        | Admin          | 4000        | 2       |
| 104         | Dorvin        | Finance        | 6500        | 1       |
| 106         | Rajesh        | Finance        | 5000        | 2       |
| 102         | Rajkumar      | HR             | 3000        | 1       |
| 105         | Rohit         | HR             | 3000        | 2       |
| 103         | Akbar         | IT             | 4000        | 1       |
| 109         | Sanjay        | IT             | 6500        | 2       |
+ ----------- + ------------- + -------------- + ----------- + ------- +
8 rows

Execute:
> select * from (
	select e.*,
	row_number() over(partition by dept_name order by emp_id) as rn
	from employee e) x
where x.rn < 3

+ ----------- + ------------- + -------------- + ----------- + ------- +
| emp_ID      | emp_NAME      | DEPT_NAME      | SALARY      | rn      |
+ ----------- + ------------- + -------------- + ----------- + ------- +
| 101         | Mohan         | Admin          | 4000        | 1       |
| 108         | Maryam        | Admin          | 4000        | 2       |
| 104         | Dorvin        | Finance        | 6500        | 1       |
| 106         | Rajesh        | Finance        | 5000        | 2       |
| 102         | Rajkumar      | HR             | 3000        | 1       |
| 105         | Rohit         | HR             | 3000        | 2       |
| 103         | Akbar         | IT             | 4000        | 1       |
| 109         | Sanjay        | IT             | 6500        | 2       |
+ ----------- + ------------- + -------------- + ----------- + ------- +
8 rows

Execute:
> select * from (
	select e.*,
	rank() over(partition by dept_name order by salary desc) as rnk
	from employee e) x
where x.rnk < 4

+ ----------- + ------------- + -------------- + ----------- + -------- +
| emp_ID      | emp_NAME      | DEPT_NAME      | SALARY      | rnk      |
+ ----------- + ------------- + -------------- + ----------- + -------- +
| 120         | Monica        | Admin          | 5000        | 1        |
| 101         | Mohan         | Admin          | 4000        | 2        |
| 108         | Maryam        | Admin          | 4000        | 2        |
| 104         | Dorvin        | Finance        | 6500        | 1        |
| 116         | Satya         | Finance        | 6500        | 1        |
| 118         | Tejaswi       | Finance        | 5500        | 3        |
| 119         | Cory          | HR             | 8000        | 1        |
| 107         | Preet         | HR             | 7000        | 2        |
| 117         | Adarsh        | HR             | 3500        | 3        |
| 124         | Dheeraj       | IT             | 11000       | 1        |
| 112         | Komal         | IT             | 10000       | 2        |
| 111         | Melinda       | IT             | 8000        | 3        |
| 122         | Ibrahim       | IT             | 8000        | 3        |
| 123         | Vikram        | IT             | 8000        | 3        |
+ ----------- + ------------- + -------------- + ----------- + -------- +
14 rows

Execute:
> select e.*,
rank() over(partition by dept_name order by salary desc) as rnk,
dense_rank() over(partition by dept_name order by salary desc) as dense_rnk,
row_number() over(partition by dept_name order by salary desc) as rn
from employee e

+ ----------- + ------------- + -------------- + ----------- + -------- + -------------- + ------- +
| emp_ID      | emp_NAME      | DEPT_NAME      | SALARY      | rnk      | dense_rnk      | rn      |
+ ----------- + ------------- + -------------- + ----------- + -------- + -------------- + ------- +
| 120         | Monica        | Admin          | 5000        | 1        | 1              | 1       |
| 101         | Mohan         | Admin          | 4000        | 2        | 2              | 2       |
| 108         | Maryam        | Admin          | 4000        | 2        | 2              | 3       |
| 113         | Gautham       | Admin          | 2000        | 4        | 3              | 4       |
| 104         | Dorvin        | Finance        | 6500        | 1        | 1              | 1       |
| 116         | Satya         | Finance        | 6500        | 1        | 1              | 2       |
| 118         | Tejaswi       | Finance        | 5500        | 3        | 2              | 3       |
| 106         | Rajesh        | Finance        | 5000        | 4        | 3              | 4       |
| 119         | Cory          | HR             | 8000        | 1        | 1              | 1       |
| 107         | Preet         | HR             | 7000        | 2        | 2              | 2       |
| 117         | Adarsh        | HR             | 3500        | 3        | 3              | 3       |
| 102         | Rajkumar      | HR             | 3000        | 4        | 4              | 4       |
| 105         | Rohit         | HR             | 3000        | 4        | 4              | 5       |
| 114         | Manisha       | HR             | 3000        | 4        | 4              | 6       |
| 124         | Dheeraj       | IT             | 11000       | 1        | 1              | 1       |
| 112         | Komal         | IT             | 10000       | 2        | 2              | 2       |
| 111         | Melinda       | IT             | 8000        | 3        | 3              | 3       |
| 122         | Ibrahim       | IT             | 8000        | 3        | 3              | 4       |
| 123         | Vikram        | IT             | 8000        | 3        | 3              | 5       |
| 110         | Vasudha       | IT             | 7000        | 6        | 4              | 6       |
| 109         | Sanjay        | IT             | 6500        | 7        | 5              | 7       |
| 121         | Rosalin       | IT             | 6000        | 8        | 6              | 8       |
| 115         | Chandni       | IT             | 4500        | 9        | 7              | 9       |
| 103         | Akbar         | IT             | 4000        | 10       | 8              | 10      |
+ ----------- + ------------- + -------------- + ----------- + -------- + -------------- + ------- +
24 rows

Execute:
> select 
     e.*,
     lag(salary) over(partition by dept_name order by emp_id) as prev_empl_sal,
     case when e.salary>lag(salary) over(partition by dept_name order by emp_id) then 'Higher than previous employee'
     when e.salary<lag(salary) over(partition by dept_name order by emp_id) then 'lower than previous employee'
     when e.salary=lag(salary) over(partition by dept_name order by emp_id) then 'equal to previous employee'
     end as sal_range
     from employee e

+ ----------- + ------------- + -------------- + ----------- + ------------------ + -------------- +
| emp_ID      | emp_NAME      | DEPT_NAME      | SALARY      | prev_empl_sal      | sal_range      |
+ ----------- + ------------- + -------------- + ----------- + ------------------ + -------------- +
| 101         | Mohan         | Admin          | 4000        |                    |                |
| 108         | Maryam        | Admin          | 4000        | 4000               | equal to previous employee |
| 113         | Gautham       | Admin          | 2000        | 4000               | lower than previous employee |
| 120         | Monica        | Admin          | 5000        | 2000               | Higher than previous employee |
| 104         | Dorvin        | Finance        | 6500        |                    |                |
| 106         | Rajesh        | Finance        | 5000        | 6500               | lower than previous employee |
| 116         | Satya         | Finance        | 6500        | 5000               | Higher than previous employee |
| 118         | Tejaswi       | Finance        | 5500        | 6500               | lower than previous employee |
| 102         | Rajkumar      | HR             | 3000        |                    |                |
| 105         | Rohit         | HR             | 3000        | 3000               | equal to previous employee |
| 107         | Preet         | HR             | 7000        | 3000               | Higher than previous employee |
| 114         | Manisha       | HR             | 3000        | 7000               | lower than previous employee |
| 117         | Adarsh        | HR             | 3500        | 3000               | Higher than previous employee |
| 119         | Cory          | HR             | 8000        | 3500               | Higher than previous employee |
| 103         | Akbar         | IT             | 4000        |                    |                |
| 109         | Sanjay        | IT             | 6500        | 4000               | Higher than previous employee |
| 110         | Vasudha       | IT             | 7000        | 6500               | Higher than previous employee |
| 111         | Melinda       | IT             | 8000        | 7000               | Higher than previous employee |
| 112         | Komal         | IT             | 10000       | 8000               | Higher than previous employee |
| 115         | Chandni       | IT             | 4500        | 10000              | lower than previous employee |
| 121         | Rosalin       | IT             | 6000        | 4500               | Higher than previous employee |
| 122         | Ibrahim       | IT             | 8000        | 6000               | Higher than previous employee |
| 123         | Vikram        | IT             | 8000        | 8000               | equal to previous employee |
| 124         | Dheeraj       | IT             | 11000       | 8000               | Higher than previous employee |
+ ----------- + ------------- + -------------- + ----------- + ------------------ + -------------- +
24 rows

Execute:
> select e.*,
lag(salary) over(partition by dept_name order by emp_id) as prev_empl_sal,
lead(salary) over(partition by dept_name order by emp_id) as next_empl_sal
from employee e

+ ----------- + ------------- + -------------- + ----------- + ------------------ + ------------------ +
| emp_ID      | emp_NAME      | DEPT_NAME      | SALARY      | prev_empl_sal      | next_empl_sal      |
+ ----------- + ------------- + -------------- + ----------- + ------------------ + ------------------ +
| 101         | Mohan         | Admin          | 4000        |                    | 4000               |
| 108         | Maryam        | Admin          | 4000        | 4000               | 2000               |
| 113         | Gautham       | Admin          | 2000        | 4000               | 5000               |
| 120         | Monica        | Admin          | 5000        | 2000               |                    |
| 104         | Dorvin        | Finance        | 6500        |                    | 5000               |
| 106         | Rajesh        | Finance        | 5000        | 6500               | 6500               |
| 116         | Satya         | Finance        | 6500        | 5000               | 5500               |
| 118         | Tejaswi       | Finance        | 5500        | 6500               |                    |
| 102         | Rajkumar      | HR             | 3000        |                    | 3000               |
| 105         | Rohit         | HR             | 3000        | 3000               | 7000               |
| 107         | Preet         | HR             | 7000        | 3000               | 3000               |
| 114         | Manisha       | HR             | 3000        | 7000               | 3500               |
| 117         | Adarsh        | HR             | 3500        | 3000               | 8000               |
| 119         | Cory          | HR             | 8000        | 3500               |                    |
| 103         | Akbar         | IT             | 4000        |                    | 6500               |
| 109         | Sanjay        | IT             | 6500        | 4000               | 7000               |
| 110         | Vasudha       | IT             | 7000        | 6500               | 8000               |
| 111         | Melinda       | IT             | 8000        | 7000               | 10000              |
| 112         | Komal         | IT             | 10000       | 8000               | 4500               |
| 115         | Chandni       | IT             | 4500        | 10000              | 6000               |
| 121         | Rosalin       | IT             | 6000        | 4500               | 8000               |
| 122         | Ibrahim       | IT             | 8000        | 6000               | 8000               |
| 123         | Vikram        | IT             | 8000        | 8000               | 11000              |
| 124         | Dheeraj       | IT             | 11000       | 8000               |                    |
+ ----------- + ------------- + -------------- + ----------- + ------------------ + ------------------ +
24 rows

