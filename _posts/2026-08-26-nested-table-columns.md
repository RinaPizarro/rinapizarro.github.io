---
layout: post
title: Nested Table Columns
categories: powerquery
description: This guide will explain working with nested table columns in the
  power query editor.
---


### Section 1 Table.Group

Before we can understand how nested table columns work, we should begin by understanding the *table.group()* function.

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

