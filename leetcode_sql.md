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
