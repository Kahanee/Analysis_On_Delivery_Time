
# Meal Time Matters: A Data-Driven Analysis Approach to Food Delivery Time

### Optimising and Improving Food Delivery with Data Analysis
[Link to dataset](https://www.kaggle.com/datasets/gauravmalik26/food-delivery-dataset)

![Screenshot of dashboard](https://imgur.com/ugIegJR.jpg)

#### Entity Relationship Diagram:

![Screenshot ERD ](https://imgur.com/WAODsMH.jpg)

#### SCHEMA AND TABLE DIAGRAM :
![Screenshot Schema and TableDiagram ](https://imgur.com/UzW8G8C.jpg)

Description of dataset:

Dataset of over 47K rows with over 20 coloumns to analyse estimated Food delivery time analysis.
Analysis of the dataset:To identify what are the internal and external factors that have the most significant impact on delivery time.


Insights of the Analysis and the outcome :

- Summarize the key findings and insights gained from the analysis, including any trends or patterns in delivery time, and any external factors that have a significant impact on delivery time.
- By analyzing delivery time data, businesses can optimize their operations to reduce delivery time and improve customer satisfaction.

- Delivery time analysis can also help businesses to identify areas for improvement in their operations, such as inefficient delivery routes or inadequate staffing.

- With accurate delivery time estimates, businesses can provide better customer service by providing customers with more accurate delivery times and minimizing delays.

- Food delivery time analysis can also help businesses to make data-driven decisions about pricing, promotions, and other aspects of their operations, based on factors that affect delivery time.

- By analyzing delivery time data over time, businesses can identify trends and patterns, such as seasonal fluctuations or changes in customer preferences, that can inform their business strategies.
- 
- Suggestions for business implementation: Base on the analysis to  recommendation how the business can use this analysis to improve delivery time, such as optimizing routes, adjusting staffing levels, or providing real-time updates to customers.


Data Wrangling:
- Data cleaning in Ms excel and Postgres SQL, transforming raw data from Orders, Emp and factors table into format suitable for analysis.
- Remove redundant values in the table, clean duplicates and blank cells using Ms Excel
- Split single column to two seperate column using Split Column Delimiter.
- Change the various column Data type to appropriate data type is PostgresSQL.
- Update the date set with proper headings using PostgresSQL.

Data Normalization and Data structuring :
- Split the raw Database to 3 tables.
- Insert Primary Key and Foreign Key to the table to normalize and create relationship between tables.
- Insert new table by extracting day from Data table using PostgresSQL. 

Queries executed that were used to manipulate data and create the necessary tables for the food delivery time analysis in PostgresSQL not limited to :

-CREATE TABLE: Used to create a new table in the database
INSERT INTO: Used to insert new data into a table
SELECT: Used to retrieve data from a table
WHERE: Used to filter data based on specified conditions
JOIN: Used to combine rows from two or more tables based on a related column between them
GROUP BY: Used to group data based on one or more columns
ORDER BY: Used to sort data in ascending or descending order based on one or more columns
UPDATE: Used to modify existing data in a table
ALTER TABLE: Used to add, modify, or delete columns in an existing table
DROP TABLE: Used to delete an entire table from the database


Sample Queries :

--ALTER TABLE orders ADD COLUMN day_of_week varchar(10);
UPDATE orders SET day_of_week = to_char(order_date, 'Day');

--CREATE TABLE orders (
    id serial PRIMARY KEY,
    order_id text,
    order_date date,
    order_time time,
    order_picked time,
    mul_delivery int,
    emp_id text,
    day_of_week varchar(10)
);

-- Populate the day_of_week column
UPDATE orders SET day_of_week = to_char(order_date, 'Day');

-- Create a subquery to calculate the time_period
SELECT
  order_time,
  CASE 
    WHEN order_time BETWEEN '08:00:00' AND '10:59:59' THEN 'Peak Hours'
    WHEN order_time BETWEEN '11:00:00' AND '15:59:59' THEN 'Lunch Hours'
    ELSE 'Non-Peak Hours'
  END AS time_period,
  COUNT(*) AS num_orders
FROM orders
GROUP BY order_time, time_period;

--To find the demand and relationship between time_period,total delivery & avg delivery time:

WITH time as
  (SELECT  min_taken,mul_delivery,
  CASE 
  WHEN order_time BETWEEN '10:00:00' AND '12:00:00' THEN 'Lunch Hour'
    WHEN order_time BETWEEN '17:00:00' AND '20:00:00' THEN 'Peak Hour'
	WHEN order_time BETWEEN '21:00:00' AND '24:00:00' THEN 'Happy Hour'
    ELSE 'Non-Peak Hours'
  END AS time_period
 FROM orders)
 SELECT time_period, count(time_period) AS total_deliveries,
 ROUND (AVG(min_taken), 1) AS avg_time
 FROM time
 GROUP BY time_period
 ORDER BY 3 DESC;



Data Import from .CSV file to post PostgresSQL using SQL Command line:
#### SQL Command Line :
![Screenshot command line](https://imgur.com/zTMumOR.jpg)



Data inform from PostgresSQL to Ms Excel for Data Visualisation:
- As part of this portfolio, data visualization was used to communicate insights and findings from the analysis of the food delivery time data.

- The data visualization involved the use of charts, graphs, and tables to represent the relationships, trends, and patterns found in the data.
- The visualization focused on presenting the analysis results in a clear and concise manner that can be easily understood by stakeholders and decision-makers.



[My Linkedin Prolife ](https://www.linkedin.com/in/sailaja-begum/)

