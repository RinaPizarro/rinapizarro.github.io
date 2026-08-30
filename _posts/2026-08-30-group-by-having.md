---
layout: post
title: GROUP BY, HAVING
categories: sql
---
### Section 1 Understanding Aggregation

Let's begin by understanding how our database breaks down aggregations:

1. Filtering Phase: WHERE clauses are applied first prior to aggregation
2. Grouping Phase: Records are grouped together with the GROUP BY
3. Aggregation Phase: Aggregate functions like SUM and COUNT are computed
4. Post Aggregation Phase: HAVING clauses filters the applied aggregations
5. Ordering Phase: ORDER BY is applied as the final step

