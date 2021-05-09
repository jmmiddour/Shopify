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
   
    Result --> 54
    ```

2. What is the last name of the employee with the most orders?
    - My thought process:
        1. Need to find the table(s) with employee last names.
            - Found the `Employees` table has the `LastName` of the employees and their `EmpployeeID`.
        2. Need to find the table(s) with the employee ids, and the orders that employee processed.
            - Found that the `Orders` table has the information that I need
        3. Need to calculate the total orders for each employee id.
        4. Then need to sort those totals by value in descending order.
        5. Lastly, I will show only the employee's last name that is at the top of the list
    ```
    SELECT emp.LastName
    FROM Employees AS emp
        JOIN Orders AS ord ON ord.EmployeeID = emp.EmployeeID
    GROUP BY emp.EmployeeID
    ORDER BY COUNT(emp.EmployeeID) DESC
    LIMIT 1;
    
    Result --> Peacock
    ```

3. What product was ordered the most by customers in Germany?
    - My thought process:
        1. Find the table(s) where the customer's country is listed.
            - Found the country where the customer is in the `Customers` table. 
        2. Look at the `Products` table to see how I have to link it back to the `Customers` table, since it was the only one with the country where the customer resides.
            - There is a `ProductID` in the `Products` table that links to the `OrderDetails` table, which also has the `Quanitity` of the product ordered.
            - Then the `Orders` table is what links the `Customers` table to the `OrderDetails` table with `CustomerID` and `OrderID`.
        3. Going to need to do 3 inner joins in order to get all the information linked that I need.
        4. Have to have a conditional statement to only look at customers in Germany
        5. Need to get a sum for each product id
        6. Sort all the sums in descending order
        7. Finally, return the first value in the product name column.
    ```
    SELECT prod.ProductName
    FROM Products AS prod
        JOIN OrderDetails AS details ON details.ProductID = prod.ProductID
        JOIN Orders AS ord ON ord.OrderID = details.OrderID
        JOIN Customers AS cust ON cust.CustomerID = ord.CustomerID
    WHERE cust.Country = "Germany"
    GROUP BY prod.ProductName
    ORDER BY SUM(details.Quantity) DESC
    LIMIT 1;
   
    Result --> Boston Crab Meat
    ```
