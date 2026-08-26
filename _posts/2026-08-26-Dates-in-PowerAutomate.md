---
layout: post
title:  "Date and Time in Power Automate"
categories: powerautomate
description: "Understanding date and time in Power Automate is crucial for retrieveing the correct date and time format."
---

This guide will explain how to work with date and functions in Power Automate. 

By default, Power Automate treats date and time in **Coordinated Universal Time (UTC).** To put UTC into perspective, note the following:

* London is around UTC+0
* New York City and Chicago are around UTC-5
* Tokyo is in UTC+9

Treat London as the starting point, and depending on where you wish the retrieve the date and time, you'll either go forward (UTC+) or backwards (UTC-).  

### Section 1 Functions
This section will cover the main functions you would need to begin working and understanding date and time in Power Automate.

#### Section 1.1 utcNow()
utcNow() returns the current date and time in UTC. 

 `2026-08-24T19:34:40.1234567Z`

* **2026-08-24** is the date in short date format
* **T** is the seperator between the date (left side) and the time (right side)
* **19:34:40** is the time formatted as HH:mm:ss
* **.1234566** is fractional seconds 
* **Z** indicates the datetime is in UTC. It is *not* local time. 

#### Section 1.2 formatDateTime()
formatDateTime() takes a date expressions and allows the user to format into a desired format

 `formatDateTime( Date, 'NamedFormat)`

* **Date** *required* is the date to be formatted
* **NamedFormat** *optional* is a numeric value of a the format to be used. The user may also specify the desired format in single quotations marks.

Here are the numeric formats for NamedFormat:
* **0** displays date or time
    * If date, displays as short date
    * if time, displays as short date
    * if date and time, displays both as short date and time
* **1** displays long time from local computer settings
* **2** displays short time from local computer settings
* **3** displays time from local computer settings
* **4** displays time in 24 hour format (HH:mm)

If the numerical value doesn't fit your formatting needs, you may also specify format in single quotation marks. Here are some examples:
* *'yyyy-mm-dd'*
* *'HH:mm:ss'*

#### Section 1.3 convertTimeZone()
This where we take the UTC datetime and convert to our desired timezone.

 `convertTimeZone( 'timestamp' , 'sourceTimeZone' , 'destinationTimeZone' , 'format')`

* **timestamp** is the datetime you want to convert
* **sourceTimeZone** is the timezone your timestamp is currently in
* **destinationTimeZone** is the desired time zone
* **format** *optional* is the desired format for your output

[Microsoft's timezones can be found on this page](https://learn.microsoft.com/en-us/windows-hardware/manufacture/desktop/default-time-zones?view=windows-11&utm_source=chatgpt.com)

#### Section 1.4 parseDateTime()
This function parses a string into a datetime object. 

#### Section 1.5 Extract Part of Date and Time
Here are functions that let you extract a specific part of your date and time.

* *Day()*
* *Month()*
* *Year()*
* *dayOfWeek()*
    * 0 is for Sunday, 6 is for Saturday
* *startOfDay()*
* *startOfMonth()*
* *endOfDay()*
* *endOfMonth()*

#### Section 1.6 Adding Date and Time
Here is a list of functions that allow you to add or subtract  to your date and time.

* *addDays()*
* *addHours()*
* *addMinutes()*
* *subtractDays()*
* *subtractHours()*
* *subtractMinutes()*

### Section 2 Examples with Functions

This function grabs the current date and time in UTC format

 `MyDate = utcNow()`

This grabs the current datetime in UTC, and then formats its output in short date.

 `MyFormattedDate = formatDateTime(utcNow(), 'yyyy-mm-dd')`

This grabs the currentdate in UTC and converts to Eastern Standard Time (EST).

 `MyLocalDate = convertDateTime(utcNow(), 'UTC', 'Eastern Standard Time')`

### Section 3 Search Query using Dates
If you are trying to retrieve emails from a certain date (or from range of dates), you will need to mnow how to format dates in tha searchquery. 

### Section 4 Recurrence Trigger

### Section 5 Buisness Hours
Sometimes you need your flow to run only during certain buisness hours. Lets say your company has buisness hours Monday-Friday 8am-5pm EST. You may want your cloud flow to run only during this hours.

#### Section 5.1 Condition action
Beginning with a condition action. You need to answer two questions

1. Is today a weekday?
2. Is the current hour within buisness hours?

Let's begin by grabbing today'a date 

`dayOfWeek(convertTimeZone(utcNow(), 'UTC', 'Eastern Time Zone'))`

Now let's grab the current hour

'int)formatDateTime(convertTimeZone(utcNow(), 'UTC', 'Eastern Time Zone), 'H'))`

We have today's date as a number and the current hour. Now we will see if the number is a weekday and current hour is within buisness hours.

#### Section 5.2 Terminate Action for Condition
If you completed section 5.1, then you may have a false branch that does nothing. It may be helpful to add an error message for backtracking. 

Add a **terminate** action. 

#### Section 5.3 Handling Holidays 
You will need a data source. This could be a Sharepoint List or Excel file. Let's take a SharePoint List as an example. Ensure there is a date column.

Add **Get Items** action

### Section 6 Concurrency Runs

