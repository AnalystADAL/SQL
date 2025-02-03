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
