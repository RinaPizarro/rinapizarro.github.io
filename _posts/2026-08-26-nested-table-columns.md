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

Section 1.2 Example of *Table.Group()*

Section 1.2.1 Advanced Editor

Suppose we have a table about Uber drives. Let's say we want to group the rides by vehicle type and drop off location.

![](/assets/images/power_query_group_by_function.png){:width="300px"}

- Our *table* parameter is filled by our previous step named *#"Changed Type 1"*
- *Key* is filled by our two columns in the form of a list as *{"Vehicle Type", "Drop Location"}.* Notice how our column names are strings in a list.
- *aggregatedColumns* are also in the form of a list. We begin by specifying the output column name as *All Rides*. We then specify the type as table with a record of column names to be stores within our nested tables.

Our output end up looking something like this:

![](/assets/images/power_query_nested_table_columns.png){:width="300px"}

As you can see, we have our vehcile type and drop location as our key columns. Everything else got wrapped into our new column called *All Rides*.

Section 1.2.2 GUI

The advanced edtior is one way to group columns into tables. The second way is using the GUI in Power Query. In the *Home* tab, you'll click on your column(s) and select *Group By* in the ribbon. A new window will pop up where you can edit the *New Column Name* and select an *Operation*. For our purposes, we will select *All Rows* to create the table column.

![](/assets/images/power_query_group_by_gui.png)

{:width="300px"}

### Section 2 *Editing the Table Column*

Section 2.1 *table.transformColumns()*

Now that we have created our nested table column, we may want to create new columns, remove rows, or transform the data in general. To achieve this, we use the *table.transformcolumns()* function.

```
Table.TransformColumns(
    table as table,
    transformOperations as list,
    optional defaultTransformation as nullable function,
    optional missingField as nullable number
)
```

- *table* will be the previous step
- *transformOperations* will take the form of *{Column name as string, transformation, optional new column type}*

Now that we understand how the function works, lets use this function in our query. 

![](/assets/images/power_query_transform_nested_table_column.png){:width="300px"}

- We begin by defining our *table* as our previous step which was *#"Grouped Rows"*
- We then begin creating our list for *transformOperations*. Our nested table column is called *Vehicle Type*. We then add an *each* to tell Power Query to transform each row in the *Vehicle Type* column. We then use *Table.SelectRows()* to select the rows in each nested table that contains the text "he"

Section 2.2 Referencing outer table

Now that we know how to transform the nested table columns, we may want to consider how to reference our outer table. We will need to understand a few different functions to acheieve this.

```
Table.FromRecords(
    records as list,
    optional columns as any,
    optional missingField as nullable number
) 
```

- *records* is the list containg records that need to be converted to table
- *columns* is a list of the table column names

```
Record.TransformFields(
    record as record,
    transformOperations as list,
    optional missingField as nullable number
)
```

- `transformOperations` is expected to be a list with two items. The first item in `transformOperations` specifies a field name, and the second item in `transformOperations` specifies the function to be used for transformation. For example, `{"Quantity", Number.FromText}`



&nbsp;