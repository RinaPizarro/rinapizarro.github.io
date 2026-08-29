---
layout: default
title: JSON Objects
categories: powerautomate
description: Action outputs in Power Automate will often times returns a JSON
  object. This guide will teach you the parts of a JSON object and how to
  retrieve certain properties of a JSON object.
---
Let's say you are creating a scheduled flow in Power Automate that retrieves the Outlook emails from the previous business day. Whether you do this by using an HTTP request or using the built in Outlook action in Power Automate, your output will be all the emails from the previous business day returned as a JSON object. Let's dive in deeper and understand JSON objects and how to use them.

### Section 1 JSON object

Section 1.1 Introduction

**JSON** stands for **Javascript Object Notation**. Whereas tables contain rows and columns, JSON objects contain keys and values. Together, they are known as *key value pair*.

```
{
  "Field1":"aValue1",
  "Field2":"aValue2",
  "Field3":"aValue3"
}
```

Values can be strings, integers, arrays, or booleans. So if you want to extract the value of a certain key, you can use the following syntax:

```
variables('ObjectName')?['KeyName']
```

- *variables('ObjectName')* gets the value stored in the object *ObjectName*
- *?* acts as a safe navigator. If the value is *null* or the property doesn't exist, it will not break
- *['KeyName']* retrieves the value of the specified key

Section 1.2 Accessing Fields

```
outputs('Action_name')
```

If we run the expression above, we will get the *entire* output of a JSON object, including headers, metadata, and payload. However, we may not want all that extra information. We only care about the body of the JSON object. Thus, we would run the following expression below:

```
outputs('Action_name')?['body']
```

```
body('Action_name')
```

These two examples are exactly the same. Just choose however you want to write it.

Now that we have the list of objects, we may want to access a specific property. To do so, we can write an expression like this:

```
outputs('Action_name')?['body']?['receivedDateTime']
```

We are essentially telling JSON to keep searching until we hit the property named *receivedDateTime* and return the value of the property. Depending on your action output, your target property make be deeply nested.

```
outputs('Get_user_profile')?['body']?['user']?['firstName']
```

