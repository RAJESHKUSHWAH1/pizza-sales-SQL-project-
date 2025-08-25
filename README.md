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




select  top 5 pizza_name,count(distinct order_id)as 'Total_order' from pizza_sales
group by pizza_name
order by total_order asc


