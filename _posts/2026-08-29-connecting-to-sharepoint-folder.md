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

- The *url* must the root URL of the SharePoint website, not the direct URL to the target folder. Therefore, if our direct URL to the target folder is something like *[https://sharepoint.com/companyname/documents/weeklyreports/](https://sharepoint.com/companyname/documents/weeklyreports/)* then our root URL would be *[https://sharepoint.com/companyname](https://sharepoint.com/companyname)*
- At the time of writing this article, *options* is used to specify the SharePoint API version to use for the site. By default, this is API Version 14. However, you may specify API Version 15.

Thus, we get the first step in our query:

```
let
     Source = SharePoint.Files("https://sharepoint.com/analyststudios.com", [ApiVersion = 15]
in
     Source
```

When we run this query, we get a table of all the files within the SharePoint site. Now we go on to the second step which is filtering down to our specific folder. To do so, we will filter down the File Path Column with the function *Table.SelectRows().*

```
Table.SelectRows(table as table, condition as function)
```

- The *table* will the the name of our previous step which was *Source*.
- *condition* will contain the properties we need. For our condition, we want to see if the file path contains our specific folder. For that, we will use the function *Text.Contains()*. 

```
Text.Contains(
    text as nullable text,
    substring as text,
    optional comparer as nullable function
)
```

- *text* will be the column in our example
- substring will be the file path of the folder

We will then wrap the *Text.Contains()* function with the *Table.SelectRows()* to produce the following code:

```
let
     Source = SharePoint.Files("https://sharepoint.com/analyststudios.com", [ApiVersion = 15]
     FilteredRows =  Table.SelectRows(
        Source,
        each Text.Contains(
            [Folder Path],
            "/Shared Documents/Reports/"
        )
    )
in
     FilteredRows

```



&nbsp;