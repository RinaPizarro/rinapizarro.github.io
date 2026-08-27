---
layout: post
title: Syntax, Types, and Expressions for M Language
categories: powerquery
description: "This guide will explain the syntax rules, data types, and
  expressions for M language. "
---
Learning M language is incredibly valuable for when Power Query's GUI editor poses limitations to your work. M language allows user to create complex logic and transformations that would be nearly impossible with the GUI. This guide will explain the basic building blocks to M language. 

### Section 1 Structure

```
let
    [insert steps]
in
    [insert output step]
```

- *Let* defines a series of steps, which are variables with values. 
- *in* specifies what the query should return.

Inside the *Let* block, we define a series of steps. Each steps is defined by a name and followed by various functions and transormations. When you open the advanced edtitor, you'll typically see something like this:



&nbsp;

&nbsp;