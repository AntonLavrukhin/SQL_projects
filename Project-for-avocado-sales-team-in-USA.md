# 🥑🥑🥑 **Inspecting Avocado sales in USA (New York vs San Francisco)**

    **🔑 Tool: ClickHouse via Redash🔑**
   

### _-- Task 1. Avocado NY, SF type share._

```SQL
SELECT region, type, total

FROM

(select region, type, SUM(total_volume) as total

from

(select region, type, SUM(total_volume) AS total_volume

from default.avocado


GROUP BY region, type

ORDER BY total_volume DESC)

GROUP BY region, type

ORDER BY total DESC

)

WHERE region IN ('SanFrancisco', 'NewYork')

GROUP BY region, type, total

ORDER BY total DESC
```

**Output:**
![Без имени12](https://github.com/AntonLavrukhin/SQL_projects/assets/143402791/c42c15fe-b14c-44fc-a0b8-35ed6d97a224)

![Без имени13](https://github.com/AntonLavrukhin/SQL_projects/assets/143402791/1ccb8214-40e9-417c-98c9-876341abff99)

### _-- Task 2. NY, SF total_volume time line by month._

```SQL
SELECT toStartOfMonth(date) AS by_month, year, region, SUM(total_volume) AS total_v

FROM

(select date, year, region, type, SUM(total_volume) AS total_volume

from default.avocado

--WHERE region != 'TotalUS' 

GROUP BY date, year, region, type

ORDER BY total_volume DESC)

WHERE region IN ('SanFrancisco', 'NewYork')

GROUP BY toStartOfMonth(date), year, region

ORDER BY total_v DESC
```

**Output:**
![Без имени14](https://github.com/AntonLavrukhin/SQL_projects/assets/143402791/b1947014-c5e3-4cc5-ba63-0f732298f83c)

### _-- Task 3. Average price per unit in compare with total US for New York & San Francisco by month & year._

```SQL
SELECT toStartOfMonth(date) AS by_month, region, AVG(average_price) AS total_avg

FROM 

(select date, year, region, type, average_price

from default.avocado)

WHERE region IN ('SanFrancisco', 'NewYork', 'TotalUS')

GROUP BY toStartOfMonth(date) AS by_month, region

ORDER BY total_avg DESC
```

**Output:**

![Без имени15](https://github.com/AntonLavrukhin/SQL_projects/assets/143402791/5568a987-4dae-4d59-8fe1-f179329c5f81)

### _-- Task 4. Organic type sales volume by month & week._

```SQL
SELECT CAST(date AS date), total_volume, region, 
SUM(total_volume) OVER(PARTITION BY region ORDER BY year ASC ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS total

FROM avocado

WHERE region IN ('NewYork', 'SanFrancisco') AND type = 'organic'
```

**Output:**
![Без имени16](https://github.com/AntonLavrukhin/SQL_projects/assets/143402791/cc34d6e2-a7fa-4c5c-826c-b5ac13d5454c)

### _-- Task 5. Final DASHBOARD._

https://redash.lab.karpov.courses/dashboards/4264-sales_team_avocado_usa

![Без имени17](https://github.com/AntonLavrukhin/SQL_projects/assets/143402791/49b8cf0d-4aa4-4f5d-84f9-f3e4fe848377)
![Без имени18](https://github.com/AntonLavrukhin/SQL_projects/assets/143402791/c78fa390-e91c-4b7d-9a81-c965bb7a9109)
![Без имени19](https://github.com/AntonLavrukhin/SQL_projects/assets/143402791/e6367a3d-bae0-4acd-a3c9-242adfcf0954)
![Без имени20](https://github.com/AntonLavrukhin/SQL_projects/assets/143402791/2d63cd56-c443-499b-b197-cd7dc6ff9fd2)


