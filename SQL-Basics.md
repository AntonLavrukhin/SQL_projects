 # 🌮 **Learning SQL language basics**

    **🔑 Tool: PostgreSQL 🔑**
   

### _-- Task 1. Get TOP5 the most expensive units in our products table._

```SQL
SELECT name AS product_name, price AS product_price
FROM products
ORDER BY price DESC
LIMIT 5
```

**Output:**
![Без имени](https://github.com/AntonLavrukhin/SQL_projects/assets/143402791/31797aa8-4d93-4a23-88f3-b11072fbf195)

### _-- Task 2. Get unit in our products table with the longest product name._

```SQL
SELECT name AS product_name, LENGTH(name) AS name_length, price AS product_price
FROM products
ORDER BY name_length DESC
LIMIT 1
```

**Output:**

![Без имени1](https://github.com/AntonLavrukhin/SQL_projects/assets/143402791/e77b5bdf-b25f-43d4-91e9-194d9888a85c)

### _-- Task 3. Use functions UPPER & SPLIT_PART with name column and get the first word from name column._

```SQL
SELECT name, UPPER(SPLIT_PART(name, ' ', 1)) AS first_word, price
FROM products
```

**Output:**

![Без имени2](https://github.com/AntonLavrukhin/SQL_projects/assets/143402791/871d4aa4-2d7b-469a-8f62-953d2370533a)

### _-- Task 4. Changing data type from INT to VARCHAR with two diff ways to do it._

```SQL
SELECT name, price, price :: VARCHAR AS price_char
FROM products
```

```SQL
SELECT name, price, CAST(price AS VARCHAR) AS price_char
FROM products
```

**Output:**

![Без имени3](https://github.com/AntonLavrukhin/SQL_projects/assets/143402791/c1c43910-bc48-48de-ac53-70f54b619bcb)

### _-- Task 5. Using CONCAT function and converting data type into DATE._

```SQL
SELECT CONCAT('Заказ № ', order_id, ' создан ', DATE(creation_time)) AS order_info
FROM orders
LIMIT 200
```

**Output:**

![Без имени4](https://github.com/AntonLavrukhin/SQL_projects/assets/143402791/b552e0e5-181e-446e-ac01-8b19bbc99efe)

### _-- Task 6. Filter the table and get only year of couriers from date_of_birth column using DATE_PART()._

```SQL
SELECT courier_id, DATE_PART('year', birth_date) AS birth_year
FROM couriers
ORDER BY birth_year DESC, courier_id ASC
```

**Output:**

![Без имени5](https://github.com/AntonLavrukhin/SQL_projects/assets/143402791/ab58500b-2895-470c-bd0c-1fca3af366b3)

### _-- Task 7. USING COALESCE() function to populate empty rows._

```SQL
SELECT courier_id, COALESCE(DATE_PART('year', birth_date)::VARCHAR, 'unknown') AS birth_year
FROM couriers
ORDER BY birth_year DESC, courier_id ASC
```

**Output:**

![Без имени6](https://github.com/AntonLavrukhin/SQL_projects/assets/143402791/b36981dd-f20d-4406-8ce1-29f1dbac54a3)

### _-- Task 8. Trying logical_expressions._

```SQL
SELECT product_id, name, price AS old_price, 

COALESCE((CASE 
WHEN price > 100 AND name != 'икра' THEN price * 1.05 
END), price)  AS  new_price

FROM products

ORDER BY new_price DESC, product_id
```

**Output:**

![Без имени7](https://github.com/AntonLavrukhin/SQL_projects/assets/143402791/439c8d11-0442-4387-9f41-a345b7bd2879)

