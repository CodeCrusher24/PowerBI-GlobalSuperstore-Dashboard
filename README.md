# Global Superstore Sales Performance Dashboard – Power BI

A complete business intelligence and data analysis project built using Microsoft Power BI.  
This dashboard provides insights into sales performance, profitability, customer segments, product behavior, and return patterns using the Global Superstore dataset.

---

## Project Overview

This project demonstrates the end-to-end workflow of developing a Power BI dashboard:
- Data ingestion
- Data cleaning and transformation
- Data modeling with relationships
- DAX-based calculations
- Building interactive and insightful visualizations
- Business insight extraction

---

## Dataset Information

**Dataset:** Global Superstore  
**Format:** Excel (.xlsx)  
**Rows:** 50,000+  
**Tables Included:**  
- Orders  
- Returns  
- People  

**Key Fields:**  
Sales, Profit, Quantity, Discount, Category, Sub-Category, Segment, Region, Country, Order Date, Ship Date, Customer details, Product details, Return status.

---

## Tools and Technologies Used

- Microsoft Power BI Desktop  
- Power Query  
- DAX (Data Analysis Expressions)  
- Excel  

---

## Steps Followed

### 1. Data Loading
Imported Orders, Returns, and People tables from an Excel file into Power BI.

### 2. Data Cleaning (Power Query)
- Verified and corrected data types  
- Removed duplicates  
- Promoted headers  
- Renamed inconsistent column names  
- Handled null postal codes appropriately  

### 3. Date Table Creation
Created a dedicated Date dimension table using M-code:

```m
= List.Dates(
    List.Min(Orders[Order Date]),
    Duration.Days(List.Max(Orders[Order Date]) - List.Min(Orders[Order Date])) + 1,
    #duration(1,0,0,0)
)
```
Added Year, Quarter, Month, and Month Number columns.

### 4. Data Modeling
Established relational connections between tables:

- `Date[Date]` → `Orders[Order Date]`
- `People[Region]` → `Orders[Region]`
- `Returns[Order ID]` → `Orders[Order ID]`

All relationships were configured using:
- Single-direction filtering  
- Appropriate cardinality (One-to-Many or Many-to-One)

This data model allowed the dashboard to support cross-filtering, dynamic slicers, and time intelligence functions.

---

### 5. DAX Calculations
Developed a calculated column to distinguish returned orders from non-returned ones, because the Returns table contains only returned entries.

```DAX
Return Status =
IF(
    CONTAINS(Returns, Returns[Order ID], Orders[Order ID]),
    "Yes",
    "No"
)
```
This enabled the creation of a Return Status Overview chart showing both “Yes” and “No” cases clearly.

### 6. Dashboard Visualizations
Built a complete Power BI dashboard with the following elements:

#### KPI Cards
- **Total Sales**  
- **Total Profit**  
- **Quantity Sold**  
- **Return Rate**

#### Charts Created
- **Line Chart:** Sales Trend Over Time (uses Date table for Year/Month drilling)  
- **Bar Chart:** Sales by Region  
- **Column Chart:** Profit by Category  
- **Tree Map:** Profit by Sub-Category  
- **Donut Chart:** Sales by Segment  
- **Bar Chart:** Top 10 Products by Sales (Top N filter applied)  
- **Column Chart:** Return Status Overview (using Orders[Return Status])

#### Slicers
- **Year** (Date table)  
- **Region** (Orders table)  
- **Segment** (Orders table)  
- **Category** (Orders table)

Formatting and usability features implemented:
- Consistent theme and color palette for readability  
- Data labels enabled where useful for quick interpretation  
- Titles and tooltips configured for clarity  
- Visual interactions adjusted to support focused analysis (Edit Interactions)  
- Proper sorting and Top N filtering applied for product ranking  
- Dashboard layout aligned and grouped for presentation

---

## Key Insights
- **Technology** is the most profitable category.  
- **West** region records the highest sales contribution.  
- **Consumer** segment generates the majority of overall sales.  
- Several sub-categories demonstrate high sales but low profit margins due to discounts or cost structure.  
- **Return analysis** highlights specific product groups and regions where returns are concentrated, indicating areas for operational review.

---

## Files Included
- `.pbix` Power BI project file (Power BI Desktop file)  
- Screenshots of the dashboard and data model (in `Screenshots/`)  
- DAX formulas used (in `DAX/`)  
- Dataset file in `Dataset/`  
- This `README.md` and supporting documentation

---

## Conclusion
This project demonstrates an end-to-end Power BI solution: data ingestion and cleaning, dimensional modeling, DAX-based logic, visualization design, and actionable insight generation. It showcases practical skills in data preparation, business intelligence, and storytelling with data.

---

## Author
**Parag Kumar**  
B.Tech CSE, SMVDU  
Business Intelligence | Data Analytics | Software Development

---

## License
This repository is provided for educational and academic use. Please credit the repository if its content is used in assignments or projects.
