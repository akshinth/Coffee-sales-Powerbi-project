## COFFEE SHOP SALES PROJECT
## MY SQL QUERIES
### Description 
This project aimed to transform raw sales data from a coffee shop into actionable insights using MySQL. By standardizing date and time formats and correcting data types, we ensured data consistency. Key metrics such as total sales, total orders, and total quantity sold were computed, including Month-over-Month growth, to assess performance trends. The project also analyzed sales by day, hour, location, product category, and top-selling products. These insights help in understanding customer behavior, optimizing inventory, and making data-driven decisions to enhance sales strategies and business operations.


1) CONVERT DATE (transaction_date) COLUMN TO PROPER DATE FORMAT
       
       UPDATE coffee_shop_sales
       SET transaction_date = STR_TO_DATE(transaction_date, '%d-%m-%Y');

2) ALTER DATE (transaction_date) COLUMN TO DATE DATA TYPE

       ALTER TABLE coffee_shop_sales
       MODIFY COLUMN transaction_date DATE;

3) CONVERT TIME (transaction_time)  COLUMN TO PROPER DATE FORMAT

       UPDATE coffee_shop_sales
       SET transaction_time = STR_TO_DATE(transaction_time, '%H:%i:%s');

4) ALTER TIME (transaction_time) COLUMN TO DATE DATA TYPE
       ALTER TABLE coffee_shop_sales
       MODIFY COLUMN transaction_time TIME;

5) DATA TYPES OF DIFFERENT COLUMNS

   DESCRIBE coffee_shop_sales;

   ![Snap_1](https://github.com/akshinth/COFFEE-SHOP-SALES-SQL--PROJECT/assets/108680058/3c1f55c9-c24c-4a0b-9354-c2fb87f935a2)

CHANGE COLUMN NAME `ï»¿transaction_id` to transaction_id

      ALTER TABLE coffee_shop_sales
      CHANGE COLUMN `ï»¿transaction_id` transaction_id INT;
6) TOTAL SALES

       SELECT ROUND(SUM(unit_price * transaction_qty)) as Total_Sales 
       FROM coffee_shop_sales 
       WHERE MONTH(transaction_date) = 5 -- for month of (CM-May)

        
   ![image](https://github.com/akshinth/COFFEE-SHOP-SALES-SQL--PROJECT/assets/108680058/aeb48ca9-3bd3-482a-86bf-d53bf09dc5d1)


6) TOTAL SALES KPI - MOM DIFFERENCE AND MOM GROWTH

            SELECT 
              MONTH(transaction_date) AS month,
              ROUND(SUM(unit_price * transaction_qty)) AS total_sales,
              (SUM(unit_price * transaction_qty) - LAG(SUM(unit_price * transaction_qty), 
              OVER (ORDER BY MONTH(transaction_date))) / LAG(SUM(unit_price * transaction_qty), 1) 
              OVER (ORDER BY MONTH(transaction_date)) * 100 AS mom_increase_percentage
            FROM 
              coffee_shop_sales
            WHERE 
              MONTH(transaction_date) IN (4, 5) -- for months of April and May
            GROUP BY 
              MONTH(transaction_date)
            ORDER BY 
              MONTH(transaction_date);
      ![image](https://github.com/akshinth/COFFEE-SHOP-SALES-SQL--PROJECT/assets/108680058/13190099-1b30-4840-b977-c37fd1f60209)


Explaination

SELECT clause:

 - MONTH(transaction_date) AS month: Extracts the month from the transaction_date column and renames it as month.
 - ROUND(SUM(unit_price * transaction_qty)) AS total_sales: Calculates the total sales by multiplying unit_price and transaction_qty, then sums the result for each month. The ROUND function rounds the result to the nearest integer.
 - (SUM(unit_price * transaction_qty) - LAG(SUM(unit_price * transaction_qty), 1) OVER (ORDER BY MONTH(transaction_date))) / LAG(SUM(unit_price * transaction_qty), 1) OVER (ORDER BY MONTH(transaction_date)) * 100 AS mom_increase_percentage with the functions used:
     - SUM(unit_price * transaction_qty): This calculates the total sales for the current month. It multiplies the unit_price by the transaction_qty for each transaction and then sums up these values.
     - LAG(SUM(unit_price * transaction_qty), 1) OVER (ORDER BY MONTH(transaction_date)): This function retrieves the value of the total sales for the previous month. It uses the LAG window function to get the value of the SUM(unit_price * transaction_qty) from the previous row (previous month) ordered by the transaction_date.
    - (SUM(unit_price * transaction_qty) - LAG(SUM(unit_price * transaction_qty), 1) OVER (ORDER BY MONTH(transaction_date))): This part calculates the difference between the total sales of the current month and the total sales of the previous month.
    - LAG(SUM(unit_price * transaction_qty), 1) OVER (ORDER BY MONTH(transaction_date)): This function retrieves the value of the total sales for the previous month again. It's used in the denominator to calculate the percentage increase.
    - (SUM(unit_price * transaction_qty) - LAG(SUM(unit_price * transaction_qty), 1) OVER (ORDER BY MONTH(transaction_date))) / LAG(SUM(unit_price * transaction_qty), 1) OVER (ORDER BY MONTH(transaction_date)): This calculates the ratio of the difference in sales between the current and previous months to the total sales of the previous month. It represents the percentage increase or decrease in sales compared to the previous month.
    - 100: This part multiplies the ratio by 100 to convert it to a percentage.
- FROM clause:
coffee_shop_sales: Specifies the table from which data is being selected.
- WHERE clause:
MONTH(transaction_date) IN (4, 5): Filters the data to include only transactions from April and May.
- GROUP BY clause:
MONTH(transaction_date): Groups the results by month.
- ORDER BY clause:
MONTH(transaction_date): Orders the results by month.




7) TOTAL ORDERS

       SELECT COUNT(transaction_id) as Total_Orders
       FROM coffee_shop_sales 
       WHERE MONTH (transaction_date)= 5 -- for month of (CM-May)
 ![image](https://github.com/akshinth/COFFEE-SHOP-SALES-SQL--PROJECT/assets/108680058/09461a46-d74b-480e-82ac-96b3eac2a054)



8) TOTAL ORDERS KPI - MOM DIFFERENCE AND MOM GROWTH

       SELECT 
         MONTH(transaction_date) AS month,
         ROUND(COUNT(transaction_id)) AS total_orders,
         (COUNT(transaction_id) - LAG(COUNT(transaction_id), 1) 
         OVER (ORDER BY MONTH(transaction_date))) / LAG(COUNT(transaction_id), 1) 
         OVER (ORDER BY MONTH(transaction_date)) * 100 AS mom_increase_percentage
       FROM 
         coffee_shop_sales
       WHERE 
         MONTH(transaction_date) IN (4, 5) -- for April and May
       GROUP BY 
         MONTH(transaction_date)
       ORDER BY 
         MONTH(transaction_date);
  ![image](https://github.com/akshinth/COFFEE-SHOP-SALES-SQL--PROJECT/assets/108680058/719dff84-eff5-4c8e-b54d-ffdd367eb16c)





9) TOTAL QUANTITY SOLD

         SELECT SUM(transaction_qty) as Total_Quantity_Sold
         FROM coffee_shop_sales 
         WHERE MONTH(transaction_date) = 5 -- for month of (CM-May)
    
    
    
![image](https://github.com/akshinth/COFFEE-SHOP-SALES-SQL--PROJECT/assets/108680058/69cb7e1c-1288-42f8-9ca3-3f203656b4b5)



10) TOTAL QUANTITY SOLD KPI - MOM DIFFERENCE AND MOM GROWTH

        SELECT 
            MONTH(transaction_date) AS month,
            ROUND(SUM(transaction_qty)) AS total_quantity_sold,
            (SUM(transaction_qty) - LAG(SUM(transaction_qty), 1) 
            OVER (ORDER BY MONTH(transaction_date))) / LAG(SUM(transaction_qty), 1) 
            OVER (ORDER BY MONTH(transaction_date)) * 100 AS mom_increase_percentage
        FROM 
            coffee_shop_sales
        WHERE 
            MONTH(transaction_date) IN (4, 5)   -- for April and May
        GROUP BY 
            MONTH(transaction_date)
        ORDER BY 
            MONTH(transaction_date);

![image](https://github.com/akshinth/COFFEE-SHOP-SALES-SQL--PROJECT/assets/108680058/cb027602-2611-41b9-8168-54a63e12acb7)





11) CALENDAR TABLE – DAILY SALES, QUANTITY and TOTAL ORDERS


        SELECT
            SUM(unit_price * transaction_qty) AS total_sales,
            SUM(transaction_qty) AS total_quantity_sold,
            COUNT(transaction_id) AS total_orders
        FROM 
            coffee_shop_sales
        WHERE 
            transaction_date = '2023-05-18'; --For 18 May 2023

![image](https://github.com/akshinth/COFFEE-SHOP-SALES-SQL--PROJECT/assets/108680058/98a909f9-e22e-4626-bb38-93e068831adc)


12) SALES TREND OVER PERIOD

        SELECT AVG(total_sales) AS average_sales
        FROM (
            SELECT 
                SUM(unit_price * transaction_qty) AS total_sales
            FROM 
                coffee_shop_sales
            WHERE 
                MONTH(transaction_date) = 5  -- Filter for May
            GROUP BY 
                transaction_date
        ) AS internal_query;

Query Explanation:

- This inner subquery calculates the total sales (unit_price * transaction_qty) for each date in May. It filters the data to include only transactions that occurred in May by using the MONTH() function to extract the month from the - - - transaction_date column and filtering for May (month number 5).
- The GROUP BY clause groups the data by transaction_date, ensuring that the total sales are aggregated for each individual date in May.
- The outer query calculates the average of the total sales over all dates in May. It references the result of the inner subquery as a derived table named internal_query.
- The AVG() function calculates the average of the total_sales column from the derived table, giving us the average sales for May.

![image](https://github.com/akshinth/COFFEE-SHOP-SALES-SQL--PROJECT/assets/108680058/b2a8b0fc-5653-41ee-b5b8-3b5a2f0c02ce)



13) DAILY SALES FOR MONTH SELECTED
        SELECT 
            DAY(transaction_date) AS day_of_month,
            ROUND(SUM(unit_price * transaction_qty),1) AS total_sales
        FROM 
            coffee_shop_sales
        WHERE 
            MONTH(transaction_date) = 5  -- Filter for May
        GROUP BY 
            DAY(transaction_date)
        ORDER BY 
            DAY(transaction_date);

    ![image](https://github.com/akshinth/COFFEE-SHOP-SALES-SQL--PROJECT/assets/108680058/46634183-11c9-4a07-bcef-4cd683a66fd3)          ![image](https://github.com/akshinth/COFFEE-SHOP-SALES-SQL--PROJECT/assets/108680058/5f0ce014-91d2-42f0-95be-4533b509ab65)


   

COMPARING DAILY SALES WITH AVERAGE SALES – IF GREATER THAN “ABOVE AVERAGE” and LESSER THAN “BELOW AVERAGE”

        SELECT 
            day_of_month,
            CASE 
                WHEN total_sales > avg_sales THEN 'Above Average'
                WHEN total_sales < avg_sales THEN 'Below Average'
                ELSE 'Average'
            END AS sales_status,
            total_sales
        FROM (
            SELECT 
                DAY(transaction_date) AS day_of_month,
                SUM(unit_price * transaction_qty) AS total_sales,
                AVG(SUM(unit_price * transaction_qty)) OVER () AS avg_sales
            FROM 
                coffee_shop_sales
            WHERE 
                MONTH(transaction_date) = 5  -- Filter for May
            GROUP BY 
                DAY(transaction_date)
        ) AS sales_data
        ORDER BY 
            day_of_month;
    ![image](https://github.com/akshinth/COFFEE-SHOP-SALES-SQL--PROJECT/assets/108680058/cb98c545-9841-4fa6-8da1-14b8f07b6bae)


14) SALES BY WEEKDAY / WEEKEND:

        SELECT 
            CASE 
                WHEN DAYOFWEEK(transaction_date) IN (1, 7) THEN 'Weekends'
                ELSE 'Weekdays'
            END AS day_type,
            ROUND(SUM(unit_price * transaction_qty),2) AS total_sales
        FROM 
            coffee_shop_sales
        WHERE 
            MONTH(transaction_date) = 5  -- Filter for May
        GROUP BY 
            CASE 
                WHEN DAYOFWEEK(transaction_date) IN (1, 7) THEN 'Weekends'
                ELSE 'Weekdays'
            END;

    ![image](https://github.com/akshinth/COFFEE-SHOP-SALES-SQL--PROJECT/assets/108680058/200fb338-7b6e-4fd2-9fb9-883dbe9a57b5)


15) SALES BY STORE LOCATION

        SELECT 
            store_location,
            SUM(unit_price * transaction_qty) as Total_Sales
        FROM coffee_shop_sales
        WHERE
            MONTH(transaction_date) =5 
        GROUP BY store_location
        ORDER BY 	SUM(unit_price * transaction_qty) 
    
    ![image](https://github.com/akshinth/COFFEE-SHOP-SALES-SQL--PROJECT/assets/108680058/0fdd6a5f-f71f-400e-8a67-108558370f98)


16) SALES BY PRODUCT CATEGORY

        SELECT 
            product_category,
            ROUND(SUM(unit_price * transaction_qty),1) as Total_Sales
        FROM coffee_shop_sales
        WHERE
            MONTH(transaction_date) = 5 
        GROUP BY product_category
        ORDER BY SUM(unit_price * transaction_qty) DESC

   ![image](https://github.com/akshinth/COFFEE-SHOP-SALES-SQL--PROJECT/assets/108680058/3dcaaea8-c802-4616-959e-acd41f8ffd18)


17) SALES BY PRODUCTS (TOP 10)

        SELECT 
            product_type,
            ROUND(SUM(unit_price * transaction_qty),1) as Total_Sales
        FROM coffee_shop_sales
        WHERE
            MONTH(transaction_date) = 5 
        GROUP BY product_type
        ORDER BY SUM(unit_price * transaction_qty) DESC
        LIMIT 10

    ![image](https://github.com/akshinth/COFFEE-SHOP-SALES-SQL--PROJECT/assets/108680058/d0460e26-c434-45f4-9fd1-b29c05d12892)


18) SALES BY DAY | HOUR

        SELECT 
            ROUND(SUM(unit_price * transaction_qty)) AS Total_Sales,
            SUM(transaction_qty) AS Total_Quantity,
            COUNT(*) AS Total_Orders
        FROM 
            coffee_shop_sales
        WHERE 
            DAYOFWEEK(transaction_date) = 3 -- Filter for Tuesday (1 is Sunday, 2 is Monday, ..., 7 is Saturday)
            AND HOUR(transaction_time) = 8 -- Filter for hour number 8
            AND MONTH(transaction_date) = 5; -- Filter for May (month number 5)

    ![image](https://github.com/akshinth/COFFEE-SHOP-SALES-SQL--PROJECT/assets/108680058/e654f61b-56e6-41d6-a8db-18a10b361a8e)


TO GET SALES FROM MONDAY TO SUNDAY FOR MONTH OF MAY

        SELECT 
            CASE 
                WHEN DAYOFWEEK(transaction_date) = 2 THEN 'Monday'
                WHEN DAYOFWEEK(transaction_date) = 3 THEN 'Tuesday'
                WHEN DAYOFWEEK(transaction_date) = 4 THEN 'Wednesday'
                WHEN DAYOFWEEK(transaction_date) = 5 THEN 'Thursday'
                WHEN DAYOFWEEK(transaction_date) = 6 THEN 'Friday'
                WHEN DAYOFWEEK(transaction_date) = 7 THEN 'Saturday'
                ELSE 'Sunday'
            END AS Day_of_Week,
            ROUND(SUM(unit_price * transaction_qty)) AS Total_Sales
        FROM 
            coffee_shop_sales
        WHERE 
            MONTH(transaction_date) = 5 -- Filter for May (month number 5)
        GROUP BY 
            CASE 
                WHEN DAYOFWEEK(transaction_date) = 2 THEN 'Monday'
                WHEN DAYOFWEEK(transaction_date) = 3 THEN 'Tuesday'
                WHEN DAYOFWEEK(transaction_date) = 4 THEN 'Wednesday'
                WHEN DAYOFWEEK(transaction_date) = 5 THEN 'Thursday'
                WHEN DAYOFWEEK(transaction_date) = 6 THEN 'Friday'
                WHEN DAYOFWEEK(transaction_date) = 7 THEN 'Saturday'
                ELSE 'Sunday'
            END;
    

![image](https://github.com/akshinth/COFFEE-SHOP-SALES-SQL--PROJECT/assets/108680058/fcbc2c5f-5ee3-4d11-8d75-9fa4129e6d0c)


TO GET SALES FOR ALL HOURS FOR MONTH OF MAY

        SELECT 
            HOUR(transaction_time) AS Hour_of_Day,
            ROUND(SUM(unit_price * transaction_qty)) AS Total_Sales
        FROM 
            coffee_shop_sales
        WHERE 
            MONTH(transaction_date) = 5 -- Filter for May (month number 5)
        GROUP BY 
            HOUR(transaction_time)
        ORDER BY 
            HOUR(transaction_time);


 ![image](https://github.com/akshinth/COFFEE-SHOP-SALES-SQL--PROJECT/assets/108680058/3ae219c5-828f-457d-aa5e-2f7407b36366)




