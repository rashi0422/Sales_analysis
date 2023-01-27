# Sales_analysis

-- data from date table--

SELECT * FROM sales.date;

-- no. of product sales in different year --

select year, count(year) as 'no._of_product_sale_year' from date group by year ; 

-- no. of product sales according to month --

select month_name , count(month_name) from date group by month_name;
