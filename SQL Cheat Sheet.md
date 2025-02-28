# SQL Cheat Sheet

## Order of a SQL query execution

Here’s the order in which SQL queries are executed, from top to bottom:

```
1. FROM            - Data is fetched from the tables (or views).
2. JOIN            - Joins tables together based on the join conditions. (if applicable)
3. WHERE           - Filters rows based on conditions (before grouping).
4. GROUP BY        - Groups rows based on specified columns for aggregation.
5. HAVING          - Filters groups after aggregation (useful with GROUP BY).
6. SELECT          - Calculates the results (aggregations, columns, and aliases).
7. DISTINCT        - Removes duplicate rows (if using SELECT DISTINCT). (if applicable)
8. ORDER BY        - Sorts the result set (can use aliases here in many DBMS).
9. LIMIT/OFFSET    - Limits the number of rows returned and/or skips rows.
```

## Example SQL Query

```
SELECT column_name
FROM table_name
JOIN another_table
  ON table_name.id = another_table.id
WHERE column_name = 'value'
GROUP BY column_name
HAVING COUNT(*) > 5
ORDER BY column_name
LIMIT 10;
```

---

### 1. SQL Basics

#### Shape of a Database
- **Table**: Organises data into rows and columns.
- **Row**: Represents a single record.
- **Column**: Represents a field in the database.

Example:
```sql
SELECT DISTINCT author, genre
FROM books;
```

#### Views
Virtual tables based on SQL queries:
```sql
CREATE VIEW library_authors AS
SELECT DISTINCT author AS unique_author
FROM books;

SELECT * FROM library_authors;
```

---

### 2. Intermediate SQL

#### Aggregations
- **`COUNT`**: Counts rows or specific values.
- **`SUM`**, **`AVG`**: Sum or average numerical data.
- **`MIN`**, **`MAX`**: Find minimum or maximum values.

Example:
```sql
SELECT COUNT(*) AS total_records FROM people;
SELECT AVG(budget) AS avg_budget FROM films;
```


#### Filtering Data
- **`WHERE`**: Filter rows based on conditions.
- **Operators**: `<`, `>`, `=`, `<>`, `BETWEEN`.

Example:
```sql
SELECT title FROM films
WHERE release_year BETWEEN 1990 AND 2000;
```

#### Pattern Matching
- **`LIKE`**: Match patterns in strings.
- **Wildcards**:
  - `%`: Any sequence of characters.
  - `_`: Any single character.

Example:
```sql
SELECT name FROM people WHERE name LIKE '_r%';
```

---

### 3. Advanced SQL

#### Grouping and Ordering
- **`GROUP BY`**: Group rows by column values.
- **`ORDER BY`**: Sort rows in ascending/descending order.


Example:
```sql
SELECT release_year, COUNT(*) AS film_count
FROM films
GROUP BY release_year
ORDER BY release_year;
```


#### Combining Conditions
- Use **`AND`**, **`OR`**, and **`NOT`** to combine multiple filters.

Example:
```sql
SELECT title FROM films
WHERE (release_year = 1994 OR release_year = 2000)
AND language = 'English';
```

#### Aliases and Arithmetic
Use arithmetic in queries and alias results:
```sql
SELECT title, (duration / 60.0) AS duration_hours
FROM films;
```

---

### 4. SQL Execution Order
Understanding execution order is critical for writing efficient queries:
1. **`FROM`**: Fetch data from tables.
2. **`JOIN`**: Combine data from multiple tables.
3. **`WHERE`**: Filter rows before grouping.
4. **`GROUP BY`**: Group rows for aggregation.
5. **`HAVING`**: Filter aggregated results.
6. **`SELECT`**: Choose columns/values to return.
7. **`DISTINCT`**: Remove duplicates.
8. **`ORDER BY`**: Sort rows.
9. **`LIMIT/OFFSET`**: Restrict the number of rows returned.


### 5. Practical Examples

#### Find Movies by Decade
```sql
SELECT (MAX(release_year) - MIN(release_year)) / 10.0 AS decades
FROM films;
```

#### Calculate Revenue
```sql
SELECT SUM(gross) AS total_revenue
FROM films
WHERE release_year >= 2000;
```

#### Grouping by Certification
```sql
SELECT certification, COUNT(*) AS film_count
FROM films
