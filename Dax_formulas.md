
Power BI DAX Formulas

This file contains the important DAX measures created for the Sales Dashboard project.

1. Total Sales

Total Sales = SUM(Sales_Dataset[Total Sales])

2. Total Orders

Total Orders = DISTINCTCOUNT(Sales_Dataset[Order_ID])

3. Total Customers

Total Customers = DISTINCTCOUNT(Sales_Dataset[Customer_ID])

4. Total Quantity

Total Quantity = SUM(Sales_Dataset[Quantity])

5. Average Age

Average Age = AVERAGE(Sales_Dataset[Age])

6. Average Unit Price

Average Unit Price = AVERAGE(Sales_Dataset[Unit Price])

7. Average Order Value

Average Order Value =
DIVIDE(
    [Total Sales],
    [Total Orders]
)

8. Sales Growth %

Sales Growth % =
DIVIDE(
    [Current Month Sales] - [Previous Month Sales],
    [Previous Month Sales]
)

9. Total Products

Total Products =
DISTINCTCOUNT(Sales_Dataset[Product])

10. Total Categories

Total Categories =
DISTINCTCOUNT(Sales_Dataset[Category])

11. Male Customers

Male Customers =
CALCULATE(
    [Total Customers],
    Sales_Dataset[Gender] = "Male"
)

12. Female Customers

Female Customers =
CALCULATE(
    [Total Customers],
    Sales_Dataset[Gender] = "Female"
)

13. High Value Customers

High Value Customers =
COUNTROWS(
    FILTER(
        VALUES(Sales_Dataset[Customer_ID]),
        CALCULATE(SUM(Sales_Dataset[Total Sales])) >
        AVERAGEX(
            VALUES(Sales_Dataset[Customer_ID]),
            CALCULATE(SUM(Sales_Dataset[Total Sales]))
        )
    )
)

14. Top Product Sales

Top Product Sales =
MAXX(
    VALUES(Sales_Dataset[Product]),
    CALCULATE(SUM(Sales_Dataset[Total Sales]))
)

1. Gender Count

Gender Count =
COUNT(Sales_Dataset[Customer_ID])

2. High Value Customers

High Value Customers =
COUNTROWS(
    FILTER(
        VALUES(Sales_Dataset[Customer_ID]),
        CALCULATE(SUM(Sales_Dataset[Total Sales])) >
        AVERAGE(Sales_Dataset[Total Sales])
    )
)

3. Lost Customers

Lost Customers =
[Total Customers] - [Repeat Customers]

4. Lowest Product Name

Lowest Product Name =
CONCATENATEX(
    TOPN(
        1,
        VALUES(Sales_Dataset[Product]),
        CALCULATE(SUM(Sales_Dataset[Total Sales])),
        ASC
    ),
    Sales_Dataset[Product]
)

5. Lowest Product Sales

Lowest Product Sales =
MINX(
    VALUES(Sales_Dataset[Product]),
    CALCULATE(SUM(Sales_Dataset[Total Sales]))
)

6. Repeat Customers

Repeat Customers =
COUNTROWS(
    FILTER(
        VALUES(Sales_Dataset[Customer_ID]),
        CALCULATE(COUNT(Sales_Dataset[Order_ID])) > 1
    )
)

7. Top Product Name

Top Product Name =
CONCATENATEX(
    TOPN(
        1,
        VALUES(Sales_Dataset[Product]),
        CALCULATE(SUM(Sales_Dataset[Total Sales])),
        DESC
    ),
    Sales_Dataset[Product]
)

8. Top Product Sales

Top Product Sales =
MAXX(
    VALUES(Sales_Dataset[Product]),
    CALCULATE(SUM(Sales_Dataset[Total Sales]))
)

9. Funnel Value

Funnel Value =
SUM(Sales_Dataset[Total Sales])

10. Sort Order

Sort Order =
SWITCH(
    Sales_Dataset[Category],
    "Electronics",1,
    "Clothing",2,
    "Food",3,
    4
)

11. Age Group

Age Group =
SWITCH(
    TRUE(),
    Sales_Dataset[Age] < 20,"Below 20",
    Sales_Dataset[Age] <= 30,"20-30",
    Sales_Dataset[Age] <= 40,"31-40",
    Sales_Dataset[Age] <= 50,"41-50",
    "50+"
)

12. Average Age

Average Age =
AVERAGE(Sales_Dataset[Age])

13. Average Age Growth %

Avg Age Growth % =
DIVIDE(
    [Current Avg Age]-[Previous Avg Age],
    [Previous Avg Age]
)

14. Female %

Female % =
DIVIDE(
    CALCULATE([Total Customers],Sales_Dataset[Gender]="Female"),
    [Total Customers]
)

15. Male %

Male % =
DIVIDE(
    CALCULATE([Total Customers],Sales_Dataset[Gender]="Male"),
    [Total Customers]
)

16. Price Growth %

Price Growth % =
DIVIDE(
    [Current Avg Price]-[Previous Avg Price],
    [Previous Avg Price]
)
Previous Month Sales =
CALCULATE(
    [Total Sales],
    DATEADD(
        Sales_Dataset[Order_Date],
        -1,
        MONTH
    )
)Current Month Sales =
SUM(Sales_Dataset[Total Sales])Sales Growth % =
DIVIDE(
    [Current Month Sales] - [Previous Month Sales],
    [Previous Month Sales],
    0
)Sales Growth % =
DIVIDE(
    [Current Month Sales] - [Previous Month Sales],
    [Previous Month Sales],
    0
)## Sales Growth Percentage

```DAX
Sales Growth % =
DIVIDE(
    [Current Month Sales] - [Previous Month Sales],
    [Previous Month Sales],
    0
)
```
