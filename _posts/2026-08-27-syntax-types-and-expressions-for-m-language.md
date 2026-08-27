---
layout: post
title: Syntax, Types, and Expressions for M Language
categories: powerquery
description: "This guide will explain the syntax rules, data types, and
  expressions for M language. "
---
Learning M language is incredibly valuable for when Power Query's GUI editor poses limitations to your work. M language allows user to create complex logic and transformations that would be nearly impossible with the GUI. This guide will explain the basic building blocks to M language. 

### Section 1 Structure

#### Section 1.1 Let and In Block

```
let
    [insert steps]
in
    [insert output step]
```

- *Let* defines a series of steps, which are variables with values. 
- *in* specifies what the query should return.

Inside the *Let* block, we define a series of steps. Each steps is defined by a name and followed by various functions and transormations. When you open the advanced edtitor, you'll typically see something like this:

![](/assets/images/m_language_syntax_example_1.png){:height="300px"}

- We beginning our *let* block by defining a *Source*. Here, wer are using a local .csv file for Uber ride bookings. 
- Our next step named *#"Promoted Headers"* referenced our previous step. The next step named *#"Changed Type"* referenced our previous step. Notice how its a pipeline of steps, each one referencing the previous step.

Section 1.2 Naming Conventions for Steps

As mentioned in *Section 1.1 Let and In Block*, the let block contains a serious of steps. All of these steps can be viewed in the righthand side of your query edtiro in the section labeled *Applied Steps*.