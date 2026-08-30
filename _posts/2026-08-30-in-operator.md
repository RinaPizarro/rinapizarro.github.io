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

