---
layout: post
title: Connecting to Web Pages and APIs
categories: powerquery
description: This guide will explain how to use web pages and APIs as a source.
---
Our target data not always be in something as nicely organized as a SQL database or Excel file. Pulling data from a web page requires authentication that will be explained in this guide.

### Source 1 Functions

Section 1.1 Web.Contents()

```
Web.Contents(url as text, optional options as nullable record)
```

This function is used for APIs and structured website requests. This function returns the contents in the URL as binary.

*Web.Contents()* works with HTTP requests. Thus, it is great for REST APIs or web services.

Section 1.2 Web.Page()

```
Web.Page(html as any)
```

This function is great for scraping HTML elements. It processes a complete HTML documents into table structures.

Section 1.3 Json.Document()

```
Json.Document(jsonText as any, optional encoding as nullable number)
```

When you use REST APIs for retrieve data, your output will be in the form of JSON. Thus, the *json.document()* returns the content of the specified JSON text as a record.

## Section 2 API requests



&nbsp;

&nbsp;