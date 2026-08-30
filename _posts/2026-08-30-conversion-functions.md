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

*CONVERT()*

```
CONVERT(data_type(length), expression, style)
```

- *data_type* is the type to convert *expression* to. Can be one of the following: bigint, int, smallint, tinyint, bit, decimal, numeric, money, smallmoney, float, real, datetime, smalldatetime, char, varchar, text, nchar, nvarchar, ntext, binary, varbinary, or image
- *length* is the length of the resulting datatype, specifically for string datatypes like varchar. 
- *expression* is the value to convert
- *style* is the format to convert. 

*TO_DATE()*

```
TO_DATE(string, format_mask)
```

- *string* will be your column name or target string
- *format_mask* tells your database how to read the string. This could be something like *'YYYY-MM-DD'*

Please note that there are different formats.

- DD (01-31)
- DAY (full day of the week as Monday to Sunday)
- MM (01-12)
- MON (the abbreviation of the month)
- MONTH (full name of the month)
- YYYY
- YY

*TO_NUMBER()*

```
TO_NUMBER(string, format_mask)
```

- *string* is your number in type text
- *format_mask* specifies the format of the output

*TO_CHAR()*

```
TO_CHAR(NUMBER, FORMAT_MASK)
```

- *number* is your number or date to convert to string
- *format_mask* tells us how the string should be formatted



&nbsp;