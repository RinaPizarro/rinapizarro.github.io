---
layout: post
title: Calculated Columns and Measures
categories: powerbi
description: Calculated Columns and Measures serve slightly different purposes.
  This guide will explain how calculated columns and measures can be used.
---
### Section 1 Row Context versus Filter Context

Calculated columns produce an output or value based off the current row. Calculated columns work methodologically through each row.

Measures look at a group of items based on any current filters that have already been applied. 

In a real world example, a calculated columns produce would be best if you are trying to calculate the total cost of each sale row.


| Item Name | Price | Quantity | Total |
| --------- | ----- | -------- | ----- |
| Book | 5.40 | 1 |  |
| Pencil | 1.29 | 2 |  |


```
Total = SalesTable[Price] * SalesTables[Quantity]
```

This is an example of how we would use a calculated columns when we need a value for each output. You could also use categories. For example, we would make a calculated columns called "Quality" that tells us the quality of each item.

```
Quality =
SWITCH(
     TRUE(),
     SalesTable[Item] = "Book", "Low",
     SalesTable[Item] = "Pens", "Low",
     "High"
      )
)
```

Now if we want the sum of all the total prices, we can use a measure:

```
TotalSum = SUM(SalesTable[Total])
```

If you have regions of the United States (East, West, South, North) you could do the following

1. Create a calculated columns called that calculates the total of products sold in each region
2. Create a visual that shows each region in the United States
3. Create a measure that calculates the sum of the calculated columns called.
4. Please the measure in the visual. All four regions will remain the same but now we get the sum of each region's products sold.

