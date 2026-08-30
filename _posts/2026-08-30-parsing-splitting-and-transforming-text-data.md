---
layout: post
title: Parsing, Splitting, and Transforming Text Data
categories: powerquery
---
If we have a column that contains html text of an email body, we need to know how to parse it down to a specific line or text. In the real-world, data can be messy. Therefore, we need to know how to clean it up.

### Section 1 Text Library

The Text library in Power Query is a collection of functions for transformating text data. More often than not, the first argument will be the text you want to work with.

- *Text.Trim()* removes leading and trailing whitespaces at the beginning and end of a string.
- *Text.Clean()* removes non-printable characters

