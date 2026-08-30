---
layout: post
title: Custom M Functions
categories: powerquery
---
Sometimes the built-in functions by Power Query may not achieve your desires results. For example, the may be some buisness logic that you are trying to implement but the built-in functions do not work. Creating custom functions allows us to use the same logic multiple times without having to rewrite the same code over and over. 

### Section 1 Structure

```
(parameters) =>
let
     result = [transformation]
in
     result
```

- your function can have more than one input. For example, you can use (x, y) as your parameters. 

Therefore, if you use

```
(name, age) =>
let
    result = name & " is " & Text.From(age) & " years old"
in
    result
```

then you can call it by using

```
myFunction("Jessica", 25)
```

