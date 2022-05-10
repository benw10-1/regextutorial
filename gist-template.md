# Regex Is Pretty Cool Honestly

On this page, we will be reviewing the <strong>Regular Expressions</strong> (<strong>RegEx</strong>) and their usages. We will go over examples of <strong>RegEx</strong> and their applications as well as specific parts of the <strong>RegEx syntax</strong>.

## Summary

The specific components of <strong>RegEx</strong> we are going to be going through are groups, ranges, assertions, quantifiers, character classes, flags, and character escapes. Learning all of these aspects of <strong>RegEx</strong> will allow anyone to build extremely useful <strong>RegEx</strong> statements. I will also explain how multiple components can be compounded to form a more useful expression.

## Table of Contents
- [Introduction](#introduction)
- [Groups](#groups)
- [Ranges and Character Classes](#ranges-and-character-classes)
- [Assertions](#assertions)
- [Quantifiers](#quantifiers)
- [Flags](#flags)
- [Character Escapes](#character-escapes)
- [Full Examples](#full-examples)

## Regex Components

### Introduction

RegEx is a tool used in many popular languages such as Python and JavaScript used for formatting strings, replacing text, and finding substrings. In the tutorial, I will be using JavaScript to demonstrate functional code.

#### Creating a new Regular Expression

We can create a new RegEx by either using the built-in RegEx tokens - ```var exp = /Regular Expression/``` <br>
or create a new RegExp object - ```var exp = new RegExp("Regular Expression")```<br>

#### Using a Regular Expression

We can execute a Regular expression in a variety of ways. One way to do it is - <br>
```
var exp = /I'm/;
exp.exec("Hi, I'm some text");
// Returns: ["I'm"]
```
Another more standard way is -
```
var exp = /I'm/;
var text = "Hi, I'm some text"
text.match(exp)
// Returns: ["I'm"]
```
Without using [groups](#groups), [ranges](#ranges), or [flags](#flags), RegEx will simply look for the specified substring and return the first one it finds that matches the expression.<br>
If it can't find the substring it will return null instead like here -
```
var exp = /I'm/;
var text = "Hi, some text"
text.match(exp)
// Returns: null
```

### Groups

#### What are they?

Groups are a way for you to seperate parts of a Regular Expression and evaluate them independently from the main expression. This means we can look for substrings within our original subtring. An example of such an expression is - ```/(pre)fix/``` - executed on the string . This expression will match the "pre" in "prefix" as well as the entire word "prefix" as well. RegEx looks for the substring "pre" as well as the entire substring "prefix". With the same logic, ```/(pre)(fix)/``` matches with "prefix", "pre", and "fix", and ```/pre(fix)/``` matches with "prefix" and "fix".

#### Using groups

We will go into groups further as we use them more in the tutorial as we need to learn a few more things about RegEx before they become useful, but for now we can add a ton of usability to an expression by using the "or" operator. The or operator is denoted by a - ```|``` - and its usage syntax is - ```x|y```. It matches a substring if the substring matches expression x OR expression y. This can be chained with multiple or operators for maximum effect. A very simple but effective implementation of the "or" operator is when we are looking for words in a sentance. The code for this would be -
```
var text = "Hi, my name is Ben and I like to eat"
var exp = /name|like/
text.match(exp)
// Returns: ["name"]

var second_text = "Hi, my nombre is Ben and I like to eat"
second_text.match(exp)
// Returns: ["like"]
```

The main importance of groups is you are able to extract specific information from a regular expression match.<br>
If you understand the other aspects of RegEx continue to the [full examples](#full-examples), otherwise continue to [Ranges and Character Classes](#ranges-and-character-classes)

### Ranges and Character Classes

#### Ranges

Ranges are groups of characters that can be matched. The most direct equivalence would be to a long string of the "or" operator discussed in the [groups](#groups) section. An example of this equivalence would be to look at this example - 
```
let or_exp = /a|b|c|d|e|f|g/
let range_exp = /[abcdefg]/

let text = "first"
console.log(text.match(or_exp), text.match(range_exp))
// ["f"], ["f"]

text = "second"
console.log(text.match(or_exp), text.match(range_exp))
// ["e"], ["e"]

text = "first"
console.log(text.match(or_exp), text.match(range_exp))
// ["f"], ["f"]
```
Both the "or" expression and the range function identically in this case. The difference between an "or" expression and a range is that a range can only contain single characters and not groups like the "or" expression. Within a range there are a few special rules as well.<br>
<strong>First</strong>, periods, ```.```, are treated as a literal ```.```<br>
<strong>Second</strong>, the hyphen character, ```-```, is treated only as a literal hyphen when being the first or last character in the range. Otherwise, it is used to denote an ascending group of characters.<br>
<strong>Third</strong>, the rules of [character escapes](#character-escapes) applies (using ```\``` to escape or write a whitespace character), so if you want a backslash, ```\```, you would need to do a double backslash, ```\\```.
<strong>Last</strong>, since we can't use groups in ranges, parenthesis, ```()```, are treated as a literal ```(``` or ```)```

### Flags

### Assertions

### Quantifiers

### Character Escapes

### Full examples

Verify an email - 
```
// will match a full email address, its address, and its domain in that order
// null if email not valid
let exp = /^([a-z0-9_\.-]+)@([\da-z\.-]+\.[a-z\.]{2,6})$/

let shawn = "shawnce22@msn.com"
console.log(shawn.match(exp))
// ["shawnce22@msn.com", "shawnce22", "msn.com"]

let jack = "1999jacks@yahoo.com"
console.log(jack.match(exp))
// ["1999jacks@yahoo.com", "1999jacks", "yahoo.com"]

let invalid = "invalid##@email.com"
console.log(invalid.match(exp))
// null
```

## Author

Ben Wirth<br>
[GitHub Repo](https://github.com/benw10-1/bugTracker)<br>
[Website](https://ben-devs.com)
