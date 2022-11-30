# Using_CTE_PreparedStatement_JSON_in_MySQL
I use CTE to optimize a query, create a prepared statement to query a table, and use an inner join on a table with JSON datatype


I will be using these three tables to complete these tasks. I am showing the table columns instead of the table contents to save on space
![columns from orders](https://user-images.githubusercontent.com/106580846/204768773-81ad512e-3100-469d-a8c0-75026bb75625.png)
![columns from products](https://user-images.githubusercontent.com/106580846/204768818-998e14bb-151c-40d6-9244-cb6835ffb113.png)
![columns from activity](https://user-images.githubusercontent.com/106580846/204768831-14da1b9b-51b2-47c6-b838-0034524eb1b6.png)

Task 1

We need to find out how many orders were placed by clients with the following ClientIDs in 2022; Cl1, Cl2 and Cl3.  We could have used the following query to get this information, which works well if the table doesn't have many records.

SELECT CONCAT("Cl1: ", COUNT(OrderID), "orders") AS "Total number of orders" FROM Orders WHERE YEAR(Date) = 2022 AND ClientID = "Cl1" UNION SELECT CONCAT("Cl2: ", COUNT(OrderID), "orders") FROM Orders WHERE YEAR(Date) = 2022 AND ClientID = "Cl2" UNION SELECT CONCAT("Cl3: ", COUNT(OrderID), "orders") FROM Orders WHERE YEAR(Date) = 2022 AND ClientID = "Cl3";
![cte1](https://user-images.githubusercontent.com/106580846/204769461-9739c80d-ea9f-4970-812a-939e7d11e1cc.png)

However, we would be better off using a CTE optimize this query for a table with many records

![cte2](https://user-images.githubusercontent.com/106580846/204769541-27f54c85-93a2-49ec-b420-f28ce50e1096.png)

Task 2

We need to create a prepared statement called GetOrderDetail that will accept two input arguments: a ClientID value and a year value. 
The statement should return the order id, the quantity, the order cost and the order date from the Orders table.

![prepstatement 1](https://user-images.githubusercontent.com/106580846/204770319-59738b52-2ab6-4a30-871d-44d5eeeafa4d.png)

Then we declare the variables for clientID and YEAR

![variables](https://user-images.githubusercontent.com/106580846/204771331-96119a45-3200-4f1a-a05d-a680fdc4fbbf.png)

Finally we excecute the prepared statement

![statement executed](https://user-images.githubusercontent.com/106580846/204771367-f50f4381-0778-4026-90a8-b5de17dadab7.png)

Task 3

The ProductID and ClientID of every order is logged in a JSON Properties column in the Activity table.
This is the data content in the Activity table.

![activity table](https://user-images.githubusercontent.com/106580846/204772803-462dafb0-4c1e-4914-ac78-4920dcea99d4.png)

The task is to use the Properties column data to output the product id, name, buy price and sell price of the product where the Order value in the Activity table is True.

![results activity table](https://user-images.githubusercontent.com/106580846/204772985-a02a8091-032b-4f8e-ae38-ea37591e7a45.png)


