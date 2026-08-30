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
// 5
```

*UPPER()* and *LOWER()*



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

![image.png](/assets/images/image.png)

![image.png](/assets/images/image-1.png)

