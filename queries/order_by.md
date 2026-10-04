# ORDER BY

Ascending / Descending

Oldest → newest 
```sql
ORDER BY year ASC; or ORDER BY year;
```

Newest → oldest
```sql
ORDER BY year DESC;
```
---
The first column has priority, the next column is used when values are equal.
```sql
ORDER BY year DESC, title ASC;
```
---
Sort by calculated total
```sql
ORDER BY price * quantity DESC;
```
---
Sort by the second selected column
```sql
ORDER BY 2 ASC;
```
---
Sort by title length
```sql
ORDER BY LENGTH(title) DESC;
```
| **title** |
| --------- |
| WALL-E    |
| Brave     |
| Cars      |
| Up        |

 ---

Sort by a column alias
```sql
SELECT
    title,
    year - 2000 AS years_after_2000
FROM movies
ORDER BY years_after_2000 DESC;
```

---
Get the 5 most recent rows
```sql
ORDER BY year DESC
LIMIT 5;
```
---

Skip 10 rows and return the next 5
```sql
ORDER BY year DESC
LIMIT 5 OFFSET 10;
```
---

Sort with NULL values last (or FIRST)
```sql
ORDER BY year ASC NULLS LAST; 
```

---
Sort by a custom status order
```sql
ORDER BY CASE status
    WHEN 'active' THEN 1
    WHEN 'pending' THEN 2
END;
```
```sql
SELECT
    status,
    CASE status
        WHEN 'active' THEN 1
        WHEN 'pending' THEN 2
    END AS status_order
FROM users
ORDER BY status_order;
```
| **status** | **status_order** |
| ---------- | -------------: |
| active     |              1 |
| active     |              1 |
| pending    |              2 |
| pending    |              2 |

---
Sort available products first (boolean condition)
```sql
ORDER BY available DESC;
```

```sql
ORDER BY (status = 'active') DESC;
```

| **product** | **available** |
| ----------- | ------------- |
| Phone       | TRUE          |
| Mouse       | TRUE          |
| Laptop      | FALSE         |
| Keyboard    | FALSE         |

---

Removes duplicate values from the result.
```sql
SELECT DISTINCT director
FROM movies
ORDER BY director ASC;
```

---

Defines the rules used to compare and sort text. POSIX or C or ...
```sql
ORDER BY title COLLATE "collation_name";
```