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

# 🔍 Basic Querying

## Retrieve Cities from the UK

```sql
SELECT Name, Population
FROM city
WHERE CountryCode = 'GBR';
```

## Cities with Population Above 1 Million
<img width="651" height="573" alt="Screenshot 2026-07-27 000300" src="https://github.com/user-attachments/assets/a5d05d91-0b5e-4633-b5cb-68dfec473873" />

```sql
SELECT Name,
       country_code,
       population
FROM cities
WHERE population > 1000000;
```

---

# 📈 Aggregate Functions

## Total Population per Country

```sql
SELECT CountryCode,
       SUM(population) AS total_population
FROM city
GROUP BY CountryCode
ORDER BY total_population DESC;
```

## Average Population per Country

```sql
SELECT CountryCode,
       AVG(population) AS avg_population
FROM city
GROUP BY CountryCode
ORDER BY avg_population DESC;
```

## Largest City by Country

```sql
SELECT CountryCode,
       MAX(population) AS largest_city
FROM city
GROUP BY CountryCode;
```

## Smallest City by Country

```sql
SELECT CountryCode,
MIN(population) AS smallest_city
FROM city
GROUP BY CountryCode;
```

---

# 📊 GROUP BY Analysis

## Number of Cities per Country

```sql
SELECT CountryCode,
       COUNT(*) AS city_count
FROM city
GROUP BY CountryCode
ORDER BY city_count DESC;
```

## Total Population by District

```sql
SELECT district,
       SUM(population) AS district_population
FROM city
GROUP BY district
ORDER BY district_population DESC;
```

---

# 🏆 Ranking Functions

## Top 10 Most Populated Cities

```sql
SELECT city_name,
       CountryCode,
       population,
       RANK() OVER(
           ORDER BY population DESC
       ) AS city_rank
FROM city
LIMIT 10;
```

## Largest City in Each Country

```sql
SELECT *
FROM (
    SELECT Name,
           CountryCode,
           population,
           ROW_NUMBER() OVER(
               PARTITION BY CountryCode
               ORDER BY population DESC
           ) AS rn
    FROM city
) ranked
WHERE rn = 1;
```

---

# ⚡ Window Functions

## Running Population Total

```sql
SELECT CountryCode,
       Name,
       population,
       SUM(population) OVER(
           PARTITION BY CountryCode
           ORDER BY population
       ) AS running_total
FROM city;
```

## Compare Cities to Country Average

```sql
SELECT Name,
       CountryCode,
       population,
       AVG(population) OVER(
           PARTITION BY CountryCode
       ) AS country_avg
FROM city;
```

---

# 🔤 String Functions

## Convert City Names to Uppercase

```sql
SELECT UPPER(Name) AS Name
FROM city;
```

## Cities Beginning with "San"

```sql
SELECT Name
FROM city
WHERE Name LIKE 'San%';
```

## Length of City Names

```sql
SELECT Name,
       LENGTH(Name) AS character_count
FROM city;
```

---

# 🎯 CASE Statements

## Categorize Cities by Population

```sql
SELECT Name,
       population,
       CASE
           WHEN population >= 5000000 THEN 'Mega City'
           WHEN population >= 1000000 THEN 'Large City'
           WHEN population >= 500000 THEN 'Medium City'
           ELSE 'Small City'
       END AS city_category
FROM city;
```

---

# 🧠 Common Table Expressions (CTEs)

## Top 5 Cities per Country

```sql
WITH ranked_cities AS (
    SELECT Name,
           CountryCode,
           population,
           ROW_NUMBER() OVER(
               PARTITION BY CountryCode
               ORDER BY population DESC
           ) AS ranking
    FROM city
)
SELECT *
FROM ranked_cities
WHERE ranking <= 5;
```

---

# 🚀 Advanced Analytics

## Country Share of Population

```sql
SELECT CountryCode,
       SUM(population) AS country_population,
       ROUND(
           SUM(population) * 100.0 /
           SUM(SUM(population)) OVER (),
           2
       ) AS population_percentage
FROM city
GROUP BY CountryCode
ORDER BY population_percentage DESC;
```

## Cities Above Their Country Average

```sql
WITH country_avg AS (
    SELECT CountryCode,
           AVG(population) AS avg_population
    FROM city
    GROUP BY CountryCode
)
SELECT c.Name,
       c.CountryCode,
       c.population
FROM city c
JOIN country_avg a
ON c.CountryCode = a.CountryCode
WHERE c.population > a.avg_population;
```

---

# ✅ Data Quality Checks

## Missing District Values

```sql
SELECT *
FROM city
WHERE district IS NULL
   OR district = '–';
```

## Duplicate City Names

```sql
SELECT Name,
       COUNT(*) AS occurrences
FROM city
GROUP BY Name
HAVING COUNT(*) > 1;
```

---

# 📚 Business Questions

## Which Countries Have the Largest Urban Populations?

```sql
SELECT CountryCode,
       SUM(population) AS urban_population
FROM city
GROUP BY CountryCode
ORDER BY urban_population DESC;
```

## Top 20 Most Populated Cities

```sql
SELECT name,
       countryCode,
       population
FROM city
ORDER BY population DESC
LIMIT 20;
```

## Highest Population District

```sql
SELECT district,
       SUM(population) AS total_population
FROM city
GROUP BY district
ORDER BY total_population DESC
LIMIT 1;
```

## Percentage of Population Living in the Largest City

```sql
WITH country_totals AS (
    SELECT CountryCode,
           SUM(population) AS total_population
    FROM city
    GROUP BY CountryCode
),
largest_city AS (
    SELECT CountryCode,
           MAX(population) AS max_population
    FROM city
    GROUP BY CountryCode
)
SELECT ct.CountryCode,
       ROUND(
           lc.max_population * 100.0 / ct.total_population,
           2
       ) AS percentage_in_largest_city
FROM country_totals ct
JOIN largest_city lc
ON ct.CountryCode = lc.CountryCode;
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



