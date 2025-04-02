# Reliance_sales_project
1.In this Power Bi (Business Intelligent) using 1997 -1998 reliance sales data across the world makes a report files
2.In this project I am using Microsoft Power Bi, Kaggle to Extract data of Reliance sales.
3.First I create did ETL (Extraction, Transform,  load)
4. Using Power Bi Extract file in .csv mode after that Tranform in precise and correct it.
5.There are 8 .csv file and 1 folder  using in this poject.
the 8 files are Product.csv, Region.csv, calender.csv, return-1997-1998.csv, customer.csv, stores.csv, and 2 sales file which is in inner folder (sales)
After the Extraction FIrst change the file original name to dimentiona and fact name like d_Products.csv, d_Region.csv, d_calender.csv. f_return, etc.
It only for developer they understand easily.
After the ETL Process we do data Modelling which is also a complex process.
In data Modelling first step is connect tables in modelling view. In Power BI this process is Automatic done but we disable the functionality and done by manually to understand better
After the connect of modelling view 
Start Another step that is DAX which also more complex process which take more time. DAX Stand for data analysis extration which 
In DAX we have good prior knowledge of Excel formulas
**DAX Process**
1. Add Calculated Column
Add new column on d_calender.csv that name is Weekend
Weekend = IF(OR(d_Calendar[Day Name] = "Saturday", d_Calendar[Day Name] = "Sunday"), "Y", "N")
Add two new column in d_customer.csv that name is Age and Priority
Age = YEAR(TODAY())- d_Customers[Birth_Year]
Priority = IF(d_Customers[homeowner] = "Y" && d_Customers[member_card] = "Golden", "High", "Standard")

2. ADD Measures
M_ALL_Transaction = CALCULATE([M_Total_Transaction], ALL(F_Transaction))
M_Previou_Month_Transaction = CALCULATE([M_Total_Transaction], PREVIOUSMONTH(d_Calendar[date]))
M_ALL_Returns = CALCULATE([M_Total_Return], ALL(f_Returns))
M_Previous_Month_Profit = CALCULATE([M_Total_Profit],PREVIOUSMONTH(d_Calendar[date]))
M_Previous_Month_Return = CALCULATE([M_Quantity_Returned],PREVIOUSMONTH(d_Calendar[date]))
M_Previous_Month_Revenu = CALCULATE([M_total_Revenu],PREVIOUSMONTH(d_Calendar[date]))
M_Profit_Margin = [M_Total_Profit]/[M_total_Revenu]
M_Quantity_Returned = SUM(f_Returns[quantity])
M_Quantity_Sold = SUM(F_Transaction[quantity])
M_Total_Cost = SUMX(F_Transaction, F_Transaction[quantity]*RELATED(d_Products[product_cost]))
M_Total_Profit = [M_total_Revenu]- [M_Total_Cost]
M_Total_Return = COUNTA(f_Returns[return_date])
M_total_Revenu = SUMX(F_Transaction, F_Transaction[quantity]* RELATED(d_Products[product_retail_price]))
M_Total_Transaction = COUNTA(F_Transaction[store_id])
M_Unique_Product = DISTINCTCOUNT(d_Products[product_id])
M_weekend = CALCULATE([M_Total_Transaction],d_Calendar[Weekend] = "Y")
M_YTD_Revenue = CALCULATE([M_total_Revenu],DATESYTD(d_Calendar[date]))
These Measures not stored in the memory.
