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
 from 45 different walmart stores and 6436 rows. Since the data is a first party data it is ROCCC, we have access to their weekly Sales 
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
         FROM `my-sandbox-project-417117.Walmart.walmart_data`
         ORDER BY Store
                  Date ASC
         LIMIT 10

 ![image](https://github.com/user-attachments/assets/351e937b-34f9-4da6-ba7d-6c6a52875093)

  Now that we are sure of the data, lets do a further analysis.

 1. Firstly, we look at the total revenue generated for each stores 
           SELECT store,
                  SUM(Weekly_Sales) AS total_weekly_sales
           FROM `my-sandbox-project-417117.Walmart.walmart_data`
           GROUP BY Store
           ORDER BY total_weekly_sales DESC;
      
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

![image](https://github.com/user-attachments/assets/b1f1b1f7-f38d-446d-a243-576884e8155c)

![Sheet 1 (6)](https://github.com/user-attachments/assets/b9d983ab-6eba-4abf-b055-f666d0ff93bb)

*This shows that the year 2011 recorded the highest total sales while 2012 recorded the least sales*

 3. Now we look at what holiday is impacting weeekly sales
    
        SELECT Date,
               Weekly_Sales,
               Holiday_Flag
        FROM `my-sandbox-project-417117.Walmart.walmart_data`
        WHERE Holiday_Flag=1
        ORDER BY Weekly_Sales DESC

    ![image](https://github.com/user-attachments/assets/1cae7e96-adba-4ec0-9c7b-dc85b0aaf758)

*This query shows that the major holidays shown in the top 12 are mainly Thanksgiving and holidays like Christmas are not available. We can therefore not draw major conclusions using 
 this query*

4. Now we look at how unemployment is impacting weekly sales

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

