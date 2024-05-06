SELECT * FROM BIT_DB.CUSTOMERS LIMIT 20;

SELECT * FROM BIT_DB.JanSales LIMIT 20;

SELECT * FROM BIT_DB.FebSales;

**How many orders were placed in Janurary?
SELECT count(orderID)
FROM BIT_DB.JanSales
WHERE length (orderID)= 6
AND orderID<> 'orderID';

**How many of those orders were for an Iphone?
SELECT count (orderID) as TotalNum
FROM BIT_DB.JanSales
WHERE Product= 'IPhone'
AND length (orderID)= 6
AND orderID<>'orderID';

**Select the customer account numbers for all the orders that were placed in February.
select distinct cust.acctnum
from BIT_DB.customers cust
JOIN BIT_DB.FebSales feb
ON cust.order_id= feb.orderID 
where length (order_id)= 6
and order_id <>'orderID';

**Which product was the cheapest one sold in Januray, and what was the price?
SELECT Product,price
FROM BIT_DB.JanSales
WHERE length (orderID)=6
AND orderID<> 'orderID' LIMIT 1;

**What is the total revenue for each product sold in January?
SELECT sum (quantity)*price as revenue, product 
FROM BIT_DB.JanSales
GROUP BY product;

**Which products were sold in Feburary at 548 lincoln St, Seattle, WA 98101, how many of each were sold, and what was the total revenue?
SELECT product, quantity, SUM(quantity)*price as revenue
FROM BIT_DB.FebSales
WHERE location = '548 Lincoln St, Seattle, WA 98101';

**How many customers ordered more than 2 products at a time in Feburary, and what was the average amount spent for those customers?
SELECT  avg (quantity *price),count(distinct cust.acctnum)
FROM BIT_DB.FebSales Feb
INNER JOIN BIT_DB.customers cust
ON Feb.orderID = cust.order_id
WHERE Feb.quantity > (2)
AND length (orderid) = 6 
AND orderid<> 'orderid';

SELECT orderdate 
FROM BIT_DB.FebSales
WHERE orderdate between '02/13/19 00:00' AND '02/18/19 00:00';

SELECT location
FROM BIT_DB.FebSales
WHERE orderdate = '02/18/19 01:35';

SELECT sum(quantity)
FROM BIT_DB.FebSales
WHERE orderdate like '02/18/19%';

SELECT distinct Product, Price
FROM BIT_DB.FebSales
WHERE Product like '%Batteries%';

SELECT distinct Product, Price
FROM BIT_DB.FebSales
WHERE Price like '%.99';

**List all the products sold in Los Angeles in Februrary, and include how many of each were sold.
SELECT Product, sum (quantity )
FROM BIT_DB.FebSales
WHERE location like '%Los Angeles%'
GROUP BY Product;


**Which locations in New York recieved at least 3 orders in January, and how manu orders did they each receive?
SELECT jan.location, sum (cust.acctnum) as total
FROM BIT_DB.JanSales jan
INNER JOIN BIT_DB.customers cust
ON jan.orderID = cust.order_id
GROUP BY location like 'NY'
HAVING acctnum >=3;

**How many of each type of headphone were sold in February?
SELECT sum( quantity) as total, product
FROM BIT_DB.FebSales
WHERE product like '%headphone%'
GROUP BY product;

**What was the average amount spent per account in February?
SELECT SUM( quantity* price)/ count (cust.acctnum )as total
FROM BIT_DB.FebSales feb
INNER JOIN BIT_DB.customers cust
ON feb.orderID= cust.order_id
WHERE length (order_id)= 6
AND orderID<> 'order_id';

**What was the average quanitity of products purchased per account in February?
SELECT SUM(quantity* feb.product)/ count (cust.acctnum) as average
FROM BIT_DB.FebSales feb
INNER JOIN BIT_DB.customers cust
ON feb.orderID = cust.order_id
WHERE length (order_id)  = 6
AND orderID <> 'feb.product';

**Which product brought in the most reveneue in January and how much revenue did it bring in total?
SELECT product, SUm (quantity) *price as revenue 
FROM BIT_DB.JanSales
GROUP BY product 
ORDER BY (revenue) DESC LIMIT 1;
