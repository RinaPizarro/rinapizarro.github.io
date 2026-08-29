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



![](/assets/images/graph_api_basic_url_example_1.png)

{:height="300px"}

### Section 2 Retrieving Emails

Section 2.1 mailFolders

Our output ends up being a JSON object that has various keys with values. 

```
https://graph.microsoft.com/v1.0/me/mailFolders
```

![](/assets/images/graph_api_mailfolders.png){:height="300px"}

Here is an example of a URL that gets our folders or *mailFolders*. Emails, or *messages*, are organized in our *mailFolders*. As we can see in our screenshot, we have a mailFolder called *Arhcivo* and another one called *Bandeja de Entrada*. 

- *id* is the identifier for the folder object. 
- *displayName* is the name of the folder as it appears in Outlook
- *parentFolderId* is the ID of the folder in which the current folder object resides in
- *childFolderCount* lets us know the number of subfolders in the current folder object

Section 2.2 Messages

Let's say we want to grab the emails from our Inbox.

```
https://graph.microsoft.com/v1.0/me/mailFolders/AAMkADlmZTFiNzc1LThjZTEtNDgyYi04MTAxLWJkMzY4OGRmZTI3MAAuAAAAAAB8dGH_gOEhS58qBHWH-2K3AQCMJW4mPim-Q7mgBNUhcMAjAAAAAAEtAAA=
```

After */mailFolders*, we want to use the *id* of the folder in our URL. However, this URL alone will just give us the folder properties. To access the emails in the folder, we add */messages* to the end of our URL. 

```
https://graph.microsoft.com/v1.0/me/mailFolders/AAMkADlmZTFiNzc1LThjZTEtNDgyYi04MTAxLWJkMzY4OGRmZTI3MAAuAAAAAAB8dGH_gOEhS58qBHWH-2K3AQCMJW4mPim-Q7mgBNUhcMAjAAAAAAEtAAA=/messages
```

