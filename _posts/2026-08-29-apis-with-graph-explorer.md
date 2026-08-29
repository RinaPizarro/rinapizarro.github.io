---
layout: post
title: APIs with Graph Explorer
categories: graphapi
description: This guide will go over how to use APIs in graph explorer
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
https://graph.microsoft.com/v1.0/me/mailFolders/
AAMkADlmZTFiNzc1LThjZTEtNDgyYi04MTAxLWJkMzY4OGRmZTI3MAAuAAAAAAB8dGH_gOEhS58qBHWH-2K3AQCMJW4mPim-Q7mgBNUhcMAjAAAAAAEtAAA=
```

After */mailFolders*, we want to use the *id* of the folder in our URL. However, this URL alone will just give us the folder properties. To access the emails in the folder, we add */messages* to the end of our URL. 

```
https://graph.microsoft.com/v1.0/me/mailFolders/
AAMkADlmZTFiNzc1LThjZTEtNDgyYi04MTAxLWJkMzY4OGRmZTI3MAAuAAAAAAB8dGH_gOEhS58qBHWH-2K3AQCMJW4mPim-Q7mgBNUhcMAjAAAAAAEtAAA=
/messages
```

Section 2.3 Outlook Categories

Now that we got the messages, we may want to look at other properities of our message such as the category. We can use a URL such as

```
https://graph.microsoft.com/v1.0/me/mailFolders/
AAMkADlmZTFiNzc1LThjZTEtNDgyYi04MTAxLWJkMzY4OGRmZTI3MAAuAAAAAAB8dGH_gOEhS58qBHWH-2K3AQCMJW4mPim
Q7mgBNUhcMAjAAAAAAEMAAA=/
messages/
AAMkADlmZTFiNzc1LThjZTEtNDgyYi04MTAxLWJkMzY4OGRmZTI3MABGAAAAAAB8dGH_gOEhS58qBHWH-2K3BwCMJW4mPim-Q7mgBNUhcMAjAAAAAAEMAACMJW4mPim-Q7mgBNUhcMAjAAAAAE3XAAA=/
categories
```

Here is a breakdown of this URL:

- **[https://graph.microsoft.com/v1.0/me/mailFolders](https://graph.microsoft.com/v1.0/me/mailFolders)** is our URL 
- **AMkADlmZTFiNzc1LThjZTEtNDgyYi04MTAxLWJkMzY4OGRmZTI3MAAuAAAAAAB8dGH_gOEhS58qBHWH-2K3AQCMJW4mPim-Q7mgBNUhcMAjAAAAAAEMAAA=** is the id of the inbox folder
- **messages** retrieves the emails in the inbox folder
- **AAMkADlmZTFiNzc1LThjZTEtNDgyYi04MTAxLWJkMzY4OGRmZTI3MABGAAAAAAB8dGH_gOEhS58qBHWH-2K3BwCMJW4mPim-Q7mgBNUhcMAjAAAAAAEMAACMJW4mPim-Q7mgBNUhcMAjAAAAAE3XAAA=** is the id of one of the emails in my inbox
- **categories** gives me an array of categories associated with the email.

Section 2.4 Attachments

```
https://graph.microsoft.com/v1.0/me/mailFolders/AAMkADlmZTFiNzc1LThjZTEtNDgyYi04MTAxLWJkMzY4OGRmZTI3MAAuAAAAAAB8dGH_gOEhS58qBHWH-2K3AQCMJW4mPim-Q7mgBNUhcMAjAAAAAAEMAAA=/messages/AAMkADlmZTFiNzc1LThjZTEtNDgyYi04MTAxLWJkMzY4OGRmZTI3MABGAAAAAAB8dGH_gOEhS58qBHWH-2K3BwCMJW4mPim-Q7mgBNUhcMAjAAAAAAEMAACMJW4mPim-Q7mgBNUhcMAjAAAAAE3XAAA=/attachments
```

The following would be a URL for retrieving attachments. The output will be an array of attachments as a JSON object.

```
HTTP/1.1 200 OK
Content-type: application/json

{
  "value": [
    {
      "@odata.type": "microsoft.graph.fileAttachment",
      "contentType": "contentType-value",
      "contentLocation": "contentLocation-value",
      "contentBytes": "contentBytes-value",
      "contentId": "null",
      "lastModifiedDateTime": "datetime-value",
      "id": "id-value",
      "isInline": false,
      "name": "name-value",
      "size": 99
    }
  ]
}
```

### Section 3 Query Parameters

Section 1.1 Common Parameters

When we are passing a URL into our graph explorer, we may want to give certain parameters


| Name | Description | Example |
| ---------- | --------------------------------------------- | ------------------------------------------ |
| *$count* | returns the total count of matching resources | */me/messages?$top=2&count=true* |
| *$expand* | returns related resources | */groups?$expand=members* |
| *$filter* | filters rows | */users?$filter=startswith(givenName,'J')* |
| *$format* | returns results in a specified format | */uers?$format=json* |
| *$orderby* | orders results | */users?$orderby=displayName desc* |
| *$search* | filters columns | */me/messages?$search=pizza* |
| *$select* | skip items | */users?$select=givenName,surname* |
| *$top* | sets the paze size of results | */users?$top=2* |


- *OrderBy*
  - You may specify the column name to order along with ascending  as *asc* or decending order as *desc*

```
?$orderby=name desc
```

Section 1.2 Syntax

Now that we know what are the most common parameters, we may want to filter by multiple parameters

```
https://graph.microsoft.com/v1.0/me/mailFolders/AAMkADlmZTFiNzc1LThjZTEtNDgyYi04MTAxLWJkMzY4OGRmZTI3MAAuAAAAAAB8dGH_gOEhS58qBHWH-2K3AQCMJW4mPim-Q7mgBNUhcMAjAAAAAAEtAAA=/messages?$top=10
```

At the end of our query that retrieves all messages from our Inbox, I added *$* to specify the scope to search and *$top=10* to specify the parameter.

### Section 4 Permissions

![](/assets/images/graph_api_permissions.png){:height="300px"}