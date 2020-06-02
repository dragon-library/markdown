---
title:   Regular Expressions
subtitle: Regular expressions are essentially a highly specialized programming language embedded inside Python that empowers you to specify the rules for the set of possible strings that you want to match.  
summary: Regular expressions are essentially a highly specialized programming language embedded inside Python that empowers you to specify the rules for the set of possible strings that you want to match.  
authors:
    - admin
tags: ['Regular Expressions']
categories: ['Tutorials','Python']
date: "2020-04-15T00:00:00Z"
lastMod: "2020-04-15T00:00:00Z"
featured: true
draft: false
image: 
  caption: "Photo by http://www.w3programmers.com"
  focal_point: "Smart"
  preview_only: true
---

![](featured.jpg)

Regular expressions are essentially a highly specialized programming language embedded inside Python that empowers you to specify the rules for the set of possible strings that you want to match.

In Python you need the  **re**  module for regular expressions usage. The grammar overview is on the bottom of this page.

**Related course:**  
[Python Programming Bootcamp: Go from zero to hero](https://gum.co/dcsp)  

## The Match function

  
The match function is defined as:
```py
re.match(pattern, string)  
```

The parameters are:.  

| Parameters | Description|
|-------|------------|
| pattern | a regular expression |
| string |the input string  |

If you want to match a string to a numberic sequence of exactly five, you can use this code:

```py
#!/usr/bin/python  
import re  
  
input = raw_input("Enter an input string:")  
m = re.match('\d{5}\Z',input)  
  
if m:  
 print("True")  
else:  
 print("False")  
```
Example outputs:

## Email validation regex

  
We can use the same function to validate  _email address_. The grammar rules are seen in re.compile and in the grammar table.
```text
String	Match
12345	True
12358	True
55555	True
123	False
123K5	False
5555555	False
```
```py
#!/usr/bin/python  
import re  
  
input = raw_input("Enter an input string:")  
m = re.match('[^@]+@[^@]+\.[^@]+',input)  
  
if m:  
 print("True")  
else:  
 print("False")  
```
## The Search Function

  
The search function is defined as:
```py
re.search(pattern, string)  
```
The parameters are:  
Parameter	Description.  
pattern	a regular expression, defines the string to be searched
string	the search space

To search if an e-mail address is in a string:
```py
#!/usr/bin/python  
import re  
  
input = "Contact me by test@example.com or at the office."  
  
m = re.search('[^@]+@[^@]+\.[^@]+',input)  
  
if m:  
 print("String found.")  
else:  
 print("Nothing found.")  
```

## Regular Expression Examples

  
A few examples of regular expressions:  

## Regular Expression Grammar

|Example|Regex|
|:--------|--------------|
|IP address|	(([2][5][0-5]\.)|([2][0-4][0-9]\.)|([0-1]?[0-9]?[0-9]\.)){3}(([2][5][0-5])|([2][0-4][0-9])|([0-1]?[0-9]?[0-9]))|
|Email|	[^@]+@[^@]+\.[^@]+|  
|Date |MM/DD/YY	(\d+/\d+/\d+)|  
|Integer (positive)|	(?<![-.])\b[0-9]+\b(?!\.[0-9])|  
|Integer|	[+-]?(?<!\.)\b[0-9]+\b(?!\.[0-9])|  
|Float|	(?<=>)\d+.\d+|\d+|  
|Hexadecimal	|\s–([0-9a-fA-F]+)(?:–)?\s|  


Overview of the regex grammar:

|Regex	|Description|
|:-----------|---------------------------------|  
|\d|	Matches any decimal digit; this is equivalent to the class [0-9]|
|\D	|Matches any non-digit character; this is equivalent to the class [^0-9]. |
|\s|	Matches any whitespace character; this is equivalent to the class [ \t\n\r\f\v].|
|\S|	Matches any non-whitespace character; this is equivalent to the class [^ \t\n\r\f\v].|
|\w|	Matches any alphanumeric character; this is equivalent to the class [a-zA-Z0-9_].|
|\W|	Matches any non-alphanumeric character; this is equivalent to the class [^a-zA-Z0-9_].|
|\Z	|Matches only at end of string|
|[..]	|Match single character in brackets|
|[^..]|	Match any single character not in brackets|
|`.`	|Match any character except newline|
|$	|Match the end of the string|
|*	|Match 0 or more repetitions|
|+	|1 or more repetitions|
|{m}|Exactly m copies of the previous RE should be matched.|
| `||`	|Match A or B [A|B] |
|?|	0 or 1 repetitions of the preceding RE|
|[a-z]|	Any lowercase character|
|[A-Z]	|Any uppercase character|
|[a-zA-Z]	|Any character|
|[0-9]	|Any digit|

> Reference : [pythonspot.com](https://pythonspot.com/regular-expressions/)