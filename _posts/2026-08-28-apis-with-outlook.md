---
layout: post
title: APIs with Outlook
categories: graphapi
description: This guide will go over various APIs with Outlook.
---
Microsoft Graph allows you to use APIs to retrieve information from sources such as Outlook (which will be this guide's topic). 

### Section 1 Protocol

When you open Graph Explorer, the system will automatically pre-populate this URL:

```
https://graph.microsoft.com/v1.0/me
```

- *https* tells our computer to communicate with the server using HTTP and encryption (TSL)
- *[graph.microsoft.com](http://graph.microsoft.com)* is the host/domain the server is communicating with. This is considered the address of the API, which can be used for various things such as 
  - Outlooks
  - Users
  - Teams
  - Calendar
  - SharePoint
- */v1.0* is the API version. At the time of writing this guide, there is *v1.0* and *beta*. For general practice, *v1.0* should be used for production while *beta* should be used for testing or if something is only speciic in *beta*.
- */me* is the endpoint. 
  - */me* is the currently authenticated user 
  - */users* is all users in your Microsoft 365 organization/ tenant

If we run the URL above, we get something similar like this:

![](/assets/images/graph_api_basic_url_example_1.png){:height="300px"}

Our output ends up being. JSon object that has various keys with values. 