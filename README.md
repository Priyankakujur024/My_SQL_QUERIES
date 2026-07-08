# My_SQL_QUERIES
My_SQL_QUERIES
-- ====================================================================
-- PROJECT: CARDEKHO REAL DATASET ANALYSIS & METRICS
-- AUTHOR: Priyanka Kujur (Aspiring Data Analyst)
-- DATASET SIZE: 15,411 Rows (Columns: brand, model, selling_price, fuel_type, transmission, etc.)
-- ====================================================================

-- 1. DATABASE SETUP
CREATE DATABASE cardekho_analytics;
USE cardekho_analytics;

-- (Assuming the dataset is imported into a table named 'car_data')
SELECT * FROM car_data LIMIT 10;

-- ====================================================================
-- 2. BUSINESS QUESTIONS & ANALYTICAL QUERIES
-- ====================================================================

-- Q1. Total Cars Count: Total kitne cars ka data available hai?
SELECT COUNT(*) AS Total_Cars 
FROM car_data;


-- Q2. Fuel Type Analysis: Kis fuel type ki kitni gaadiyan hain?
SELECT fuel_type, COUNT(*) AS Total_Count
FROM car_data
GROUP BY fuel_type
ORDER BY Total_Count DESC;


-- Q3. Year-wise Car Sales/Availability: Kis saal mein sabse zyada gaadiyan aayi?
SELECT year, COUNT(*) AS Total_Cars
FROM car_data
GROUP BY year
ORDER BY year DESC;


-- Q4. Most Expensive & Cheapest Cars: Sabse mehangi aur sasti gaadi kaunsi hai?
SELECT brand, model, selling_price 
FROM car_data
WHERE selling_price = (SELECT MAX(selling_price) FROM car_data)
   OR selling_price = (SELECT MIN(selling_price) FROM car_data);


-- Q5. Average Selling Price by Brand: Kis brand ki gaadiyan ka average price sabse zyada hai?
SELECT brand, ROUND(AVG(selling_price), 2) AS Avg_Price, COUNT(*) AS Total_Cars
FROM car_data
GROUP BY brand
HAVING Total_Cars > 10
ORDER BY Avg_Price DESC
LIMIT 10;


-- Q6. Transmission Type Filter: Automatic vs Manual cars ka count aur unka avg price kya hai?
SELECT transmission, COUNT(*) AS Total_Cars, ROUND(AVG(selling_price), 2) AS Avg_Price
FROM car_data
GROUP BY transmission;


-- Q7. High Mileage Cars: Kaunsi gaadiyan best mileage de rahi hain (Top 10)?
SELECT brand, model, mileage, fuel_type
FROM car_data
ORDER BY CAST(mileage AS DECIMAL(10,2)) DESC
LIMIT 10;
