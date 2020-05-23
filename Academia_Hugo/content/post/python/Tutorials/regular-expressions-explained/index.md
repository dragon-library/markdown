---
title:   Regular Expressions Explained
subtitle: A gentle introduction to Regular Expressions. Learn about main concepts, common patterns, and functions with examples.  
summary: A gentle introduction to Regular Expressions. Learn about main concepts, common patterns, and functions with examples.
authors:
    - admin
tags: ["Regular Expressions"]
categories: ['Tutorials','Python']
date: "2019-07-07T00:00:00Z"
lastMod: "2019-07-07T00:00:00Z"
featured: true
draft: false
image:
  caption: ""
  focal_point: "Smart"
  preview_only: true
---

![](featured.jpeg)


[Source](https://www.thedataschool.co.uk/natalia-miteva/regex-what-why-and-how/)

I bet you all have encountered regular expressions at some points. They are very powerful tools that are universally supported in many platforms, including programming languages like Python, R, Java, SQL, Scala.

As a data scientist/developer, having a solid understanding of Regex can help you perform various data munging and text mining tasks very easily. Personally, I use them for lots of random stuffs, mostly when I have to work with text data or do Natural Language Processing projects.


![](https://miro.medium.com/max/687/1*ZXTb1lt1LYysa1yki__0Aw.gif)

Regular expressions can seem intimidating at first, but they are very rewarding once you grasp the basics and apply them to your work properly.

# What is Regular Expression (RegEx)?

A regular expression or regex is a text string that defines a  _search pattern._
```py
"\w+" # this is a regex
```
Typically, these patterns are used for four main tasks:

-   **Find**  text within a larger body of text
-   **Validate**  that a string conforms to a desired format
-   **Replace** or  **insert** text
-   **Split**  strings

Let’s take a quick look at some common regex patterns before we apply them to our codes.

# Common Patterns

Earlier, we have this regex example:
```py
\w+
```
“w” here means  _word_. “+” means  _one or more._ The backlash character “\” is the escape character for regular expressions.  This regex matches word characters, including ASCII letter, digit, or underscore. Now, suppose we want to match the first word we can find in a string. First, we import the  `re` module.
```py
import re
```
Then we define a pattern, and use the function  `re.match()`  to match the first word it finds:

```py
# define a regex pattern  
word_regex = '\w+'re.match(word_regex, 'hello world!') _# this matches the first word it finds  
_>>><re.Match object; span=(0, 2), match='hi'>
```

Some common patterns:

-   **w**  matches word characters
-   **d**  matches digits, while  **D**  matches non-digit characters
-   **s**  matches whitespace characters, while  **S**  matches non-whitespace characters
-   **.**  (dot) matches any letter or symbol (wildcard)
-   **[a-z]**  matches lowercase group. The bracket [] matches characters in it
-   Use  **()**  to define a group
-   Use  **[]**  to define explicit character ranges

Now as you already have some regex patterns in hand, let’s move on to some important functions.

## The match() function

This function matches  _pattern_  to  _string_. It returns a  **match**  object on success,  **_None_**  on failure.
The match function is defined as:
```py
re.match('\w+', 'hello world!')  
>>><re.Match object; span=(0, 5), match='hello'>
The match function is defined as:
```

## The findall() function

This function returns a list of all instances of the pattern in the string. Matches are returned in the order left-to-right of the original string.
```py
re.findall('[A-Z]\w+', 'hello World!')  
>>>['World']
```

**The search() function**

The  **search()**  function scans through string, looking for instances of the pattern in the string. It returns a  **match**  object on success,  **_None_**  on failure. This function is like the match() function, but it goes through the whole string. See  [search() vs match()](https://docs.python.org/3/library/re.html#search-vs-match)  for more details.
```py
re.search('ef', 'abcdef')  
>>><re.Match object; span=(4, 6), match='ef'>
```

**The split() function**

This function splits  _string_  by the occurrences of  _pattern._
```py
re.split('\s+', 'hello world this is andre')  
>>>['hello', 'world', 'this', 'is', 'andre']
```

# Random Thoughts

![](https://miro.medium.com/max/60/1*rD8bpKAGWGct2ThM2jKOaw.png?q=20)

![](https://miro.medium.com/max/921/1*rD8bpKAGWGct2ThM2jKOaw.png)

Who else loves Regex?

I love regular expressions. However, it is important to remember that while regex are very powerful tools, it is extraordinarily easy to overuse them. A few things to note:

-   Start small. Use them responsibly. Break it down into smaller regexes if needed. You would not want to end up with one huge multiple-line regex. It decreases visibility of your codes and is just not worth it.
-   Comment your regex! No one wants to waste time staring at your 20-line monster regex trying to figure out what it means.

----------

# Conclusion

In this article, you have learned the main concept of regex, common patterns, and how to apply regex using  **re**  functions. Regex is a small computer language of their own, and it requires practice too. Here are my favorite resources to get you started:

-   [https://www.rexegg.com/regex-quickstart.html](https://www.rexegg.com/regex-quickstart.html): your go-to regex cheatsheet
-   [https://www.regular-expressions.info](https://www.regular-expressions.info/): another comprehensive regex tutorial site
-   [https://regexr.com](https://regexr.com/): an online tool to learn, build, and test your regex
-   [https://pythex.org](https://pythex.org/): a Python regular expression editor. A quick way to test regular expressions as you write them
-   [https://docs.python.org/3/library/re.html](https://docs.python.org/3/library/re.html): official Python docs on regex

----------

This is my first post on Towards Data Science. Leave comments if you have any suggestions for how to improve this post. Follow me up at  [Medium](https://medium.com/@andreduong07)  or connect with me on  [LinkedIn](https://www.linkedin.com/in/andreduong/)  for more quality content!

> Reference : [towardsdatascience.com](https://towardsdatascience.com/regular-expressions-explained-c9bce508e672)