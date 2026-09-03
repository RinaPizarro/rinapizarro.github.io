---
layout: post
title: Calculate and Filter in DAX
categories: powerbi
description: This guide will explain how to use calculate and filter in your DAX
  expressions.
---
CALCULATE() modifies filter context.

```
CALCULATE(<expression>, <filter1>, <filter2>, ...)
```

Calculate ignores current filters. If you have a date slicer, your calculate will ignore the date slicer and calculate the original table model.