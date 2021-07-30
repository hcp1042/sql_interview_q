511 Game Analysis

```sql
SELECT player_id, min(event_date) as first_login
FROM activity
GROUP BY 1
ORDER BY 1
```


512

```sql
SELECT activity.player_id, device_id
FROM activity
JOIN
(SELECT player_id, min(event_date)
FROM activity
GROUP BY 1) first_login
ON activity.player_id = first_login.player_id
AND activity.event_date = first_login.event_date
```
 or window function rank() can be used  (partition by player_id
 
 
 534
 
 ```sql
 SELECT player_id, event_date,
 sum(games_played) (PARTITION BY player_id ORDER BY event_date) as game_played_so_far
 FROM activity
 ORDER BY 1,2
 
 ```
 
  550
 
 ```sql
 (SELECT player_id, min(event_date) as first_login_date 
 FROM activity
 GROUP BY 1) a
 JOIN
 activity b
 ON a.player_id = b.player_id
 AND a.first_login_date + interval('1 day') = b.event_date
 ```
 
 tips:
 SELECT ROUND(COUNT(DISTINCT b.player_id)/COUNT(DISTINCT a.player_id), 2) AS fraction FROM Activity AS a
LEFT JOIN

 
 
 **7/27**
 
 
 577
 
 ```sql
 SELECT name, bonus
 FROM employee
 LEFT JOIN bonus
 ON employee.empid = bonus.empid
 WHERE bonus < 1000
 or bonus IS NULL
 
 
 ```
 
 
 574
 ```sql

SELECT a.name
FROM candidate a
JOIN
(SELECT candidate_id, count(id)
FROM vote
LIMIT 1
GROUP BY 2
ORDER BY count(id) Desc) sub      -- can use count() for sorting and not select count(id)
on a.id = b.candidate_id
```



570
find manager that has at least 5 directs

```sql
SELECT emp.name
FROM employee emp
JOIN
(SELECT managerID
FROM employee
GROUP BY managerID
HAVING count(Distinct Id) >= 5) sub
ON emp.Id = sub.managerID

```


7/28

578

get highest answer rate question

 
 
 
580

department student number
```sql
SELECT dept.dept_name, sub.student_number
FROM department AS dept
LEFT JOIN 
(select dept_id, count(student_id) as student_number
FROM student
GROUP BY 1) sub
ON dept.dept_id = sub.dept_id
ORDER BY 2 DESC, 1
```


584

_not equal:  <>_
```sql
SELECT name
FROM customer
WHERE referral_id <> 2 
OR referral_id IS NULL


585

investment

```sql
SELECT sum(TIV_2016) as TIV_2016
FROM insurance
WHERE
TIV_2015 IN
(SELECT TIV_2015
FROM insurance
GROUP BY TIV_2015
HAVING COUNT(DISTINCT PID) > 1)
AND
CONCAT(LAT,',',LON) IN
(SELECT CONCAT(LAT,',',LON)
FROM insurance
GROUP BY CONCAT(LAT,',',LON)
 HAVING count(*)=1)
)

```
