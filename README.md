# Brazilian-E-Commerce-PowerBI

An interactive Power BI report built on the Olist Brazilian e-commerce dataset (about 100,000 orders, 2016 to 2018). The project covers the full workflow: cleaning and shaping the data in Power Query, building a relational data model, writing DAX measures, and designing report pages to explore sales, delivery performance, customer reviews, payments and geography.

Dashboard preview

Overview page

Overview page: daily revenue trend, top 10 categories, KPI cards and year slicer

Analysis page

Analysis page: review score by delivery status, payment types, top 10 sellers, revenue vs last year and revenue YTD

Dataset

Source: Brazilian E-Commerce Public Dataset by Olist on Kaggle (https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce), published by Olist. All credit for the data goes to Olist; see the Kaggle page for the licence terms.

It comes as 9 linked CSV files: orders, order items, products, customers, sellers, payments, reviews, geolocation and a category translation table.

The raw data is not included in this repository. All monetary values are in Brazilian reais (BRL).

Key findings
Scale: 13.59M in revenue across 98,666 orders, with an average order value of 137.75 and an average delivery time of 12.5 days.
Growth: revenue was 6.16M in 2017, and Jan to Aug 2018 alone reached 7.39M.
Black Friday: 24 November 2017 was the highest revenue day in the data, at roughly 152K, and November 2017 was the strongest month.
Delivery drives reviews: orders delivered on time averaged a review score of 4.3, compared with 2.6 for orders delivered after the estimated date.
Top categories by revenue: health_beauty (about 1.26M), watches_gifts and bed_bath_table. Review scores vary by category, for example 4.18 for health_beauty against 3.62 for office_furniture.
Payments: credit card accounts for 78% of payment value and boleto (bank slip) for 18%.
Geography: sellers cluster in the south-east and south of Brazil, while customers are spread across the whole country.
What I built
Data preparation (Power Query)
Corrected data types for dates, prices and review scores across the tables.
Merged English category names into the products table and replaced missing categories with "Unknown".
Reduced the 1M-row geolocation table to one row per zip code prefix using Group By (average latitude and longitude), then merged the coordinates into the customers and sellers tables.
Removed unused columns (such as review comment text) to keep the model light.
Data model
Connected orders, order items, products, customers, sellers, reviews and payments with one-to-many relationships and single-direction filtering.
Created a Date table in DAX and marked it as the model's date table.
Worked around filter propagation: reviews and payments sit on the orders side of the model, so category-level views needed a CROSSFILTER measure to respond to filters coming from order items.
DAX
Calculated column: delivery status (on time or late, based on delivered date versus estimated delivery date).
Core measures: Total Revenue, Orders, Average Order Value, Average Delivery Days (AVERAGEX), Total Paid.
Reviews: Average Review Score using CALCULATE with CROSSFILTER.
Time intelligence: Revenue YTD (TOTALYTD), Revenue LY (SAMEPERIODLASTYEAR) and YoY %.
Ranking: Seller Rank with RANKX, used for a top 10 sellers table.
Report
Overview page: KPI cards, daily revenue trend, top 10 categories by revenue, and a year slicer.
Analysis page: review score by delivery status, payment type breakdown, top 10 sellers, monthly revenue against last year, and revenue YTD.
Maps: seller and customer revenue by location.
Category detail page: reached by drill-through from any category, showing orders, revenue, average review score and a monthly revenue trend for that category.
Running it yourself
Download the dataset from Kaggle (link above).
Open the .pbix file in Power BI Desktop.
If the data fails to load, go to Home → Transform data → Data source settings and point each file to where you saved the CSVs.
Tools

Power BI Desktop, Power Query (M), DAX
