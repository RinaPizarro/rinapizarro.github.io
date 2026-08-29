---
layout: post
title: Connecting to SQL server
categories: powerquery
description: This guide will explain the proper steps to connecting to your SQL
  database in Power Query.
---
Let’s say we’re building a Power BI report based on sales transactions from our e-commerce website. Whenever a customer purchases an item, the transaction details are automatically stored in our database.

Our goal is to take that data directly from the database and load it into Power BI for daily reporting—without having to manually download, update, or upload Excel files or other documents.

This is where connecting Power BI directly to a SQL database becomes especially useful. Instead of relying on someone to maintain files in a SharePoint folder, Power BI can connect directly to the database and retrieve the latest transaction data whenever the report is refreshed. The entire process becomes more automated, reliable, and easier to maintain

### Section 1  Understand database connection

When it comes to connecting Power Query to data, the choice between a file stored in SharePoint and a SQL Server database often comes down to runtime and efficiency.

With a file stored in SharePoint, Power Query has to *locate and read* the contents of the file before it can retrieve the data. With a SQL database, Power Query *establishes a network connection, authenticates the user, and sends a query directly to the database*. As a result, retrieving data from SQL is generally faster and more efficient than retrieving data from files.

There’s also the issue of maintaining the data source. Your organization may store the same data in multiple places—for example, a transactions table in a SQL database alongside Excel files containing the same sales transactions. If your Power Query source is a SharePoint folder, someone may need to manually upload or drop the daily transaction files into that folder. That quickly becomes tedious and exhausting.

A SQL database eliminates much of that manual work. Once the connection and query are set up, the process can be largely automated, allowing you to spend less time managing files and more time working with the data.



### Section 2 Setting up the Source in Advanced Editor

I'm going to use the advanced editor for this. 

```
let
     Source = SQL.Database('serverName', 'databaseName')
     MyQuery = Value.NativeQuery(Source, "Write Your Query Here")
in
    MyQuery
```

