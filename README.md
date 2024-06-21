# Coffee sales - Dashboard

### Dashboard Link : https://app.powerbi.com/view?r=eyJrIjoiY2M2ODQyOWYtMzUzNi00ODE4LWE4ZTEtZDI0YTVkNzE1OTc1IiwidCI6Ijc3MWYyOTlmLWU5ZmItNDgwNS05M2RkLTBlOTkwZmNkNWZkZiJ9

## Problem Statement

This dashboard helps the coffee shop understand its sales performance better. It provides insights into monthly sales trends, order volumes, and product category performance. By analyzing sales data, the coffee shop can identify areas for improvement and growth opportunities.

The dashboard highlights month-on-month changes in sales, the total number of orders, and the total quantity sold, allowing the coffee shop to track its performance over time. Daily sales analysis with an average line helps identify exceptional sales days, ensuring better inventory and staffing management..

The sales analysis by product category reveals which product categories contribute the most to overall sales, enabling the shop to focus on popular items and optimize the product mix. The top 10 products by sales section allows quick visualization of the best-performing products, aiding in promotional and marketing efforts.

By using this dashboard, the coffee shop can improve its services, increase customer satisfaction, and drive sales growth. It allows the management to make data-driven decisions, optimize inventory, and enhance customer experience by addressing identified improvement areas.

### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4 : It was observed that in none of the columns errors & empty values were present.
- Step 5 : Total Sales Analysis:
   -  Create Monthly Sales Measure: Using DAX, I created a measure for total sales per month.
           
             Total Sales = SUM(Sales[Amount])
   -  Create Month-on-Month Sales Measure: I calculated the month-on-month percentage change in sales.

            MoM Sales Change = (SUM(Sales[Amount]) - CALCULATE(SUM(Sales[Amount]), DATEADD(Sales[Date], -1, MONTH))) / CALCULATE(SUM(Sales[Amount]), DATEADD(Sales[Date], -1, MONTH))
      ![Snap_1](https://github.com/akshinth/Coffee-sales-Powerbi-project/assets/108680058/2a785865-099d-491c-a8f6-9242ba505750)

   -  Visualize Total Sales: I used a line chart to display total sales over time and added a card to show the current month's sales.
- Step 6 : Total Orders Analysis:
  -    Create Monthly Orders Measure: Using DAX, I created a measure for total orders per month.

           Total Orders = COUNT(Sales[OrderID])
 
  - Create Month-on-Month Orders Measure: I calculated the month-on-month percentage change in orders.

           MoM Orders Change = (COUNT(Sales[OrderID]) - CALCULATE(COUNT(Sales[OrderID]), DATEADD(Sales[Date], -1, MONTH))) / CALCULATE(COUNT(Sales[OrderID]), DATEADD(Sales[Date], -1, MONTH))
       ![Snap_1](https://github.com/akshinth/Coffee-sales-Powerbi-project/assets/108680058/290febf1-5fff-4140-9a2c-b5f08ac72c87)

- Step 7 :Total Quantity Sold Analysis:
   - Create Monthly Quantity Measure: Using DAX, I created a measure for total quantity sold per month.

          Total Quantity = SUM(Sales[Quantity])

   -  Create Month-on-Month Quantity Measure: I calculated the month-on-month percentage change in quantity sold.

         MoM Quantity Change = (SUM(Sales[Quantity]) - CALCULATE(SUM(Sales[Quantity]), DATEADD(Sales[Date], -1, MONTH))) / CALCULATE(SUM(Sales[Quantity]), DATEADD(Sales[Date], -1, MONTH))

   - Visualize Total Quantity: I used a bar chart to display total quantity sold over time and added a card to show the current month's quantity sold.

     ![Snap_1](https://github.com/akshinth/Coffee-sales-Powerbi-project/assets/108680058/b04c8276-e47f-4f8f-92a3-a3f810caf5c0)

        
- Step 8 : Daily Sales Analysis with Average Line:
     - Create Daily Sales Measure: Using DAX, I calculated daily sales.

             Daily Sales = SUM(Sales[Amount])
    -  Create Average Daily Sales Measure: I calculated the average daily sales.

           Average Daily Sales = AVERAGE(Sales[Amount])
    - Visualize Daily Sales: I used a line chart to display daily sales with an average line, and applied conditional formatting to highlight days where sales exceeded or fell below the average.
        
 - Step 9 : Sales Analysis by Product Category:
   - Create Sales by Category Measure: Using DAX, I calculated sales per product category.

         Sales by Category = SUM(Sales[Amount])
   - Visualize Sales by Category: I used a bar chart to display sales by product category, providing insights into which categories contributed the most to overall sales.
         
        ![Snap_1](https://github.com/akshinth/Coffee-sales-Powerbi-project/assets/108680058/4d381a64-6593-4cf4-ab47-976ab5cd3e2b)

 
 
 - Step 10 : N Top 10 Products by Sales:
    - Create Top 10 Products Measure: Using DAX, I ranked products by sales.

          Top 10 Products = TOPN(10, VALUES(Sales[ProductName]), [Total Sales], DESC)
   -    Visualize Top 10 Products: I used a bar chart to display the top 10 products based on sales volume, allowing us to quickly see the best-performing products.

        ![Snap_1](https://github.com/akshinth/Coffee-sales-Powerbi-project/assets/108680058/e93149be-8c57-44ea-ab3a-2dc012b4347f)
 

 
 - Step 11 : Sales Analysis by Days and Hours:

   - Create Sales by Day and Hour Measure: Using DAX, I calculated sales for each day and hour.

         Sales by Day and Hour = SUM(Sales[Amount])
   - Visualize Sales by Day and Hour: I used a heat map to display sales patterns by days and hours, and added tooltips to show detailed metrics when hovering over specific day-hour slots.

# Final Touches:

### Design and Formatting: 
I applied consistent formatting and color schemes to align with our coffee shop's branding.

### Interactivity: 
I added filters and slicers to allow users to interact with the data (e.g., filter by date, product category).

### Testing: 
I thoroughly tested the dashboard to ensure all measures and visualizations were working as expected.

