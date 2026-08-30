---
layout: post
title: GROUP BY, HAVING, COUNT, SUM, AVG
categories: sql
---
### Section 1 Understanding Aggregation

Let's begin by understanding how our database breaks down aggregations:

1. Filtering Phase: WHERE clauses are applied first prior to aggregation
2. Grouping Phase: Records are grouped together with the GROUP BY
3. Aggregation Phase: Aggregate functions like SUM and COUNT are computed
4. Post Aggregation Phase: HAVING clauses filters the applied aggregations
5. Ordering Phase: ORDER BY is applied as the final step

### Section 2 Aggregate Functions

Section 2.1 Introduction to Aggregate Functions

**Aggregate Functions** are functions that perform calculations on a set of value, and returns a single value. All aggregate functions ignore *null* values except for *COUNT(*).* Aggregate functions are **determinstic**, which are functions that always return the same result any time they are called with specific set of input values and given the same state of the database. Although we will only go through a a select few of aggregate functions, here are all the aggregate functions identified by Microsoft:

- ANY_VALUE
- APPROX_COUNT_DISTINCT
- AVG
- CHECKSUM_AGG
- COUNT
- COUNT_BIG
- GROUPING
- GROUPING_ID
- MAX
- MIN
- PRODUCT
- STDEV
- STDEVP
- STRING_AGG
- SUM
- VAR
- VARP

All of our examples will comebine aggregate functions with *GROUP BY()*. However, we don't always need to use the *GROUP BY()* function. 

Section 2.2 Common Aggregate Functions

*COUNT(*)*

- tells you how many rows meet the criteria

```
SELECT COUNT(*) FROM SalesTable
```

This query will tell us how many rows exist in the SalesTable

```
SELECT COUNT(*) FROM SalesTable GROUP BY CustomerName
```

This query tells us how many rows exist for each Customer in the SalesTable. 

*SUM()* 

- gives you total summation of a column

```
SELECT SUM(PaymentTotal) FROM SalesTable GROUP BY CustomerName
```

*AVG()* 

- gives you the average of a column

```
SELECT AVG(Price) FROM SalesTable GROUP BY CustomerName
```

*MIN()* and *MAX()*

- returns the minimum value or maximum value in a column (numbers, text, and dates)

```
SELECT MAX(SalesDate) FROM SalesTable GROUP BY CustomerName
```

Section 2.3 *HAVING()*