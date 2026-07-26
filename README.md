# 🌍 SQL Functions Showcase: World Cities Dataset

![SQL](https://img.shieldsge/SQL-Advanced-blue
![Database](https://img.shields.io/badge/Databasereen
![Data Analysis](https://img.Data%20Analysis-SQL-orange

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
(456,'London','GBR','England',7285000
