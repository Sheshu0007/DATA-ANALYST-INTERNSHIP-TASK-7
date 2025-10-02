# DATA-ANALYST-INTERNSHIP-TASK-7
# Task 7: Basic Sales Summary from SQLite Database

## Objective

Use SQL inside Python to pull simple sales information (like total quantity sold, total revenue) from a SQLite database, and display it using basic print statements and visualizations.

## Tools & Libraries

* Python (>=3.8 recommended)
* SQLite (built into Python via `sqlite3`)
* Pandas (`pip install pandas`)
* Matplotlib (`pip install matplotlib`)
* Jupyter Notebook or a `.py` file

## Dataset

* **Database:** `sales_data.db`

* **Table:** `sales`

* **Columns:**

  * `id` → INTEGER, Primary Key, Auto-increment
  * `product_name` → VARCHAR, Not Null
  * `product_price` → INT, Not Null
  * `p_quantity` → INT
  * `total_price` → INT

* **Sample Data:**

| product_name | product_price | p_quantity | total_price |
| ------------ | ------------- | ---------- | ----------- |
| Laptop       | 750           | 2          | 1500        |
| Mouse        | 20            | 5          | 100         |
| Keyboard     | 50            | 3          | 150         |
| Monitor      | 200           | 2          | 400         |
| USB Cable    | 10            | 10         | 100         |

## Steps / Workflow

1. **Connect to SQLite database**

```python
import sqlite3
conn = sqlite3.connect("sales_data.db")
```

2. **Create sales table (if not exists)**

```sql
CREATE TABLE IF NOT EXISTS sales(
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    product_name VARCHAR NOT NULL,
    product_price INT NOT NULL,
    p_quantity INT,
    total_price INT
)
```

3. **Insert sample data** (optional, only if table is empty)

```sql
INSERT INTO sales (product_name, product_price, p_quantity, total_price)
VALUES ('Laptop', 750, 2, 1500), ...;
```

4. **Run SQL query for sales summary**

```sql
SELECT product_name AS product,
       SUM(p_quantity) AS total_qty,
       SUM(total_price) AS revenue
FROM sales
GROUP BY product_name
```

5. **Load query result into pandas**

```python
import pandas as pd
df = pd.read_sql_query(query, conn)
print(df)
```

6. **Visualize data using matplotlib**

* **Bar chart:** Revenue by product
* **Bar chart:** Quantity sold by product
* **Pie chart:** Revenue share by product

```python
import matplotlib.pyplot as plt
df.plot(kind='bar', x='product', y='revenue')
plt.show()
```

7. **Close database connection**

```python
conn.close()
```

## Deliverables

1. `sales_data.db` → SQLite database file
2. Python script / Jupyter notebook (`sales_summary.py` or `sales_summary.ipynb`)
3. Bar chart and pie chart visualizations (can be saved as PNG if required)

## Additional Features

* Calculates **overall totals**: total quantity sold & total revenue
* Identifies **highest revenue product**
* Displays **revenue contribution per product** using pie chart
