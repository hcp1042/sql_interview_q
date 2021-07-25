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
