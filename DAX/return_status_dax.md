# DAX Calculations Used in the Power BI Project

## 1. Return Status (Calculated Column)

The Global Superstore Returns table contains only entries for orders that were returned.  
To identify both returned and non-returned orders, we created a calculated column inside the **Orders** table using the following DAX expression:

```DAX
Return Status =
IF(
    CONTAINS(Returns, Returns[Order ID], Orders[Order ID]),
    "Yes",
    "No"
)
```

### Purpose:
- The Returns table contains only “Yes” entries
- The Orders table contains all orders
- This column allows us to:
  - Display **Returned vs Non-Returned** order counts
  - Build a proper Return Status Overview chart
  - Avoid relying solely on the Returns table

### Visuals Using This DAX:
- Return Status Overview (Column Chart)
- KPI Card for Return Rate (optional)
- Segment-wise or Category-wise return analysis

---

## 2. Return Rate (DAX Measure)

This measure calculates the proportion of orders that were returned.

```DAX
Return Rate =
DIVIDE(
    COUNTROWS(Returns),
    DISTINCTCOUNT(Orders[Order ID])
)
```

### Purpose:
- Defines KPI for return percentage
- Helps evaluate operational efficiency
- Used in Return Rate KPI card
- Helps correlate returns with category, region, or segment

---

## Additional Notes

You can extend this project with more DAX measures, such as:

### Profitability Measures
```DAX
Profit Ratio = 
DIVIDE(SUM(Orders[Profit]), SUM(Orders[Sales]))
```

### Year-to-Date Sales (requires Date table)
```DAX
YTD Sales =
TOTALYTD(
    SUM(Orders[Sales]),
    'Date'[Date]
)
```

### Month-to-Date Sales
```DAX
MTD Sales =
TOTALMTD(
    SUM(Orders[Sales]),
    'Date'[Date]
)
```

These can further enhance the analytical capability of the dashboard.

---

## File Information
**File Name:** return_status_dax.md  
**Folder:** /DAX  
**Project:** Power BI Global Superstore Dashboard

This file documents all custom DAX calculations used in the project for clarity, reproducibility, and version control.
