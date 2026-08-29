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

Values can be strings, integers, arrays, or booleans.