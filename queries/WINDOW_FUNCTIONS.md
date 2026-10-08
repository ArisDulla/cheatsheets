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
