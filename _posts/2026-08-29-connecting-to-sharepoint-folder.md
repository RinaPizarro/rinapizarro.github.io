---
layout: post
title: Connecting to SharePoint Folder
categories: powerquery
description: This guide will explain connecting to SharePoint Folder in the
  Advanced Editor of Power Query.
---
Suppose a colleague on our team uploads the weekly sales transaction summary to a SharePoint folder every Monday. Rather than manually updating our query each week to point to the latest Excel file, we can connect the query to the entire folder, filter for the most recent file, and load its contents automatically.

This guide will explain how we can do this in the Advanced Editor. 

### Section 1 Connecting to SharePoint Folder

Let's begin by figuring out what function we need to use for our first step. First and foremost, we need to connect to SharePoint Site. To do so, we can use the following function:

```
SharePoint.Files(url as text, optional options as nullable record)
```

- The *url* must the root URL of the SharePoint website, not the direct URL to the target folder. Therefore, if our direct URL to the target folder is something like *https://sharepoint.com/companyname/documents/weeklyreports/* then our root URL would be 

