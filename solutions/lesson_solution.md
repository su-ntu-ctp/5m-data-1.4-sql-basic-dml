# Lesson Solutions

## Basic Syntax

> Select any 3 columns from the table.

```sql
SELECT town, street_name, flat_type
FROM resale_flat_prices_2017;
```

## Operators and Functions

> Select column town as lowercase

```sql
SELECT LOWER(town)
FROM resale_flat_prices_2017;
```

> Concatenate block and street_name and return as a new column named address

```sql
SELECT CONCAT(block, ' ', street_name) AS address
FROM resale_flat_prices_2017;
```

## Filters

> Select flats with floor area greater than 100 sqm

```sql
SELECT *
FROM resale_flat_prices_2017
WHERE floor_area_sqm > 100;
```

> Select flats with resale price between 400,000 and 500,000

```sql
SELECT *
FROM resale_flat_prices_2017
WHERE resale_price BETWEEN 400000 AND 500000;
```

> Select flats with lease commence date later than year 2000 and floor area greater than 100 sqm

```sql
SELECT *
FROM resale_flat_prices_2017
WHERE lease_commence_date > 2000 AND floor_area_sqm > 100;
```

## Sorting

> Select flats from highest to lowest resale price in Punggol

```sql
SELECT *
FROM resale_flat_prices_2017
WHERE town = 'PUNGGOL'
ORDER BY resale_price DESC;
```

## Aggregate Functions

> Select the average resale price of flats in Bishan

```sql
SELECT AVG(resale_price) AS avg_price
FROM resale_flat_prices_2017
WHERE town = 'BISHAN';
```

> Select the total resale value (price) of flats in Tampines

```sql
SELECT SUM(resale_price) AS total_value
FROM resale_flat_prices_2017
WHERE town = 'TAMPINES';
```

## Group By

> Select the average resale price by flat type

```sql
SELECT flat_type, AVG(resale_price) AS avg_price
FROM resale_flat_prices_2017
GROUP BY flat_type;
```

> Select the average resale price by flat type and flat model

```sql
SELECT flat_type, flat_model, AVG(resale_price) AS avg_price
FROM resale_flat_prices_2017
GROUP BY flat_type, flat_model;
```

> Select the average resale price by town and lease commence date only for lease commence dates after year 2010 and sort by town (descending) and lease commence date (descending)

```sql
SELECT town, lease_commence_date, AVG(resale_price) AS avg_price
FROM resale_flat_prices_2017
WHERE lease_commence_date > 2010
GROUP BY town, lease_commence_date
ORDER BY town DESC, lease_commence_date DESC;
```

## Having

> Select the maximum resale price by town only for town with maximum resale price greater than 1,000,000

```sql
SELECT town, MAX(resale_price) AS max_price
FROM resale_flat_prices_2017
GROUP BY town
HAVING MAX(resale_price) > 1000000;
```

## Advanced Operators and Functions

> Return the unique flat types and flat models

```sql
SELECT DISTINCT flat_type, flat_model
FROM resale_flat_prices_2017;
```

> Return the records with a new column `flat_size` with values `Small` if flat type is `1-3 ROOM`, `Medium` if flat type is `4 ROOM` and `Large` if flat type is `5 ROOM`, `EXECUTIVE` or `MULTI-GENERATION`

```sql
SELECT *,
CASE
    WHEN flat_type LIKE '1%' OR flat_type LIKE '2%' OR flat_type LIKE '3%' THEN 'Small'
    WHEN flat_type LIKE '4%' THEN 'Medium'
    WHEN flat_type IN ('5 ROOM', 'EXECUTIVE', 'MULTI-GENERATION') THEN 'Large'
END AS flat_size
FROM resale_flat_prices_2017;
```
