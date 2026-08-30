---
layout: post
title: IN operator
categories: sql
description: This guide will explain how to use IN operator in SQL.
---
***IN*** is an operator that tells the database whether a value exists in a specified list of values. 

```
test_expression [ NOT ] IN   
    ( subquery | expression [ ,...n ]  
    )   
```

- *test_expression* is any valid expression
- *subquery* has a result set of one column. This column must have the same data type as *test_expression*.
- *expression[ **,**... n ]* is a list of expressions to test for a match. All expressions must be of the same type as *test_expression*.

An example of this in practice is if we have multiple OR conditions.

```
SELECT * FROM customer_transactions
WHERE customer_country = 'United States'
   OR customer_country = 'Canada'
   OR customer_country = 'Mexico'
   OR customer_country = 'United Kingdom'
   OR customer_country = 'Australia';
```

Instead of writing multiple OR statements, we can simply use an IN statement.

```
SELECT * FROM customer_transactions
WHERE customer_country IN ('United States', 'Canada', 'Mexico', 
                           'United Kingdom', 'Australia');
```

This makes the syntax easier to read and edit (such as if we need to add or remove a value from the IN statement). 

