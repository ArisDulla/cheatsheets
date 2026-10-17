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
---
---

## 3. Aggregate Functions

### PARTITION BY category

| title     | category  | year |  SUM |    AVG | COUNT |  MIN |  MAX |
| --------- | --------- | ---: | ---: | -----: | ----: | ---: | ---: |
| Brave     | Adventure | 2012 | 4023 | 2011.5 |     2 | 2011 | 2012 |
| WALL-E    | Adventure | 2011 | 4023 | 2011.5 |     2 | 2011 | 2012 |
| Up        | Animation | 2009 | 6024 | 2008.0 |     3 | 2006 | 2009 |
| Toy Story | Animation | 2009 | 6024 | 2008.0 |     3 | 2006 | 2009 |
| Cars      | Animation | 2006 | 6024 | 2008.0 |     3 | 2006 | 2009 |


# SUM() OVER () - Calculates the total across all rows.
```sql 
SELECT
    title,
    year,
    SUM(year) OVER () AS total_years
FROM movies;
```
# with partition
```sql 
SUM(year) OVER ( PARTITION BY category ) 
```

# AVG() OVER () - Calculates the average across all rows.
```sql 
SELECT
    title,
    year,
    AVG(year) OVER () AS average_year
FROM movies;
```
# with partition
```sql 
AVG(year) OVER (PARTITION BY category)
```

# COUNT() OVER () - Counts all rows.
```sql 
SELECT
    title,
    year,
    COUNT(*) OVER () AS total_movies
FROM movies;
```

# with partition
```sql 
COUNT(*) OVER (
        PARTITION BY category
    ) AS category_count
```

# MIN() OVER () - Finds the minimum value across all rows.
```sql 
SELECT
    title,
    year,
    MIN(year) OVER () AS minimum_year
FROM movies;
```

# with partition
```sql 
MIN(year) OVER (
        PARTITION BY category
    )
```

# MAX() OVER () - Finds the maximum value across all rows.
```sql 
SELECT
    title,
    year,
    MAX(year) OVER () AS maximum_year
FROM movies;
```

# with partition
```sql 
MAX(year) OVER (
        PARTITION BY category
    )
```


---
---

## 4. Distribution Functions

| **title** | **category** | **year** | **percent_rank** | **cumulative_dist** |
|:---|:---|---:|---:|---:|
| **Brave** | **Adventure** | **2012** | **1.00** | **1.00** |
| **WALL-E** | **Adventure** | **2011** | **0.00** | **0.50** |
| **Up** | **Animation** | **2009** | **0.50** | **1.00** |
| **Toy Story** | **Animation** | **2009** | **0.50** | **1.00** |
| **Cars** | **Animation** | **2006** | **0.00** | **0.33** |

# PERCENT_RANK() — Calculates the relative rank of a row as a percentage.

```sql 
SELECT
    title,
    year,
    PERCENT_RANK() OVER (
        ORDER BY year
    ) AS percent_rank
FROM movies;
```
| **title** | **year** | **percent_rank** |
|---|---:|---:|
| **Cars** | **2006** | **0.00** |
| **Up** | **2009** | **0.25** |
| **Toy Story** | **2009** | **0.25** |
| **WALL-E** | **2011** | **0.75** |
| **Brave** | **2012** | **1.00** |

# with partition
```sql 
PERCENT_RANK() OVER (
        PARTITION BY category
        ORDER BY year
    )
```
| **title** | **category** | **year** | **percent_rank** |
|:---|:---|---:|---:|
| **WALL-E** | **Adventure** | **2011** | **0.00** |
| **Brave** | **Adventure** | **2012** | **1.00** |
| **Cars** | **Animation** | **2006** | **0.00** |
| **Up** | **Animation** | **2009** | **0.50** |
| **Toy Story** | **Animation** | **2009** | **0.50** |

# CUME_DIST() — Calculates the cumulative distribution of a row.
```sql 
SELECT
    title,
    year,
    CUME_DIST() OVER (
        ORDER BY year
    ) AS cumulative_dist
FROM movies;
```
| **title** | **category** | **year** | **cumulative_dist** |
|---|---|---:|---:|
| **Cars** | **Animation** | **2006** | **0.20** |
| **Up** | **Animation** | **2009** | **0.60** |
| **Toy Story** | **Animation** | **2009** | **0.60** |
| **WALL-E** | **Adventure** | **2011** | **0.80** |
| **Brave** | **Adventure** | **2012** | **1.00** |

# with partition
```sql 
CUME_DIST() OVER (
        PARTITION BY category
        ORDER BY year
    ) AS cumulative_dist
```
| **title** | **category** | **year** | **cumulative_dist** |
|---|---|---:|---:|
| **WALL-E** | **Adventure** | **2011** | **0.50** |
| **Brave** | **Adventure** | **2012** | **1.00** |
| **Cars** | **Animation** | **2006** | **0.33** |
| **Up** | **Animation** | **2009** | **1.00** |
| **Toy Story** | **Animation** | **2009** | **1.00** |

# PERCENTILE_CONT() — Calculates a continuous percentile using interpolation.
```sql 
SELECT
    category,
    PERCENTILE_CONT(0.5) WITHIN GROUP (
        ORDER BY year
    ) AS median_year
FROM movies
GROUP BY category;
```
(It can return a value that does not exist in the dataset.)
| **category** | **median_year** |
|---|---:|
| **Adventure** | **2011.5** | 
| **Animation** | **2009** |

# PERCENTILE_DISC() — Calculates a discrete percentile by returning an existing value.
```sql 
SELECT
    PERCENTILE_DISC(0.5) WITHIN GROUP (
        ORDER BY year
    ) AS median_year
FROM movies;
```
| **median_year** |
|---:|
| **2009** |

```sql 
SELECT
    category,
    PERCENTILE_DISC(0.5) WITHIN GROUP (
        ORDER BY year
    ) AS median_year
FROM movies
GROUP BY category;
```
| **category** | **median_year** |
|---|---:|
| **Adventure** | **2011** |
| **Animation** | **2009** |