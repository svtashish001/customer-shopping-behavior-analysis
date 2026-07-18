# A PROJECT REPORT
ON
“CUSTOMER SHOPPING BEHAVIOUR ANALYSIS”
SUBMITTED TO
In partial fulfillment of the requirements for the degree of
BACHELOR OF COMPUTER APPLICATIONS
DR RAM MANOHAR LOHIYA AWADH UNIVERSITY
Ayodhya, Uttar Pradesh
SUBMITTED BY:
ASHISH KUMAR SRIVASTAVA
```
(23060100110009)
```
Under the Supervision of
ER. ABHAY DWIVEDI
Head of Department
COMPUTER APPLICATIONS
```
SESSION: 2025-26
```
SHRI LAL BAHADUR SHASTRI DEGREE COLLEGE
Gonda, Uttar Pradesh
CERTIFICATE 1
This is to certify that the project entitled "CUSTOMER SHOPPING BEHAVIOR
```
ANALYSIS", submitted by ASHISH KUMAR SRIVASTAVA (23060100110009)
```
of Bachelor of Computer Applications, 3rd Year, Shri Lal Bahadur Shastri Degree
College, affiliated to Dr. Ram Manohar Lohia Avadh University, for the award of
the bachelor's degree, is a bona fide record of work carried out by him under the
guidance of Er. ABHAY DWIVEDI.
The content of this project has not been submitted to any university or institute for
the award of any degree or diploma.
```
Date: 18/07/2026
```
```
Place: GONDA
```
____________________ ____________________
EXTERNAL EXAMINER INTERNAL EXAMINER
____________________ ____________________
HEAD OF DEPARTMENT PROJECT GUIDE
Er. Abhay Dwivedi
CERTIFICATE 2
This is to certify that I have personally worked on the dissertation entitled
"CUSTOMER SHOPPING BEHAVIOR ANALYSIS". The case study and data
mentioned in this report were obtained during genuine work done and collected by
me.
Any other data and information in this report that has been collected from an external
agency has been duly acknowledged.
```
Date: 18/07/2026
```
```
Place: GONDA
```
```
STUDENT:
```
ASHISH KUMAR SRIVASTAVA
```
(23060100110009)
```
ACKNOWLEDGEMENT
I would like to express my sincere gratitude to Er. Abhay Dwivedi, Head of
Department and project mentor, for his invaluable guidance, continuous support,
and encouragement throughout the course of this project. His insights and
suggestions were instrumental in shaping the direction and quality of this work.
I am also thankful to the Department of Computer Applications, Shri Lal Bahadur
Shastri Degree College, for providing me with the resources and environment
necessary to complete this project.
Finally, I extend my appreciation to my family and friends for their constant
motivation and support during the course of this project.
```
DATE: 18/07/26
```
```
PLACE: GONDA
```
```
STUDENT:
```
ASHISH KUMAR SRIVASTAVA
```
(23060100110009)
```
3
3
TABLE OF CONTENTS
SR
NO
TITLE
PAGE
NO
1 Introduction & Business Problem
04
2 Objectives of the Project
05
3 Tools & Technologies Used 05
4 Dataset Description 06
```
5 Data Preparation & Cleaning (Python) 07
```
```
6 Data Analysis (SQL) 08-12
```
7 Key Findings & Insights 13
8 Business Recommendations 14
9 Conclusion 15
10 References 15
11
4
4
1. Introduction & Business Problem
Retail businesses today generate vast volumes of data through everyday customer
transactions. Hidden within this data are valuable insights about customer
preferences, purchasing habits, and the factors that influence buying decisions.
This project analyses a real-world style customer shopping behaviour dataset to
help a retail company better understand its customers and improve sales,
satisfaction, and long-term loyalty.
1.1 Business Problem Statement
A leading retail company wants to better understand its customers' shopping
behaviour in order to improve sales, customer satisfaction, and long-term loyalty.
The management team has noticed changes in purchasing patterns across
demographics, product categories, and sales channels. They are particularly
interested in uncovering which factors — such as discounts, reviews, seasons, or
payment preferences — drive consumer decisions and repeat purchases.
The overarching business question addressed in this project is:
“How can the company leverage consumer shopping data to identify trends,
improve customer engagement, and optimize marketing and product strategies?”
1.2 Project Deliverables
1. Data Preparation & Modelling (Python): Clean and transform the raw
dataset for analysis.
2. Data Analysis (SQL): Organize the data into a structured format and run
queries to extract insights on customer segments, loyalty, and purchase
drivers.
3. Visualization & Insights: Identify key patterns and trends to enable data-
driven decisions.
4. Report & Presentation: Summarize key findings and business
recommendations.
2. Objectives of the Project
5
5
● To clean, transform, and prepare raw customer transaction data for
analysis.
● To analyse revenue contribution across gender, age groups, and product
categories.
● To evaluate the effect of discounts, promo codes, and subscriptions on
customer spending.
● To identify the best-performing products based on customer review
ratings and sales volume.
● To segment customers into New, Returning, and Loyal categories based on
purchase history.
● To compare shipping preferences and their impact on purchase amount.
● To generate actionable business recommendations to improve customer
engagement and revenue.
3. Tools & Technologies Used
Category Tool / Technology Purpose
Programming
Language
```
Python 3.9 (Pandas) Data cleaning, transformation
```
& feature engineering
Database PostgreSQL
Structured storage and SQL-
based analysis
Query Language SQL Aggregation, segmentation &
business queries
Environment Jupyter Notebook Interactive data analysis &
documentation
Connectivity SQLAlchemy, psycopg2 Loading the cleaned dataset
into PostgreSQL
Reporting MS Word / PowerPoint Documentation and
presentation of findings
6
6
4. Dataset Description
The dataset used for this project, customer_shopping_behavior.csv, contains
3,900 customer transaction records across 18 attributes, capturing demographic
details, purchase details, and behavioural attributes of customers.
# Column Description
1 Customer ID Unique identifier for each customer
```
2 Age Age of the customer (18–70 years)
```
3 Gender Male / Female
4 Item Purchased Name of the product purchased
5 Category
```
Product category (Clothing, Footwear,
```
```
Outerwear, Accessories)
```
```
6 Purchase Amount (USD) Transaction value in USD
```
7 Location Customer's state/location
8 Size Size of the product purchased
9 Color Colour of the product
10 Season Season of purchase
```
11 Review Rating Customer rating (2.5 – 5.0)
```
12 Subscription Status Whether customer is subscribed
13 Shipping Type Mode of shipping selected
14 Discount Applied Whether a discount was applied
15 Promo Code Used Whether a promo code was used
16 Previous Purchases Number of previous purchases by the customer
17 Payment Method Mode of payment used
18 Frequency of Purchases How often the customer shops
7
7
5. Data Preparation & Cleaning (Python)
The raw dataset was loaded and cleaned using the Pandas library in Python. The
following steps were performed to ensure data quality and analytical readiness:
5. Missing Value Treatment: The Review Rating column had 37 missing
values out of 3,900 records. These were imputed using the median rating of
the respective product category, preserving the category-level rating
distribution.
6. Column Standardization: Column names were converted to snake_case
```
(e.g., “Purchase Amount (USD)” → purchase_amount) for consistency and
```
ease of querying in SQL.
7. Feature Engineering – Age Group: Customers were segmented into four
quartile-based age groups — Young Adult, Adult, Middle-aged, and Senior
```
— using pd.qcut() for balanced demographic analysis.
```
8. Feature Engineering – Purchase Frequency (Days): The categorical
```
“Frequency of Purchases” field (e.g., Weekly, Monthly, Annually) was
```
mapped to an approximate numeric interval in days, enabling quantitative
frequency analysis.
9. Redundant Column Removal: The Promo Code Used column was found to
be identical to Discount Applied for all 3,900 records and was therefore
dropped to avoid duplication.
10.Database Loading: The cleaned DataFrame was loaded into a PostgreSQL
```
database (customer_behavior) using SQLAlchemy, enabling structured
```
SQL-based analysis.
After cleaning, the dataset contained zero missing values across all columns and
was ready for in-depth analysis.
8
8
```
SELECTgender,SUM(purchase_amount)ASrevenueFROMc
```
ustomer
```
GROUPBYgender;
```
SELECTcustomer_id,purchase_amountFROMcustome
r
```
WHEREdiscount_applied='Yes'ANDpurchase_amount>=(SELECTAVG(purchas
```
```
e_amount)FROMcustomer);
```
```
SELECTitem_purchased,ROUND(AVG(review_rating::numeric),2)ASavg_ratin
```
g
FROMcustomerGROUPBYitem_purchase
```
dORDERBYAVG(review_rating)DESC
```
```
LIMIT5;
```
6. Data Analysis (SQL)
The cleaned dataset was loaded into a PostgreSQL table named customer, and ten
business questions were answered using SQL queries. The queries and their key
results are presented below.
Q1. What is the total revenue generated by male vs. female customers?
```
Gender Total Revenue (USD)
```
Male 1,57,890
Female 75,191
```
Male customers contributed roughly 68% of total revenue (₹1,57,890) compared
```
```
to Female customers (₹75,191), largely because male customers make up 68% of
```
```
the customer base (2,652 vs 1,248).
```
Q2. Which customers used a discount but still spent more than the average
purchase amount?
The overall average purchase amount is $59.76. A total of 839 transactions met
both conditions — discount applied and spend at or above the average — showing
that discounts do not necessarily cap spending and can coexist with higher-value
purchases.
Q3. Which are the top 5 products with the highest average review rating?
9
9
```
SELECTshipping_type,ROUND(AVG(purchase_amount),2)FROMcust
```
omer
```
WHEREshipping_typeIN('Standard','Express')GROUP
```
```
BYshipping_type;
```
```
SELECTsubscription_status,COUNT(customer_id)AStotal_customers,ROUND(
```
```
AVG(purchase_amount),2)ASavg_spend,ROUND(SUM(purchase_amount
```
```
),2)AStotal_revenueFROM
```
customerGROUPBYsubscripti
```
on_status;
```
Rank Product Avg. Rating
1 Gloves 3.86
2 Sandals 3.84
3 Boots 3.82
4 Hat 3.80
5 Skirt 3.78
Q4. Compare the average Purchase Amounts between Standard and
Express Shipping.
```
Shipping Type Avg. Purchase Amount (USD)
```
Express 60.48
Standard 58.46
```
Express shipping customers spend marginally more on average ($60.48) than
```
```
Standard shipping customers ($58.46), suggesting a slight willingness to pay
```
more among customers who prioritize faster delivery.
Q5. Do subscribed customers spend more? Compare average spend and
total revenue between subscribers and non-subscribers.
Subscription Customers Avg. Spend Total Revenue
No 2,847 59.87 1,70,436
Yes 1,053 59.49 62,645
Interestingly, subscribed and non-subscribed customers spend almost the same
```
amount on average ($59.49 vs $59.87). Non-subscribers drive a much larger share
```
10
10
```
SELECTitem_purchased,ROUND(100.0*SUM(CASEWHENdiscount_applied='
```
Yes'THEN1ELS
```
E0END)/COUNT(*),2)ASdiscount_rateF
```
ROMcustomer
GROUP
BYitem_purchasedORDERBYdiscount_rat
```
eDESC LIMIT5;
```
```
WITHcustomer_typeAS(SELECTcustomer_id,previous_purchases
```
,CASEWHENprevious_purchases=1THEN'New'
WHENprevious_purchasesBETWEEN2AND10THEN'Returning'ELSE'Loya
l'END AScustomer_segment
```
FROMcustomer)SELECTcustomer_segment,COUNT(*)FROMcustomer_typeG
```
```
ROUPBYcusto mer_segment;
```
of total revenue simply because they make up 73% of the customer base —
subscription status alone is not a strong predictor of higher per-order spend.
Q6. Which 5 products have the highest percentage of purchases with
discounts applied?
```
Rank Product Discount Rate (%)
```
1 Hat 50.00
2 Sneakers 49.66
3 Coat 49.07
4 Sweater 48.17
5 Pants 47.37
Q7. Segment customers into New, Returning, and Loyal based on total
previous purchases.
Segment Definition
Number of
Customers
New 1 previous purchase 83
Returning 2–10 previous purchases 701
Loyal
More than 10 previous
purchases 3,116
11
11
```
WITHitem_countsAS(SELECTcategory,item_purchased,COUNT(customer_id)A
```
Stotal_orders,ROW
```
_NUMBER()OVER(PARTITIONBYcategoryORDERBY
```
```
COUNT(customer_id)DESC)ASitem_rankFROMcustomerGROU
```
P
```
BYcategory,item_purchased)SELECTitem_rank,category,item_pu
```
```
rchased,total_ordersFROMitem_countsWHEREitem_rank <= 3;
```
```
SELECTsubscription_status,COUNT(customer_id)ASrepeat_buyersFROMc
```
ustomer
WHEREprevious_purchases>5GRO
```
UPBYsubscription_status;
```
```
SELECTage_group,SUM(purchase_amount)AStotal_revenueFROMc
```
ustomer
GROUPBYage_groupORDERBYtotal_rev
```
enueDESC;
```
An overwhelming 80% of customers fall into the “Loyal” segment, indicating
strong repeat-purchase behaviour and a highly retained customer base.
Q8. What are the top 3 most purchased products within each category?
Category #1 Product #2 Product #3 Product
```
Clothing Blouse (171) Pants (171) Shirt (169)
```
```
Accessories Jewelry (171) Belt (161)
```
Sunglasses
```
(161)
```
```
Footwear Sandals (160) Shoes (150) Sneakers (145)
```
```
Outerwear Jacket (163) Coat (161) –
```
```
Q9. Are repeat buyers (more than 5 previous purchases) also likely to
```
subscribe?
```
Subscription Status Repeat Buyers (>5 purchases)
```
No 2,518
Yes 958
Repeat buyers are not predominantly subscribers — about 72% of repeat buyers
have not subscribed, suggesting subscription programs are under-utilised among
the most loyal customers and represent an untapped growth opportunity.
Q10. What is the revenue contribution of each age group?
12
12
```
Age Group Total Revenue (USD)
```
Young Adult 62,143
Middle-aged 59,197
Adult 55,978
Senior 55,763
Revenue is fairly evenly distributed across all four age groups, with Young Adults
```
contributing marginally more (₹62,143), indicating that the customer base is
```
broad and not overly reliant on any single age demographic.
13
13
7. Key Findings & Insights
● Male customers account for 68% of the customer base and contribute
```
68% of total revenue (₹1,57,890 out of ₹2,33,081).
```
```
● Clothing is the dominant category with 1,737 transactions (44.5%),
```
```
followed by Accessories (1,240), Footwear (599), and Outerwear (324).
```
```
● 80% of customers (3,116 out of 3,900) fall into the “Loyal” segment with
```
more than 10 previous purchases, reflecting strong customer retention.
```
● Subscription status has little effect on per-order spend ($59.49 for
```
```
subscribers vs. $59.87 for non-subscribers), but only 27% of customers
```
are subscribed — and even among high-frequency repeat buyers, 72%
remain non-subscribers.
```
● Discount usage is common (43% of all transactions) and does not
```
necessarily reduce spend — 839 discounted transactions still exceeded
the average purchase amount of $59.76.
```
● Express shipping customers spend slightly more on average ($60.48) than
```
```
Standard shipping customers ($58.46).
```
● Products such as Gloves, Sandals, Boots, Hat, and Skirt receive the
```
highest average customer review ratings (3.78–3.86 out of 5).
```
● Revenue is well distributed across age groups, with no single age bracket
```
dominating (range: $55,763 to $62,143).
```
```
● High-discount products (Hat, Sneakers, Coat, Sweater, Pants) all see
```
discount rates near 47–50%, indicating these items depend heavily on
promotions to drive sales.
14
14
8. Business Recommendations
11.Boost Subscription Enrolment: Since loyal, repeat buyers are largely
```
unsubscribed, target them with personalised subscription offers (e.g., free
```
```
shipping, early access) to convert transactional loyalty into a recurring
```
revenue stream.
12.Targeted Marketing for Female Customers: With female customers
contributing only 32% of revenue despite representing 32% of the base,
evaluate product assortment and marketing campaigns tailored to this
segment to grow share of wallet.
13.Rationalise Discount Strategy: Since discounts do not significantly suppress
```
spend, evaluate whether high discount-rate products (Hat, Sneakers, Coat)
```
can sustain slightly lower discount depths without hurting conversion,
improving margins.
14.Promote Express Shipping: Given express-shipping customers spend more
on average, consider bundling express delivery with mid-to-high value
orders or offering it as a loyalty perk.
```
15.Leverage Top-Rated Products: Feature high-rated items (Gloves, Sandals,
```
```
Boots, Hat, Skirt) more prominently in marketing campaigns and cross-sell
```
them alongside lower-rated but high-volume products.
16.Maintain Broad Age-Group Engagement: Since revenue is evenly spread
across age groups, continue diversified marketing rather than over-indexing
on a single demographic.
```
17.Re-engage New Customers: Only 83 customers fall in the “New” segment;
```
```
introduce onboarding incentives (first-purchase discounts, welcome offers)
```
to convert first-time buyers into returning customers faster.
15
15
9. Conclusion
This project successfully analysed 3,900 customer transaction records to uncover
actionable insights into shopping behaviour. Through systematic data cleaning in
Python and structured SQL analysis, the project identified key revenue drivers,
customer segments, and the impact of discounts, subscriptions, and shipping
choices on purchasing behaviour.
```
The analysis reveals a highly loyal customer base (80% classified as “Loyal”), a
```
male-dominated revenue mix, and a subscription programme that is currently
under-leveraged relative to customer loyalty. Discounts are widely used but do
not meaningfully cap spending, while shipping preference and product ratings
offer smaller but useful signals for targeted marketing.
The recommendations outlined in this report — particularly around subscription
conversion, discount rationalisation, and targeted marketing — provide a
practical roadmap for the company to strengthen customer engagement, optimise
marketing spend, and increase overall revenue.
10. References
● Customer Shopping Behavior dataset —
```
customer_shopping_behavior.csv (project dataset).
```
● Pandas Documentation — https://pandas.pydata.org/docs/
● PostgreSQL Documentation — https://www.postgresql.org/docs/
● SQLAlchemy Documentation — https://docs.sqlalchemy.org/
```
● Project Business Problem Statement Document (provided by project
```
```
guide).
```
PowerBIDesktop
1,0005000
YoungAdult
Middle-aged
Senior
Adult
SalesbyAgeGroup
100K
50K
0K
Clothing Accessories Footwear Outerwear
SalesbyCategory
2,000
1,500
1,000
RevenuebyCategor
y
0
Clothing Accessories Footwear Outerwear
RevenuebyAgeGrou
p
YoungAdult
Middle-aged
Adult
Senior
0K 20K 40K 60K
500
Customer Behavior Dashboard
3.9K
Number of Customers
$59.76
Average Purchase Amount
3.75
Average Review Rating
ShippingType
○ 2-DayShipping
○ Express
○ FreeShipping
○ NextDayAir
○ Standard
○ StorePickup
Gender
MaleFemale
SubscriptionStatus
YesNo
Category
%ofCustomersbySubscriptionStatus
Yes27%
No73%
