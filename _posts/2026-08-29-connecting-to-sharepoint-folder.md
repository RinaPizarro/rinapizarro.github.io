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

*Reports* will be the folder that contains our excel files. 

Now that we have our specific folder, we really just need the latest file in that folder. To do so, we are going to use the *Table.Sort()* function

```
Table.Sort(table as table, comparisonCriteria as any)
```

- As usual, the *table* will be the previous step in our query.
- *comparisonCriteria* will be a list thats contains our column name as text, and either *Order.descending* or *Order.ascending.*

```
let
     Source = SharePoint.Files("https://sharepoint.com/analyststudios.com", [ApiVersion = 15]),
     FilteredRows =  Table.SelectRows(
        Source,
        each Text.Contains(
            [Folder Path],
            "/Shared Documents/Reports/"
        )
    ),
      SortedFiles = Table.Sort(
        FilteredFiles,
        {{"Date modified", Order.Descending}}
    )
in
     SortedFiles
```

Now that we have our excel files within our folder sorted by descending date, we only care about the first file. This, we will grab the first file in the example below:

```
let
     Source = SharePoint.Files("https://sharepoint.com/analyststudios.com", [ApiVersion = 15]),
     FilteredRows =  Table.SelectRows(
        Source,
        each Text.Contains(
            [Folder Path],
            "/Shared Documents/Reports/"
        )
    ),
      SortedFiles = Table.Sort(
        FilteredFiles,
        {{"Date modified", Order.Descending}}
    ),
     TopFile = SortedFiles{0}[Content]
in
     TopFile
```

Now we have only the latest file! The only thing that left is reading the file so that we can get all the information in the file.

Before we do this, we need to know if our data is formatted as a *sheet* or as a *table.* If our data is formatted as a *table* then Power Query will have an easier time determining the headers. However, if our data is in a *sheet* then we need to male sure Power Query promotes those headers. Otherwise, our header names will remain as row one rather than column headers.

Alright, let's start grabbing out sheet or table. To do this, we will need the function *Excel.Workbook().*

```
Excel.Workbook(
    workbook as binary,
    optional useHeaders as any,
    optional delayTypes as nullable logical
)
```

- *Workbook* will be the name of our previous step.
- *useHeaders* can be *True* if we want to use the headers or *False* if we don't want to use the headers. By default, this is *False*.
- *delayTypes* can be True if we want Power Query to hold on on assigning data types to each column, or *False* if we want Power Query to go ahead and determine the data types of each column. By default, this is *False.*

Now we need to index in our Workbook. To do so, we use the following Syntax:

```
expression{selector}
```

This tells Power Query to take the expression and access a specific item in the expression.

If we are working with a sheet, our Item will be the sheet name and our kind will be sheet. If we are working with a table, our item will be the table name and our kind will be table. Putting all this together, we get our finalized query:

```
let
     Source = SharePoint.Files("https://sharepoint.com/analyststudios.com", [ApiVersion = 15]),
     FilteredRows =  Table.SelectRows(
        Source,
        each Text.Contains(
            [Folder Path],
            "/Shared Documents/Reports/"
        )
    ),
      SortedFiles = Table.Sort(
        FilteredFiles,
        {{"Date modified", Order.Descending}}
    ),
     TopFile = SortedFiles{0}[Content],
     Workbook = Excel.Workbook(
        TopFile,
        null,
        true
    ),

    ExcelTable = Workbook{
        [Item = "SalesTable", Kind = "Table"]
    }[Data]


in
     ExcelTable
```

