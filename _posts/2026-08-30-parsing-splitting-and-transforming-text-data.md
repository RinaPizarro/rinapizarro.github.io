---
layout: post
title: Parsing, Splitting, and Transforming Text Data
categories: powerquery
---
If we have a column that contains html text of an email body, we need to know how to parse it down to a specific line or text. In the real-world, data can be messy. Therefore, we need to know how to clean it up.

### Section 1 Text Library

The Text library in Power Query is a collection of functions for transformating text data. More often than not, the first argument will be the text you want to work with.

Section 1.1 Cleaning up Text

- *Text.Trim()* removes leading and trailing whitespaces at the beginning and end of a string.
- *Text.Clean()* removes non-printable characters or invisible characters.
- *Text.Proper()* capitalizes the first letter of each word in a string, and it lowercases everything else.

```
TransformedNames = Table.TransformColumns(
    PreviousStep,
    {{"CustomerName", each Text.Proper(Text.Trim(Text.Clean(_))), type text}}
)
```

Section 1.2 Parsing and Extracting Substrings

- *Text.Start(text, count)* returns the first count characters from a string
- *Text.End(text, count)* returns the last count characters.
- *Text.Middle(text, offset, count)* starts at the offset position and returns the count characters. Omitting *Count* returns everything from offset to the end of the string. 

Section 1.3 Splitting Text

- *Text.Split(text, seperator)* divides a string at every seperator and returns a list of every string identified.
- *Splitter.SplitTextByLengths()* 

Section 1.4 Searching within Strings

- *Text.Contains()*
- *Text.StartsWith()*
- *Text.EndsWith()*

