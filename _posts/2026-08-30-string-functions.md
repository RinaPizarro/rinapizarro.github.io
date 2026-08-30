---
layout: post
title: "String Functions "
categories: sql
description: This guide will go over various string functions in SQL.
---
Sometimes we need to clean or format our text for comparison and extracting meaningful information. 

### Section 1 General Functions

*CONCAT()*

- Combines two or more strings into one string

```
SELECT CONCAT(FirstName, ' ', LastName) AS FullName
```

*CHAR_LENGTH()* or *LENGTH()*

- Returns the length of a string of characters

```
SELECT CHAR_LENGTH('Hello') AS 'String Length'

// output: 5
```

*UPPER()* and *LOWER()*

- Converts entire string to uppercase or lowercase

```
SELECT UPPER('John Smith') as 'Capitalized'

// output: JOHN SMITH
```

*REPLACE()*

- replaces target substring with another string

```
SELECT REPLACE('Hello World', 'World', 'Bob') AS UpdatedString

// Output: Hello Bob
```

*TRIM()*

- Removed leading whitespaces

```
TRIM('Hello World    ')
```

*CONCAT_WS()*

- Join multiple string with a concatenator

```
SELECT CONCAT_WS('_', 'shoes', 'for', 'sale');

// output: shoes_for_sale
```

*FORMAT()*

- Format a number as a string in a specific way, often with commas for thousands or with a specific number of decimal places.

```
SELECT FORMAT(0.981 * 100, 'N2') + '%' AS PercentageOutput;

// output: 98.10%
```

### Section 2 Finding Substrings

Section 2.2 Functions for finding substrings

CHARINDEX() 

- Searches for a smaller string inside a larger string
- Return value: position number where smaller string starts

```
CHARINDEX(string that you want to find, column name or string)
```

SUBSTRING()

- Extracts portion of text string based on starting position and defined length
- Return value: string

```
SUBSTRING(string or column name, starting position, number of characters to extract from starting position)
```

LEFT() and RIGHT()

- Extracts a specified number of characters from beginning (left side) of a string if LEFT() or end (right side) if RIGHT()
- Return value: string

```
LEFT(string or column name, number of characters to extract)
```

Section 2.2 Example of finding substring

![](/assets/images/sql_finding_substring_example.png){:width="80px"}


![](/assets/images/sql_finding_substring_output.png){:width="200px"}



&nbsp;