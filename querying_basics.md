# Querying data basics

## Contents

- Querying fundamentals
- BigQuery SQL Basics
- BigQuery SQL Essentials

## Querying fundamentals

#### Query results

- Persisent tables -  any destination tables for your queries.
- Temporary tables - executed whenever you run a query without a destination. These expire after 24h.

#### Querying limitations

- Rate limits: 1TB & 20 queries concurrently (including 1 unlimited).
- 20,000 queries per day, 100TB processed per day.
- Maximum tables per query: 1000
- Max query length: 256Kb

#### Query priority

- Interactive query (default in the web UI): executes immediately.
- Batch queries - executes when system resources available - within 3h. At 3h, BQ escalates the query to interactive. Batch queries consume daily quote but don't consume rate limits.

#### Query caching

- BQ caches results.
- All queries that don't specify a destination talbe are cached.
- You can override the above settings in the web UI or API (useQueryCache = FALSE)
- Can check if caching was used in web UI or API (cacheHit)

#### Query costs

There are some great tools for calculating costs.

- dry_run - flag in CLI or API. Doesn't execute the query but gives you the estimated bytes processed.
- Query history exposes bytes processed.
- Cloud console (Query history-view query details or go to GCS console - overview - charges this month, then view batch analysis, processed, storage) exposes overall usages.

## BigQuery SQL Basics

#### Query syntax

Very similar to standard SQL.

- `SELECT` expressions can be literals, column names or functions.
- `FROM` can be targets or sub selects, can be multiple tables (e.g. union).
- inner, left outer and cross joins are supported.
	- union Vs join: union is akin to rbind, join is akin to merge (inner join). left outer join is akin to merge (all=TRUE).
- `WHERE` (aka predicate): conditions or data filters for a query.
- `GROUP_BY` groups rows with the same field value, helps you with aggregate functions.
- `HAVING` similar to SELECT with support for aggregate fields. Helps you filter out results.
- `ORDER BY` sorts query results, can use aliases.
- `LIMIT` limits the # of rows returned.

##### Examples

**Selecting top 10 baby names for 2010**

```
SELECT name, gender, state, count FROM [07QueryBasics.BabyNames]
WHERE year = 2010 ORDER BY count DESC LIMIT 10;
```

** Most popular baby names in New York Stage 

```
SELECT name, SUM(count) as cnt FROM [07QueryBasics.BabyNames]
WHERE state = "NY"
GROUP_BY name
HAVING cnt > 1000000
ORDER BY cnt DESC 
LIMIT 10;
```

## BigQuery SQL Essentials

- Sub queries (aka sub-selects). Selecting within the results of another query.
- Multi-selects. Selecting from a table join.
- Functions. Use the BQ query reference.
	- Standard: comparison, casting, date & time, string
	- More advanced: regex, IP, URL (e.g. extracting domain, host, tld), JSON, aggregate (max, min, mean, etc), window (functions on partitions of data - e.g. nth values, ranks), mathematical, decision making (case & if being biggest).
- Aggregate functions
	- Table functions
	- Group aggregation
	- Scoped aggregation: an addition from BQ. In the context of repeated / nested fields. e.g. within record, within known. This allows us to apply aggregate functions at different levels within the query.

#### Best practices

- Select only what you need
- Save commonly used queries as tables
- Optimise queries by using cachine
