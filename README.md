# Walmart
How Can A Business Be Successful

## INTRODUCTION
In this project, I will take on the role of a junior data analyst who was given a dataset assigned by the supervisor that needs to be 
 cleaned and analyzed in order to gain insights to  better inform the business.This analysis will follow the 6 steps of Data Analysis 
 which are: Ask, Prepare, Process, Analyze, Share and Act.

### Ask
#### Business Task:
The purpose of this project is to conduct an in-depth analysis of sales data to gain valuable insights into sales performance, identify 
 areas of improvement, and make data driven decisions to increase revenue and profitability with SQL.

#### Deliverables:
+ A clear summary of the business task.
+ A complete documentation of all the data cleaning, manipulation and analysis process.
+ A dashboard with visualizations  and outcomes.
+ Recommendations based on our insights and analysis.

### PREPARE
#### Background
The data is public dataset available through kaggle https://www.kaggle.com/datasets/mikhail1681/walmart-sales/data. It contains data 
 from 45 different walmart stores from year 2010 to year 2012 and 6436 rows. Since the data is a first party data it is ROCCC, we have access to their weekly Sales 
 along with  the Temperature, CPI, Fuel Price, and Unemployment rates at time intervals  throughout the year. We want to analyze all 
 these different values to see if there were possible correlations between two or more values at a period in our dataset. 

 #### Limitations
 The data was collected from 13 years ago, so the data is not current. The data was created for educational purposes.

 The data contains 8 columns namely; Store, Dates, Weekly_Sales, Holiday_Flag, Temperature, Fuel_Price, CPI and Unemployment.

### PROCESS
The tool used for the processing and cleaning stage will be Microsodft Excel. Since the data is already in CSV format its ideal to 
 start the clean processes by;
 + Observing the data: The data looks well structured, correct and consistent, 
 + Checking for missing data using conditional formating: With the help of conditional formating which is a technique to highlight 
   certain values of interest. We format Blank cells. This dataset returned no missing values.
 + Finally, i made sure the dates format were all formatted and consistent all through which was already that way.
 + The holiday_flag column shows 0 and 1, with '0' representing the week with no special holiday and '1' representing a special holiday 
   week

![image](https://github.com/user-attachments/assets/8bcabf07-fb01-4034-9c09-8928e352453b)

Now the dataset is cleaned and ready for analysis.


### ANALYSIS AND SHARE
For this process, we use SQL to analyze the data and Tableau and SQL for the visualization. The first stage is to load the data into SQL and check the first 10 rows to be sure it was imported correctly.

        SELECT *
        FROM `my-sandbox-project-417117.Walmart.walmart_data` 
        LIMIT 10
 
 ![image](https://github.com/user-attachments/assets/95f7bbac-438a-4083-8818-2663170ed83c)

 This shows the correct column names and shows the rows are not organized. To be sure its the same data as in excel, i arranged the data and check the first 10 rows

         SELECT *
         FROM 
              `my-sandbox-project-417117.Walmart.walmart_data`
         ORDER BY Store,
                  Date ASC;
         LIMIT 10

 ![image](https://github.com/user-attachments/assets/351e937b-34f9-4da6-ba7d-6c6a52875093)

  Now that we are sure of the data, lets do a further analysis.

 1. Firstly, we look at the total revenue generated for each stores 

           SELECT store,
                  SUM(Weekly_Sales) AS total_weekly_sales
           FROM
                 `my-sandbox-project-417117.Walmart.walmart_data`
           GROUP BY
                  Store
           ORDER BY
                  total_weekly_sales DESC;
      
![image](https://github.com/user-attachments/assets/ab5ce111-6240-4c91-a556-dd14a1cb3574)

*This result shows that store 20 has the highest total number of weekly sales and following closely is store 4.*

Since we know the store with the highest total weekly sales, we will run this query to get the store with the lowest wekly sales.

          SELECT store,
                 SUM(Weekly_Sales) AS total_weekly_sales
          FROM `my-sandbox-project-417117.Walmart.walmart_data`
          GROUP BY Store
          ORDER BY total_weekly_sales ASC;

 ![image](https://github.com/user-attachments/assets/b7b8aec2-08f0-4ccd-b7f1-7f0893d21fc2)
 
 *This result shows that store 33 has the lowest total number of weekly sales and following closely is store 44.*

![total_weekly_sales by store](https://github.com/user-attachments/assets/a18e3758-891a-401a-9875-2830ec9c182f)

2. Now we  query the year with the highest and lowest sales 

         SELECT 
            SUM(weekly_sales) AS total_sales,
            EXTRACT(year FROM Date) AS sales_year
        FROM 
           `my-sandbox-project-417117.Walmart.walmart_data`
        GROUP BY
            sales_year
        ORDER BY
            total_sales DESC; 

![Sheet 1 (6)](https://github.com/user-attachments/assets/b9d983ab-6eba-4abf-b055-f666d0ff93bb)

*This shows that the year 2011 recorded the highest total sales while 2012 recorded the least sales*

 3. Now we look at what holiday is impacting weeekly sales
    
          SELECT 
                Date,
                EXTRACT(year FROM Date) AS year,
                SUM(Weekly_Sales) AS total_sales,
                Holiday_Flag
          FROM 
               `my-sandbox-project-417117.Walmart.walmart_data`
          WHERE 
                Holiday_Flag = 1
          GROUP BY
                Date, Holiday_Flag
          ORDER BY 
                total_sales DESC

    ![image](https://github.com/user-attachments/assets/12169665-6d5b-4316-a3cb-7064d4037839)

*This query shows that the major top 3 holidays with high total sales Thanksgiving(2011-11-25 and 2010-11-26) and  Super Bowl(2012-02-10), with 2011 having the highest total sales 
 year for Thanksgiving. Holidays like Christmas are not available  in the dataset.*

*However, After further research the date 2011-11-25 and 2010-11-26 happen to be Black Friday in the United States. Black Fridays are days retailers including Walmart, often offers 
 discounts and promotions attracting  a large number of customers, making this day one of the biggest shopping days.*

4. Relationship between temperature and sales

            SELECT 
                 Weekly_Sales,
                 Temperature,
            FROM 
                `my-sandbox-project-417117.Walmart.walmart_data`
            ORDER BY 
                 Temperature DESC

   ![Weekly_Sales by Temperature (1)](https://github.com/user-attachments/assets/5f04fbb4-8441-4e5c-955e-25beec509cbb)

*Here, this shows that as temperature increases, weekly sales may slightly decrease and vice versa. Although, this result does not give a clear correlation or relationshiop between temperature and weekly sales.*

5. Correlatiion between fuel price and sales.

               SELECT 
                     Weekly_Sales,
                     Fuel_Price
               FROM 
                    `my-sandbox-project-417117.Walmart.walmart_data`
               ORDER BY 
                     Fuel_Price DESC;

   ![Sheet 1 (7)](https://github.com/user-attachments/assets/8948cc3f-c607-402f-a1d7-7f2270554046)

*This shows that fuel price have little or no impact on Walmart's weekly sales* 

6. Correlation between CPI and Sales.

             SELECT 
                  Weekly_Sales,
                  CPI
             FROM 
                 `my-sandbox-project-417117.Walmart.walmart_data`
             ORDER BY 
                  CPI DESC;
  
   ![Sheet 2 (2)](https://github.com/user-attachments/assets/7f275f6b-dd61-43e0-9e10-07412fbb767d)

*As the CPI increases which shows a high inflation of consumer prices, the weekly sales may slightly reduce, and vice versa. This result shows little or no relationship between CPI 
 and weekly sales*
 
 7. Now we look at how unemployment is impacting weekly sales

         SELECT Store,
               Weekly_Sales,
               Unemployment
         FROM `my-sandbox-project-417117.Walmart.walmart_data`
         ORDER BY Unemployment DESC
         LIMIT 16
   
![image](https://github.com/user-attachments/assets/1f5bccff-61bd-4e96-8e9f-88214ddb7d5e)

*This query shows that the highest unemployment rate was 14.313 and it happened in store 12, store 28 and store 38.*

 Now we run another query to show the lowest rate of unemployment

          SELECT Store,
                 Weekly_Sales,
                 Unemployment
          FROM `my-sandbox-project-417117.Walmart.walmart_data`
          ORDER BY Unemployment ASC
          LIMIT 5

![image](https://github.com/user-attachments/assets/1d793782-5fc8-4055-8d3c-46e305d33f3b)

*This query shows that the lowest unemployment rate was in store 4 at the rate 3.879*

![Weekly_Sales, Unemployment by Store](https://github.com/user-attachments/assets/7831fe59-f64a-4142-b4a1-a83bdd3f701f)

*This visual shows that there is no correlation between unemployment and weekly sales.*

### ACT

   + Since the data shows that the week with the highest number of sales are weeks leading to christmas, Walmart should increase the number of inventory to avoid shortages of products 
  during this period.
   + Additionally, we can suggest to hire more more workers this period to account for influx of customers during this period.
   +   There will not be any recommendation for temperature and fuel price as  we there was no positive or negative relationship with the sales price.                                                                               
