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

![](/assets/images/m_language_applied_steps.png){:height="150px"}

These are all of our steps from the advanced editor. When you are creating your steps in the advanced editor, please note the following:

- If your step name has spaces, use *#"Insert Name Here"* 
- If your step name does not have spaces, you can use *InsertStepName* or *insert_step_name*

### Section 2 Data Types

Section 2.1 Primative Types

- *Number* holds intergers and decimals
- *Text* are strings enclosed in double quotes 
  - *"John Smith"*
- *Logical* are boolean values of *True* and *False*
- *Date, DateTime* and *Time* 
  - *#date(2026,05,24)*
  - *#datetime(2026,05,24,13,30,0)*
  - *#time(13,30,0)*
- *Null* represent missing or unknown values

Section 2.2 Complex Data Types

- *Lists* are an ordered collection of values.
  - Lists are represented with curly brackets.
  - Each item in a list is seperated by a comma.
  - *{"John Smith", "Carol Baskin", "Emily White"}*
- *Records* are a single row of data
  - Records are represented with square brackets
  - Each records contains one or more *Fields = Value* where *Fields* would be your column name in a table with a *Value* associated with each field.
  - *[Name = "John Smith", Age = 17, IsMarried = True]*
    - Name, Age, and IsMarried are considered fields
    - To access a value such as Name, you would use the syntax *RecordName[Name]*
- *Tables* are a structured collection of rows and columns
  - The function *Table.FromRows()* can be used to create your own custom table. 

```
Table.FromRows(rows as list, optional columns as any) as table
```

![](/assets/images/m_language_create_table_type.png){:height="300px"}

- *Functions* can be assigned to variables

![](/assets/images/m_language_create_function_type.png){:height="300px"}

### Section 3 Expressions

Section 3.1 Comparison Expressions