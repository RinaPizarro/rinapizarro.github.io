---
layout: post
title: Nested Table Columns
categories: powerquery
description: This guide will explain working with nested table columns in the
  power query editor.
---
### Section 1 *Table.Group()*

Section 1.1 Understanding *Table.Group()*

Before we can understand how nested table columns work, we should begin by understanding the *table.group()* function

```
Table.Group(
    table as table,
    key as any,
    aggregatedColumns as list,
    optional groupKind as nullable number,
    optional comparer as nullable function
)
```

- *table* is the table we want to use. Typically, this would be the name of our previous step in the query.
- *key* can be either be a single column, or it can be a list of columns that you wish to group together.
- *aggregatedColumns* are all the columns you want to included within the group.

Suppose we have a table with a bunch of columns such as total, price, customer ID, and product name. We can group all the CustomerIDs and get the total sum of price they paid for all products with the following expression:

```
= Table.Group( 
    Source,
    { "CustomerID" },
    { "Total", each List.Sum( _[Price] ), Int64.Type }
 )
```

Section 1.2 Example of *Table.Group*

Suppose we have a table about Uber drives. Let's say we want to group the rides by vehicle type and drop off location.

![](/assets/images/power_query_group_by_function.png){:width="300px"}



&nbsp;