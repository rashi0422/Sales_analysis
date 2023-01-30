# Sales_analysis

-- data from date table--
SELECT * FROM sales.date;

-- no. of product sales in different year --
select year, count(year) as 'no._of_product_sale_year' from date group by year ; 

-- no. of product sales according to month --
select month_name , count(month_name) from date group by month_name;

-- show data in 2020 (join table) --
select sales.transactions.*, sales.date.* from sales.transactions INNER JOIN sales.date ON sales.transactions.order_date = sales.date.date where sales.date.year=2020;

-- calcualate sales in 2020 --
select sum(sales.transactions.sales_amount) as 'sales_in_2020' from  sales.transactions  INNER JOIN sales.date ON sales.transactions.order_date = sales.date.date where sales.date.year=2020;

-- calculate sales in 2020 accordingly to the market_code --
select market_code, sum(sales.transactions.sales_amount) as 'sales_in_2020' from  sales.transactions  INNER JOIN sales.date ON sales.transactions.order_date = sales.date.date where sales.date.year=2020 and sales.transactions.market_code='Mark001';

SELECT * FROM sales.products;

-- count rows --
select count(*) from products;

-- combine table transaction and product --
select sales.transactions.* , sales.products.* from sales.transactions inner join sales.products on sales.transactions.product_code = sales.products.product_code;

-- sales amount according to product_type --
select sales.transactions.market_code , sales.transactions.sales_amount , sales.products.product_type from sales.transactions inner join sales.products on sales.transactions.product_code = sales.products.product_code;

SELECT count(*) FROM sales.transactions;

-- top 5 rows --
select * from transactions  limit 5;

-- select data mark003 product code --
select * from transactions where market_code = 'Mark003';

-- count product has product code mark003 --
select count(*) from transactions where market_code = 'Mark003';

-- select USD currency --
select * from transactions where currency='USD';

-- show data where has no sale -- 
select * from sales.transactions where sales.transactions.sales_amount = 0;

-- how much quantity sells in different different market--
select market_code ,(sales_qty) from transactions group by market_code;

-- data from customers table --
SELECT * FROM sales.customers;

-- customers count present in table --
select count(*) from customers;

-- combined table transaction and customers --
select sales.transactions.* , sales.customers.* from sales.transactions Inner join sales.customers on sales.transactions.customer_code = sales.customers.customer_code;

-- total sales by Brick & Mortar --
(select sales.customers.customer_code, sales.transactions.sales_amount , sales.transactions.sales_qty  , sales.customers.customer_type from sales.transactions inner join sales.customers on sales.transactions.customer_code = sales.customers.customer_code);

-- caculate sales of Brick & Mortar --  
select sales.customers.customer_code, sales.transactions.sales_amount , sales.transactions.sales_qty  , sales.customers.customer_type from sales.transactions inner join sales.customers on sales.transactions.customer_code = sales.customers.customer_code;
-- create table B_M Values (select sales.customers.customer_code, sales.transactions.sales_amount , sales.transactions.sales_qty  , sales.customers.customer_type from sales.transactions inner join sales.customers on sales.transactions.customer_code = sales.customers.customer_code;)--
select customer_type, sum(sales_amount) from B_M group by customer_type;
