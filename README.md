## Classic Model Sales Performance, Jan 2003 to may 2005
<img width="1500" height="800" alt="image" src="https://github.com/user-attachments/assets/452aa12b-3e2b-4687-962c-0c63a6ee3a0f" />

# Project Summary
Classic Models sells scale-model cars, motorcycles, planes, ships, trains, trucks and buses to retailers in 27 countries. This project builds one report that answers four questions: what sells, what earns profit, how fast orders ship, and which customers still owe money.

The dataset is a public sample. The business scenario below is my framing of how a sales manager or finance lead would use the data.

# Business Problem
### Sales, product, shipping and payment data sit in separate tables. A manager cannot see in one place:

- Which products, countries and customers drive revenue and profit
- Whether growth is real, because 2005 holds only five months of data
- Which months carry the most profit
- How quickly orders ship
- How much customers owe and who owes it

Without that view, decisions on stock, sales coverage and credit control rely on guesswork.

## Objective and Business Questions
Objective: To give management one report that covers sales, profit, orders and collections, with figures that compare fairly across years.

## Business Questions the report answers:

* How much did the business sell, and how did sales change by year on a like-for-like basis?
* Which product lines, products, countries, customers and sales reps drive sales?
* What is the gross profit and gross margin, and where does profit come from?
* Which months carry the most profit, and do sales show seasonality or anomalies?
* How many orders did the business take, what do they contain and how fast do they ship?
* How much of sales has customers paid, and who owes the most?

# Solution
I built a Power BI report with six pages: Overview, Sales, Profit, Orders and Payments that shows $9.37M in sales and $3.73M in gross profit, ranks products, countries, customers and reps, and lists the customers with unpaid balances.

# Tools
- MS Power BI
- Power Query
- DAX
- MS Excel

# Dataset
Source: Classic Models sample database, loaded as CSV files. The company is fictional and the data is for learning.

Period: January 2003 to May 2005. 2005 holds five months of data.

# Data Model
### The model has 8 source tables, one date table and one helper table.
<img width="1450" height="750" alt="image" src="https://github.com/user-attachments/assets/cbf2b796-9be3-40a7-8249-eb4b3f013971" />

Relationships, all many-to-one with single-direction filters:

Date table: a calendar from 1 January 2003 to 31 December 2005, built in DAX, with year, month, quarter and weekday columns.

UnassignedRep: a one-row table that holds a placeholder rep with employee number 0. I appended it to the employees table so customers without a sales rep still appear in rep analysis.

# Data Preparation
Steps I applied in Power Query:

- Promoted headers and set data types on every table
- Trimmed text in name fields and merged first and last names into one full name column
- Replaced the text value NULL with true nulls in state, shipped date and sales rep fields
- Removed duplicate customers on customer number
- Removed columns not used in the report, such as phone, address lines, postal code, comments and HTML descriptions
- Added calculated columns in order details: Sales, Cost of Sales and Profit
- Merged products into order details to bring in buy price
- Added order columns: month name, day name, shipping days and delivery bands
- Added a product stock flag that marks products with fewer than 1,000 units in stock as stock required

### Example, order details line-level calculations:

<img width="600" height="120" alt="image" src="https://github.com/user-attachments/assets/1814bb86-ce06-4f39-a826-66f9520f967d" />


# Key Measures
### Sales, cost and profit exclude cancelled orders.
<img width="500" height="200" alt="image" src="https://github.com/user-attachments/assets/0ea2a58d-e38b-4245-8494-1e7baefe6d8c" />

### Like-for-like growth. The measure compares the latest year with the prior year up to the same cut-off date, so a partial year does not distort the result.
<img width="500" height="160" alt="image" src="https://github.com/user-attachments/assets/bdea8e5b-07f8-44ed-899c-772a83966fa0" />

### Seasonality. The measure averages the yearly total for each month across the years that have orders in that month.
<img width="450" height="150" alt="image" src="https://github.com/user-attachments/assets/95d6949a-f76a-4dfd-b5e6-8eb47325b782" />

### Other Measures
<img width="500" height="180" alt="image" src="https://github.com/user-attachments/assets/3b6a4097-b6aa-4293-b347-daa1623c607e" />

# Key Findings
## Overview
<img width="1242" height="655" alt="image" src="https://github.com/user-attachments/assets/f5258ab0-e80a-47c7-933c-9d8637c0cab3" />

- Total sales are $9.37M from 326 orders. Average order value is $29.3K.
- Gross profit is $3.73M, a gross margin of 39.8%. Cost of sales is $5.63M.
- On a like-for-like January to May basis, sales rose from $0.77M in 2003 to $1.19M in 2004 and $1.77M in 2005.
- Classic Cars lead with $3.8M, about 41% of sales. Vintage Cars follow with $1.8M. Together they make up about 60% of sales.
- The USA is the largest market at $3.2M, about 34% of sales. Spain and France follow at $1.1M and $1.0M.

## Sales
<img width="1200" height="600" alt="image" src="https://github.com/user-attachments/assets/0112267a-944d-49e1-9a47-eec0398e8f23" />

- Daily sales spike between October and December. Sales dipped on 4 August 2004.
- The 1992 Ferrari 360 Spider red is the top product by sales at $0.27M. It is also the top product by units, with 1,808 units.
- Euro+ Shopping Channel is the largest customer at $773.6K, about 8% of sales. The top two customers account for about 15%.
- 98 of 122 customers placed at least one non-cancelled order.

## Profit
<img width="1200" height="650" alt="image" src="https://github.com/user-attachments/assets/61cc4133-88f1-42b3-bb39-675e0f8f28d6" />

- Gross profit growth on a like-for-like basis is 44.4%. It trails sales growth of 48.3%, so margin narrowed slightly in 2005.
- Classic Cars generate $1.49M in gross profit, about 40% of the total. Vintage Cars add $0.72M.
- Average gross profit peaks in November at $389K. June is the lowest month at $72K. October to December together hold about 45% of the average annual gross profit.
- Margin by product ranges between roughly 20% and 60%. Profit depends more on sales volume than on margin.


## Orders and Fulfilment
<img width="1200" height="650" alt="image" src="https://github.com/user-attachments/assets/c97800fa-4ac7-4d13-9dcd-f7d9b085c080" />

- Customers ordered 105.5K units, an average of 324 units per order.
- Classic Cars lead unit volume with 36K units, followed by Vintage Cars with 23K.
- Unit volume is spread across vendors. The top six vendors each supply between 8.4K and 9.7K units.
- Of the 312 orders with a ship date, 307 shipped within six days and 5 took seven days or more.

## Payment
<img width="1200" height="650" alt="image" src="https://github.com/user-attachments/assets/43bfd3e1-46b4-46ff-bc06-8d42c6dfa94f" />

- Customers paid $8.85M of $9.37M in sales. The outstanding balance is $511.5K, about 5.5% of sales.
- Eight customers hold $407.9K of the balance, about 80%.
- The USA has 36 customers, more than any other country. Germany has 13 and France has 12.

# Recommendations

1. Plan stock and staffing for October to December. These months carry about 45% of average annual gross profit, and November is the peak.
2. Protect the Classic Cars and Vintage Cars lines. They carry about 60% of sales, so a supply problem in either line affects the whole business.
3. Review credit terms for The Sharp Gifts Warehouse and La Rochelle Gifts. Both have unpaid shares well above the 5.5% company average.
4. Set a collection routine for the top eight balances. They hold about 80% of the amount owed.
5. Reduce reliance on a few reps and customers. The top three reps account for about 34% of sales and the top two customers for about 15%.
6. Review the weakest products, which sell $28K to $33K each, for discount, bundling or removal.
7. Investigate why gross profit grew more slowly than sales in 2005. Check discounts, product mix and buy prices.
8. Keep the shipping standard. Almost all orders ship within six days, so the focus is the 5 late orders and the 14 orders not shipped.










