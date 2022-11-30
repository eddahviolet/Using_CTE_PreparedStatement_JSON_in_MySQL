# Using_CTE_PreparedStatement_JSON_in_MySQL
I use CTE to optimize a query, create a prepared statement to query a table, and use join on a table with JSON datatype


I will be using these three tables to complete these tasks. I am showing the table columns instead of the table contents to save on space
![columns from orders](https://user-images.githubusercontent.com/106580846/204768773-81ad512e-3100-469d-a8c0-75026bb75625.png)
![columns from products](https://user-images.githubusercontent.com/106580846/204768818-998e14bb-151c-40d6-9244-cb6835ffb113.png)
![columns from activity](https://user-images.githubusercontent.com/106580846/204768831-14da1b9b-51b2-47c6-b838-0034524eb1b6.png)

Task 1
We need to find out how many orders were placed by clients with the following Client IDs in 2022; Cl1, Cl2 and Cl3.  We could have used the following query to get this information, which works well if the table doesn't have amany records
SELECT CONCAT("Cl1: ", COUNT(OrderID), "orders") AS "Total number of orders" FROM Orders WHERE YEAR(Date) = 2022 AND ClientID = "Cl1" UNION SELECT CONCAT("Cl2: ", COUNT(OrderID), "orders") FROM Orders WHERE YEAR(Date) = 2022 AND ClientID = "Cl2" UNION SELECT CONCAT("Cl3: ", COUNT(OrderID), "orders") FROM Orders WHERE YEAR(Date) = 2022 AND ClientID = "Cl3";
![cte1](https://user-images.githubusercontent.com/106580846/204769461-9739c80d-ea9f-4970-812a-939e7d11e1cc.png)

However we are going to use a CTE to optimize this query

![cte2](https://user-images.githubusercontent.com/106580846/204769541-27f54c85-93a2-49ec-b420-f28ce50e1096.png)

Task 2
