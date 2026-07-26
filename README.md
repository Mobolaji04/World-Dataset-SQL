# 🌍 SQL Functions Showcase: World Cities Dataset


## 📌 Project Overview

This project demonstrates practical SQL skills using a global cities dataset containing:

- City Name
- Country Code
- District/State
- Population

The dataset includes **1,000+ cities across multiple countries**, making it ideal for practicing:

- Aggregate Functions
- Window Functions
- Ranking Functions
- String Functions
- Common Table Expressions (CTEs)
- Data Quality Checks
- Business Intelligence Queries

---

## 📊 Dataset Schema

```sql
CREATE TABLE cities (
    id INT PRIMARY KEY,
    city_name VARCHAR(100),
    country_code CHAR(3),
    district VARCHAR(100),
    population INT
);
```

### Sample Data

```sql
INSERT INTO cities VALUES
(1,'Kabul','AFG','Kabol',1780000),
(5,'Amsterdam','NLD','Noord-Holland',731200),
(69,'Buenos Aires','ARG','Distrito Federal',2982146),
(130,'Sydney','AUS','New South Wales',3276207),
(206,'São Paulo','BRA','São Paulo',9968485),
(456,'London','GBR','England',7285000),
(608,'Cairo','EGY','Kairo',6789479),
(939,'Jakarta','IDN','Jakarta Raya',9604900);
```

---

# 🔍 Basic Querying

## Retrieve Cities from the UK

```sql
SELECT city_name, population
FROM cities
WHERE country_code = 'GBR';
```

## Cities with Population Above 1 Million

```sql
SELECT city_name,
       country_code,
       population
FROM cities
WHERE population > 1000000;
```

---

# 📈 Aggregate Functions

## Total Population per Country

```sql
SELECT country_code,
       SUM(population) AS total_population
FROM cities
GROUP BY country_code
ORDER BY total_population DESC;
```

## Average Population per Country

```sql
SELECT country_code,
       AVG(population) AS avg_population
FROM cities
GROUP BY country_code
ORDER BY avg_population DESC;
```

## Largest City by Country

```sql
SELECT country_code,
       MAX(population) AS largest_city
FROM cities
GROUP BY country_code;
```

## Smallest City by Country

```sql
SELECT country_code,
       MIN(population) AS smallest_city
FROM cities
GROUP BY country_code;
```

---

# 📊 GROUP BY Analysis

## Number of Cities per Country

```sql
SELECT country_code,
       COUNT(*) AS city_count
FROM cities
GROUP BY country_code
ORDER BY city_count DESC;
```

## Total Population by District

```sql
SELECT district,
       SUM(population) AS district_population
FROM cities
GROUP BY district
ORDER BY district_population DESC;
```

---

# 🏆 Ranking Functions

## Top 10 Most Populated Cities

```sql
SELECT city_name,
       country_code,
       population,
       RANK() OVER(
           ORDER BY population DESC
       ) AS city_rank
FROM cities
LIMIT 10;
```

## Largest City in Each Country

```sql
SELECT *
FROM (
    SELECT city_name,
           country_code,
           population,
           ROW_NUMBER() OVER(
               PARTITION BY country_code
               ORDER BY population DESC
           ) AS rn
    FROM cities
) ranked
WHERE rn = 1;
```

---

# ⚡ Window Functions

## Running Population Total

```sql
SELECT country_code,
       city_name,
       population,
       SUM(population) OVER(
           PARTITION BY country_code
           ORDER BY population
       ) AS running_total
FROM cities;
```

## Compare Cities to Country Average

```sql
SELECT city_name,
       country_code,
       population,
       AVG(population) OVER(
           PARTITION BY country_code
       ) AS country_avg
FROM cities;
```

---

# 🔤 String Functions

## Convert City Names to Uppercase

```sql
SELECT UPPER(city_name) AS city_name
FROM cities;
```

## Cities Beginning with "San"

```sql
SELECT city_name
FROM cities
WHERE city_name LIKE 'San%';
```

## Length of City Names

```sql
SELECT city_name,
       LENGTH(city_name) AS character_count
FROM cities;
```

---

# 🎯 CASE Statements

## Categorize Cities by Population

```sql
SELECT city_name,
       population,
       CASE
           WHEN population >= 5000000 THEN 'Mega City'
           WHEN population >= 1000000 THEN 'Large City'
           WHEN population >= 500000 THEN 'Medium City'
           ELSE 'Small City'
       END AS city_category
FROM cities;
```

---

# 🧠 Common Table Expressions (CTEs)

## Top 5 Cities per Country

```sql
WITH ranked_cities AS (
    SELECT city_name,
           country_code,
           population,
           ROW_NUMBER() OVER(
               PARTITION BY country_code
               ORDER BY population DESC
           ) AS ranking
    FROM cities
)
SELECT *
FROM ranked_cities
WHERE ranking <= 5;
```

---

# 🚀 Advanced Analytics

## Country Share of Population

```sql
SELECT country_code,
       SUM(population) AS country_population,
       ROUND(
           SUM(population) * 100.0 /
           SUM(SUM(population)) OVER (),
           2
       ) AS population_percentage
FROM cities
GROUP BY country_code
ORDER BY population_percentage DESC;
```

## Cities Above Their Country Average

```sql
WITH country_avg AS (
    SELECT country_code,
           AVG(population) AS avg_population
    FROM cities
    GROUP BY country_code
)
SELECT c.city_name,
       c.country_code,
       c.population
FROM cities c
JOIN country_avg a
ON c.country_code = a.country_code
WHERE c.population > a.avg_population;
```

---

# ✅ Data Quality Checks

## Missing District Values

```sql
SELECT *
FROM cities
WHERE district IS NULL
   OR district = '–';
```

## Duplicate City Names

```sql
SELECT city_name,
       COUNT(*) AS occurrences
FROM cities
GROUP BY city_name
HAVING COUNT(*) > 1;
```

---

# 📚 Business Questions

## Which Countries Have the Largest Urban Populations?

```sql
SELECT country_code,
       SUM(population) AS urban_population
FROM cities
GROUP BY country_code
ORDER BY urban_population DESC;
```

## Top 20 Most Populated Cities

```sql
SELECT city_name,
       country_code,
       population
FROM cities
ORDER BY population DESC
LIMIT 20;
```

## Highest Population District

```sql
SELECT district,
       SUM(population) AS total_population
FROM cities
GROUP BY district
ORDER BY total_population DESC
LIMIT 1;
```

## Percentage of Population Living in the Largest City

```sql
WITH country_totals AS (
    SELECT country_code,
           SUM(population) AS total_population
    FROM cities
    GROUP BY country_code
),
largest_city AS (
    SELECT country_code,
           MAX(population) AS max_population
    FROM cities
    GROUP BY country_code
)
SELECT ct.country_code,
       ROUND(
           lc.max_population * 100.0 / ct.total_population,
           2
       ) AS percentage_in_largest_city
FROM country_totals ct
JOIN largest_city lc
ON ct.country_code = lc.country_code;
```

---

# 🛠 SQL Skills Demonstrated

✅ SELECT  
✅ WHERE  
✅ ORDER BY  
✅ GROUP BY  
✅ HAVING  
✅ COUNT()  
✅ SUM()  
✅ AVG()  
✅ MIN()  
✅ MAX()  
✅ CASE WHEN  
✅ LIKE  
✅ CTEs  
✅ Window Functions  
✅ ROW_NUMBER()  
✅ RANK()  
✅ PARTITION BY  
✅ Data Validation  
✅ Analytical SQL  

---

# 🎓 Key Takeaways

This project demonstrates how SQL can be used for:

- Exploratory Data Analysis (EDA)
- Business Intelligence Reporting
- Data Aggregation
- Data Quality Validation
- Population Analytics
- Customer Segmentation Techniques
- Dashboard Development
- Performance Reporting

Perfect for showcasing **Data Analyst**, **Business Intelligence**, **Analytics Engineer**, and **Data Science** SQL skills.



