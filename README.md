# Fall 2021 Data Science Intern Challenge 

Please complete the following questions, and provide your thought process/work. You can attach your work in a text file, link, etc. on the application page. Please ensure answers are easily visible for reviewers!


**Question 1:** Given some sample data, write a program to answer the following: [click here to access the required data set](https://docs.google.com/spreadsheets/d/16i38oonuX1y1g7C_UAmiK9GkY7cS-64DfiDMNiR41LM/edit#gid=0)

- On Shopify, we have exactly 100 sneaker shops, and each of these shops sells only one model of shoe. We want to do some analysis of the average order value (AOV). When we look at orders data over a 30-day window, we naively calculate an AOV of $3145.13. Given that we know these shops are selling sneakers, a relatively affordable item, something seems wrong with our analysis.  

    - Think about what could be going wrong with our calculation. Think about a better way to evaluate this data.  
        - What went wrong here was that there were a lot of outliers (values that were not within the range of the majority of values). 
        - A better way to evaluate this data is to remove the outliers first before attempting to get the mean (average) value, since the outliers would rarely occur in other situations.

    - What metric would you report for this dataset?
        - You can still get the mean for this dataset if you remove the outliers to get a more realistic average. However, if you did not want to remove any of the data from the dataset, you could also use median instead of mean, and it would be more accurate than the mean in this case.

    - What is its value?
        - By removing the outliers and then calculating the mean, the average value of orders is --> **$230.46**
        - Without removing the outliers and just going based on the median calculations the value is --> **$284.00**


**Question 2:** For this question you’ll need to use SQL. [Follow this link](https://www.w3schools.com/SQL/TRYSQL.ASP?FILENAME=TRYSQL_SELECT_ALL) to access the data set required for the challenge. Please use queries to answer the following questions. Paste your queries along with your final numerical answers below.

1. How many orders were shipped by Speedy Express in total?
    - My thought process:
        1. Need to find what table(s) have the shipper names listed. 
            - Found the shipper names and id numbers in the `Shippers` table.
        2. Need to next find the table(s) where I would get all the orders that the shipper shipped.
            - Found that all orders and shipper ids are in the `Orders` table.
        3. Need to join the `Shippers` and `Orders` table together on the `ShipperID` column.
        4. Get the `COUNT` of how many orders were shipped by "Speedy Express" only.
    ```
    SELECT COUNT(ord.ShipperID)
    FROM Shippers AS ship 
        JOIN Orders AS ord ON Ord.ShipperID = ship.ShipperID
    WHERE ship.ShipperName = "Speedy Express";
   
    --> Result = 54
    ```

2. What is the last name of the employee with the most orders?
    - My thought process:
        1. Need to find the table(s) with employee last names.
           - Found the `Employees` table has the `LastName` of the employees and their `EmpployeeID`.
        2. 
    ```
    
    ```

3. What product was ordered the most by customers in Germany?
    ```
    
    ```
