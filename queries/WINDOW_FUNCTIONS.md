# Window Functions

## 1. Ranking Functions

| **year** | **ROW_NUMBER** | **RANK**    | **DENSE_RANK** | **PARTITION**  | **category**   | **NTILE**      |
| -------: | -------------: | -------:    | -------------: | -------------: | -------------: | -------------: |
| **year** | **ro_number**  | **ranking** | **den_rank**   | **part_rank**  | **category**   | **group_num**  |
|     2012 |              1 |           1 |              1 |              1 | Adventure      |              1 |
|     2009 |              2 |           2 |              2 |              2 | Adventure      |              1 |
|     2011 |              3 |           2 |              2 |              1 | Animation      |              2 |
|     2009 |              4 |           4 |              3 |              2 | Animation      |              2 |
|     2006 |              5 |           5 |              4 |              3 | Animation      |              3 |


## ROW_NUMBER() - Assign a row number based on year, newest first
---
```sql
SELECT
    title,
    year,
    ROW_NUMBER() OVER (ORDER BY year DESC) AS ro_number
FROM movies;
```
---
## RANK() - Assigns the same rank to tied rows and leaves gaps after ties.

```sql
SELECT
    title,
    category,
    year,
    RANK() OVER (
        ORDER BY year DESC
    ) AS ranking
FROM movies;
```
---
## DENSE_RANK() - Assigns the same rank to tied rows without leaving gaps.

```sql
SELECT
    title,
    category,
    year,
    DENSE_RANK() OVER (
        ORDER BY year DESC
    ) AS den_rank
FROM movies;
```
---
## PARTITION - Rank movies within each category, newest first, without merging rows(PARTITION)

```sql
SELECT
    title,
    category,
    year,
    ROW_NUMBER() OVER (
        PARTITION BY category
        ORDER BY year DESC
    ) AS part_rank
FROM movies;
```

## NTILE() - Divides rows into approximately equal groups.
```sql 
SELECT
    title,
    year,
    NTILE(3) OVER (ORDER BY year DESC) AS group_num
FROM movies;
```
---
---

## 2. Navigation Functions & Value Functions

| **year** | **LAG** | **LEAD** | **FIRST_VALUE** | **LAST_VALUE** | **NTH_VALUE(3)** |
| -------: | ------: | -------: | --------------: | -------------: | ---------------: |
|     2015 |    NULL |     2014 |            2015 |           2006 |             NULL |
|     2014 |    2015 |     2011 |            2015 |           2006 |             NULL |
|     2011 |    2014 |     2010 |            2015 |           2006 |             2011 |
|     2010 |    2011 |     2006 |            2015 |           2006 |             2011 |
|     2006 |    2010 |     NULL |            2015 |           2006 |             2011 |

# LAG() → previous value
```sql 
SELECT
    title,
    year,
    LAG(year) OVER (ORDER BY year DESC) AS previous_year
FROM movies;
```

# LEAD() → next value
```sql 
SELECT
    title,
    year,
    LEAD(year) OVER (ORDER BY year DESC) AS next_year
FROM movies;
```

# FIRST_VALUE()  → first value 
```sql 
SELECT
    title,
    year,
    FIRST_VALUE(year) OVER (ORDER BY year DESC) AS first_year
FROM movies;
```

# LAST_VALUE()   → last value (includes all rows in the window)
```sql 
SELECT
    title,
    year,
    LAST_VALUE(year) OVER (
        ORDER BY year DESC
        ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
    ) AS last_year
FROM movies;
```

# NTH_VALUE(3)   → 3rd value 
```sql 
SELECT
    title,
    year,
    NTH_VALUE(year, 3) OVER (ORDER BY year DESC) AS nth_year
FROM movies;
```
