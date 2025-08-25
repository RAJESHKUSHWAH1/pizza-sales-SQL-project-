# pizza-sales-SQL-project-
pizza sales

This project focuses on analyzing pizza sales data to uncover insights into customer preferences, sales performance, and business trends. Using data analysis techniques, the project identifies key factors that drive sales and provides actionable insights for decision-making.

🎯 Objective

To transform raw pizza sales data into meaningful insights that can help improve business strategies, optimize inventory, and enhance customer experience.

📊 Key Features

Data cleaning and preprocessing for accurate analysis

Exploratory Data Analysis (EDA) with visualizations

Identification of top-selling and least-selling pizzas

Sales trends by time, day, and month

Analysis of revenue contribution by pizza category and size

Insights to support business growth and customer satisfaction


----data cleaning

select * from pizza_sales
where pizza_id is null or 
	order_id is null  or
	pizza_name_id is null or
	quantity is null or
	order_date is null or
	order_time is null or
	unit_price is null or
	total_price is null or
	pizza_size is null or
	pizza_category is null or
	pizza_ingredients is null or
	pizza_name is null 

---check duplicate------
select pizza_id,count(*) from pizza_sales
group by pizza_id
having count(*)>1


---For KPI----------


select round(sum(total_price),2) "Total Revenue" from pizza_sales

select (sum(total_price)*100/count(distinct order_id)) as 'Average Order'  from pizza_sales

select sum(quantity) as 'Total pizza sold' from pizza_sales

select count(distinct order_id)as 'Total order' from pizza_sales


select cast(cast(sum(quantity)as decimal(10,2))/
cast(count(distinct order_id)as decimal(10,2))as decimal(10,2)) as 'Average pizza per order'
from pizza_sales


---for Visualization -------

--*******daily Trend for Total orders--------
select DATENAME(DW,order_date)as 'order_day',count(distinct order_id) as 'Total order' from pizza_sales
group by DATENAME(Dw,order_date)

--*****monthly trend for total Order 

select DATENAME(MONTH,order_date)as 'month_name',count(distinct order_id) as 'Total order' from pizza_sales
group by DATENAME(MONTH,order_date)
order by [Total order] desc

*****-percentage of sales by pizza category

select pizza_category, sum(total_price) *100 /(select sum(total_price) from pizza_sales
where month(order_date)=1) as 'percentage of total sales' 
from pizza_sales
where month(order_date)=1
group by pizza_category


 ----***********for 1st month i.e january**************



 ---*******percentage of total sales by pizza size

select pizza_size,sum(total_price)*100/(select sum(total_price) from pizza_sales
where month(order_date)=1) as 'percentage of total sales by pizza size'
from pizza_sales
where month(order_date)=1
group by pizza_size


---**********top 5 best seller by Revenue ,total Quantity and total orders




select  top 5 pizza_name,sum(total_price)as 'Total_Revenue' from pizza_sales
group by pizza_name
order by Total_revenue desc

select  top 5 pizza_name,sum(Quantity)as 'Total_qautity' from pizza_sales
group by pizza_name
order by Total_qautity desc

select  top 5 pizza_name,count(distinct order_id)as 'Total_order' from pizza_sales
group by pizza_name
order by total_order desc


---**********bottom 5 best seller by Revenue ,total Quantity and total orders


select  top 5 pizza_name,sum(total_price)as 'Total_Revenue' from pizza_sales
group by pizza_name
order by Total_revenue asc

select  top 5 pizza_name,sum(Quantity)as 'Total_qautity' from pizza_sales
group by pizza_name
order by Total_qautity asc

select  top 5 pizza_name,count(distinct order_id)as 'Total_order' from pizza_sales
group by pizza_name
order by total_order asc


