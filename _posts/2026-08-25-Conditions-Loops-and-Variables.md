---
layout: post
title: Conditions, Loops, and Variables
categories: powerautomate
description: This guide will explain how to use conditions, create loops, and
  use variables in Power Automate
---
Conditions, loops, and variables serve as building blocks for creating automated processes in Power Automate. Let's define the purpose of each of these functionalities.

- **Conditions** make conditions.
- **Loops** repeat actions.
- **Variables** store and manipultae data.

### Section 1 Variables

#### Section 1.1 Introduction to Variables

Variables store information that can be used later. For example, you may have a variable called *MyAge* that is equal to the integer 16.

`MyAge = 16`

In this example, MyAge is the variable name, and 16 is the value of the variable. Now that we understand the general concept of a variable, let's review the different kinds of variables.

- **String Variables** store text data such as words, sentences, and descriptions.
- **Integer Variables** store whole numbers.
- **Float Variables** store decimals for precision such as money and percentages.
- **Boolean Variables** store logic such as true and false
- **Array Variables** store a list of items.
- **Object Variables** store complex data structures with multiple properties.

#### Section 1.2 Initialize a Variable

To initialize a variable, search for the action named **Initialize Variable**. Let's configure out variable with the following fields as an example:

![](/assets/images/image.png){:height="250px"}

#### Section 1.3 Updating a Variable

Let's say you initialized a variable in the beginning of your flow. Later on, we decide to update the variable to a different value. To update a variable's value, search for the action named **Set Variable** for complete replacement or **Increment Variable** for numeric additions.

### Section 2 Conditions

#### Section 2.1 Introduction to Conditions

Let's say you're building a flow that show run only during certain buisness hours. Creating a condition would be excelt to check the day of the week and current hour. 

Conditions have three main components:

1. **Left Side**: the a value to evaluate
2. **Operator**: decide how you want to compare the value
3. **Right Side**: the value to compare against

You will also have the option to chose *and* or *or* for your conditional statents if you have multiple statements. If you only have one statement, you can keep the option as *and*. 

The final part will be *True* and *False* branches that come aftee your condition. If your input value evaluates to true in your conditional statement(s), then your *True* branch will run. Otherwise, your *False* branch will run.

If you're evaluating strings, you can use *Contains*. Similarily, you can use *Contains* to evaluate if an array contains a value. 

### Section 3 Loops

Section 3.1 Introduction to Loops
Loops are an excellent way to repeat the same action(s) with implenting the actions multiple times. There are two many loops in Power Automate:

1. Apply to Each
2. Do Until

#### Section 3.2 Apply to Each

**Apply to Each** is excellent for evaluating a series of actions against an array of items. For example, if you have a list of items in SharePoint List, using Apply to Each would apply the same series of steps to each item in the list.

##### Section 3.2.1 Example of accessing properties with Get Emails from Outlook

Let's say you are trying to pull a bunch of emails from Outlook with the action named **Get Emails**. You want to look at the time each email was received. When you run the Get Emails, the output will be an array of emails. 

Next, take that array of emails and pass it into the Apply to Each loop. Inside your loop, you can then access the various items and their properties. 

`items('Apply_to_each')?['receivedDateTime']`

- **items()** is a function that grabs the current item in the loop.
- **'Apply_to_each'** tells Power Automate the name of the loop you're referring to.
- **?** is the safe navigation operator. It tells Power Automate to continue searching if the value exists. If it does not, don't cause an error.
- **['receivedDateTime']** is the specific property from the current item.

#### Section 3.1 Do Until

This loop continues executing until the final condition is met. When using a Do Until, you will need some kind of way to increment a value. For example, you may continue searching for an array until you find a certain value, or you will need to increment the date in your search query until you search the end of the year. 

`Condition: length of array Operator: is equal to Value: 0`

#### Section 4 Best Practices

Now that we understand conditions, loops, and variables, let's understand some ground rules for using these functionalities.

- Always initialize a variable before beginning a loop or condition. Your variable can be initializex with *null* value if necessary. In your condition or loop, you can then increment the variable or set the variable to a new value. 
- Do Until can be stuck in an infinite loop if the value never evaluates to true. Therefore, always ensure you are updating your variables in some way that reaches your end condition.
- Ensure your process runs as efficiently as possible. Runtime performance can decrease depending on the complexity of your process.

