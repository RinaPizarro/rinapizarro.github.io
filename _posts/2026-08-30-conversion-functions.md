---
layout: post
title: Conversion Functions
categories: sql
description: Sometimes we need to convert between data types. This guide will
  review various functions that achieve this goal.
---
*CAST()*

```
CAST(expression AS datatype(length))
```

- This function converts the value of any datatype into a target datatype.

```
SELECT CAST('2017-08-25' AS datetime)

// output: 2017-08-25 00:00:00.000
```

Although there are several conversions that can occur in SQL, and these conversions can be explained further in Microsoft's documentation.

![](/assets/images/sql_data_conversion_chart.png){:width="300px"}

&nbsp;