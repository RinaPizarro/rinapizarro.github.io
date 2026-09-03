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

This is an example of how we would use a calculated columns when we need a value for each output.