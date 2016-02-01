# Querying basics - demo

## Contents

- Accessing sample data
- SQL fundamentals demo
- SQL essentials demo
- BQ basics challenges

## Accessing sample data

Head over to the sample data descriptions within the documentation

- Share the dataset: use the drop-down arrow and select share, then select who has access. 
- To add the shared dataset
	- Drop-down: switch to project - display project - GBQnuggets.


## SQL fundamentals demo


##### 10 most popular baby names in the year 2010 in CA.

```sql
SELECT name, gender, count FROM [project:dataset.table]
WHERE year = 2010 AND state = "CA"
ORDER_BY count DESC
LIMIT 10
```

##### 10 most popular baby names in 2010 across all states

```sql
SELECT name, SUM(count) as total 
FROM [project:dataset.table]
WHERE year = 2010
GROUP_BY name
ORDER_BY total DESC
LIMIT 10
```

##### 25 most popular names in 1950s across all states

```sql
SELECT state, name, SUM(count) as total 
FROM [project.table]
WHERE year > 1950 AND year <= 1959
GROUP_BY state, name
ORDER_BY total DESC
LIMIT 25
```

##### List the total precipitation in 2000 at the San Francisco Airport.

```sql
SELECT round(SUM(total_precipitation), 2) as total_precip 
FROM [publicdata:samples.gsod]
WHERE station_number = 724940
AND year = 2000
```

##### List the average, mean, maximum gust and maximum sustained wind speeds by year and month at the Chicago airport in 2000 (station 725340)

```sql
SELECT year, month,
  ROUND(AVG(mean_wind_speed)) as avgmaxgustwindspeed, 
  ROUND(MAX(max_gust_wind_speed)) as maxgustwindspeed,
  ROUND(MAX(max_sustained_wind_speed)) as maxwind
FROM [publicdata:samples.gsod]
WHERE station_number = 725340 AND year = 2000
GROUP BY year, month
ORDER BY year, month ASC
LIMIT 12
```

##### List the 10 most recent days where it rained & thundered at London airport - 037720

```sql
SELECT year, month, day
FROM [publicdata:samples.gsod]
WHERE thunder = TRUE AND rain = TRUE AND station_number = 037720
GROUP BY year, month, day
ORDER BY year DESC, month DESC, day DESC
LIMIT 10

```

## SQL essentials demo

##### Find the 5 most popular baby names that start with the string Mi and have a length <= 5 char

```sql
SELECT name, SUM(count) as total
FROM [gbqnuggets:07QueryBasics.BabyNames] 
WHERE REGEXP_MATCH(name,r'^Mi') AND length(name) <=5
GROUP BY name
ORDER BY total DESC
LIMIT 5
```

##### Find baby names by decade (50s, 60s, 70s) that total more than 200,000 & sort by decade ascending, count descending

```sql
SELECT decade, name, SUM(count) as total
FROM 
	(SELECT name, count,
		case
			when year between 1950 AND 1960 THEN '1950s'
			when year between 1960 AND 1970 THEN '1960s'
			when year between 1970 AND 1980 THEN '1970s'
			when year between 1980 AND 1990 THEN '1980s'
		end as decade from [gbqnuggets:07QueryBasics.BabyNames]
	)
WHERE decade is not null
GROUP BY decade, name
HAVING total > 200000
ORDER BY decade ASC, total DESC
```

##### Rank the 10 most popular baby names in the year 2010 for each state

```sql
SELECT name, state, total, rank
FROM
	(SELECT name, state, SUM(count) as total,
	RANK() OVER (PARTITION by state ORDER BY total DESC) rank
	from [gbqnuggets:07QueryBasics.BabyNames]
	where year = 2010
	group by state, name)

WHERE rank <= 10
```

##### List employees who belong to a department

```sql
SELECT e.Name, d.Name as Department, hired 
FROM [gbqnuggets:07QueryBasics.Employees] e
JOIN [gbqnuggets:07QueryBasics.Departments] d ON e.DeptID = d.DeptID
```

##### List employees who do not belong to a department

```sql
SELECT e.Name, d.Name as Department, hired 
FROM [gbqnuggets:07QueryBasics.Employees] e
LEFT JOIN [gbqnuggets:07QueryBasics.Departments] d ON e.DeptID = d.DeptID
WHERE d.DeptID IS NULL
```

##### List employee departments & number of employees per department. Include department-less employees.

```sql
SELECT IFNULL(d.Name, 'N/A') as Department, COUNT(*) as numEmployees
FROM [gbqnuggets:07QueryBasics.Employees] e
LEFT JOIN [gbqnuggets:07QueryBasics.Departments] d ON e.DeptID = d.DeptID
GROUP BY Department
ORDER BY numEmployees DESC
```

##### List all months & the total numer of employees hired in each month

```sql
SELECT QUARTER(hired) as quarter, count(*) as total
FROM [gbqnuggets:07QueryBasics.Employees]
GROUP BY quarter
ORDER BY total DESC
```

or....

```sql
SELECT MONTH(hired) as month, count(*) as total
FROM [gbqnuggets:07QueryBasics.Employees]
GROUP BY month
ORDER BY month ASC
```

## BQ basics challenges

##### Find the top 100 most revised titles in the Wikipedia dataset
top function

```sql
SELECT top(title, 100), count(*) as numRevisions
FROM [publicdata:samples.wikipedia]
```

##### Find a sampling of titles (hash function) that are in the main namespace (wp_namespace=0) & contain a colon in the title

```sql
SELECT
  title,
  HASH(title) AS hash_value,
  IF(ABS(HASH(title)) % 2 == 1, 'True', 'False') 
    AS included_in_sample
FROM
  [publicdata:samples.wikipedia]
WHERE
  wp_namespace = 0 AND REGEXP_MATCH(title,r':') 
  LIMIT 10
```

##### Find the top 100 contributors (contributor_username) by revision count & filter out anything that has bot-suspicious contributors (bot in the name)

```sql
SELECT top(contributor_username, 100) as contributor, count(*) as numRevisions
FROM [publicdata:samples.wikipedia]
OMIT RECORD IF 
	REGEXP_MATCH(contributor_username,r'[Bb][Oo][Tt]') = TRUE;

```