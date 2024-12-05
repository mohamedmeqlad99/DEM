# Views in Databricks

Views in Databricks are logical tables created by defining a query on existing tables, but without storing physical data. They are especially useful for simplifying complex queries, organizing data, enhancing readability, and sharing common data definitions across teams and projects. Below, we outline the key types of views and their use cases.

---

## Types of Views

Databricks supports two main types of views:
1. **Temporary Views**
2. **Global Temporary Views**

### 1. Temporary Views
- **Scope**: Limited to the session in which they are created.
- **Creation Syntax**: 
    ```sql
    CREATE OR REPLACE TEMP VIEW view_name AS 
    SELECT columns 
    FROM table_name 
    WHERE conditions;
    ```
- **Use Cases**: Temporary views are best suited for exploratory analysis, intermediate calculations, or when you need a view to hold results temporarily without persisting data.

### 2. Global Temporary Views
- **Scope**: Available across multiple sessions within the same cluster.
- **Creation Syntax**:
    ```sql
    CREATE OR REPLACE GLOBAL TEMP VIEW view_name AS 
    SELECT columns 
    FROM table_name 
    WHERE conditions;
    ```
- **Use Cases**: Ideal for sharing data across different notebooks and sessions within the same cluster. Useful for cluster-wide calculations or reference data that might be reused often.

---

## Benefits of Using Views

1. **Simplified Querying**: Views encapsulate complex SQL logic, making it easier to reuse and maintain code.
2. **Data Security**: Views allow restriction of access to sensitive columns while allowing access to the rest of the table.
3. **Logical Abstraction**: Views create an abstraction layer between the actual table and querying user, so underlying data structure changes won’t impact all queries.
4. **Data Consistency**: Views can provide a consistent view of data by filtering out or transforming underlying data as needed.

---

## Managing Views in Databricks

- **Updating Views**: Use the `CREATE OR REPLACE` syntax to modify a view without first dropping it. This is particularly helpful when views are widely used in other queries or dashboards.
- **Dropping Views**: To remove a view, use:
    ```sql
    DROP VIEW IF EXISTS view_name;
    ```
- **Accessing Global Views**: Global temporary views are accessible through the `global_temp` database. To query a global view, specify the `global_temp` prefix:
    ```sql
    SELECT * FROM global_temp.view_name;
    ```

---

## Best Practices for Using Views

- **Name Views Descriptively**: Use a naming convention that clearly indicates the purpose of the view, e.g., `sales_summary_monthly`.
- **Avoid Over-Nesting**: Too many nested views can lead to performance issues. Instead, materialize data when possible if views are complex and frequently accessed.
- **Access Control**: Set appropriate permissions on views to control data access, especially when sensitive data is involved.

---

## Example: Creating and Using Views

Let’s walk through creating a simple view for customer orders.

### Creating a Temporary View
```sql
CREATE OR REPLACE TEMP VIEW customer_orders AS
SELECT customer_id, COUNT(order_id) AS total_orders
FROM orders
GROUP BY customer_id;
