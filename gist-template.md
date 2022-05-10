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

#### Using RegEx

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
[See It](https://jsfiddle.net/benw_10/d7k8ny5p/)<br><br>
### Groups

#### What are they?

Groups are a way for you to seperate parts of a Regular Expression and evaluate them independently from the main expression. This means we can look for substrings within our original subtring. An example of such an expression is - ```/(pre)fix/``` - executed on the string . This expression will match the "pre" in "prefix" in addition to the entire word "prefix". RegEx looks for the substring "pre" as well as the entire substring "prefix". With the same logic, ```/(pre)(fix)/``` matches with "prefix", "pre", and "fix", and ```/pre(fix)/``` matches with "prefix" and "fix".

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
[See It](https://jsfiddle.net/benw_10/mpcsqfny/)<br>
#### Conclusion

The most important aspect of groups is the ability to extract specific information from a regular expression match.<br>
If you understand the other parts of RegEx continue to the [full examples](#full-examples), otherwise continue to [Ranges and Character Classes](#ranges-and-character-classes)

### Ranges and Character Classes

#### Ranges

Ranges are groups (not Regex groups!) of characters that can be matched. We create ranges by surrounding our range within brackets like this - ```[abc]```. The most direct equivalence would be to a long chain "or" operators discussed in the [groups](#groups) section. A demonstration of this equivalence would be to look at this example - 
```
let or_exp = /a|b|c|d|e|f|g/
let range_exp = /[abcdefg]/

let text = "first"
console.log(text.match(or_exp), text.match(range_exp))
// ["f"], ["f"]

text = "second"
console.log(text.match(or_exp), text.match(range_exp))
// ["e"], ["e"]

text = "last"
console.log(text.match(or_exp), text.match(range_exp))
// ["a"], ["a"]
```
[See It](https://jsfiddle.net/benw_10/c14ubvh7/)<br><br>
Both the "or" expression and the range function identically in this case. The difference between an "or" expression and a range is that a range can only contain single characters and not groups like the "or" expression. Within a range there are a few special rules as well.<br>

<strong>First</strong>, periods, ```.```, are treated as a literal ```.```<br>
<strong>Second</strong>, the hyphen character, ```-```, is treated only as a literal hyphen when being the first or last character in the range. Otherwise, it is used to denote an ascending group of characters.<br>
<strong>Third</strong>, the rules of [character escapes](#character-escapes) applies (using ```\``` to escape or write a whitespace character), so if you want a backslash, ```\```, you would need to use a double backslash, ```\\```.<br>
<strong>Last</strong>, since we can't use groups in ranges, parenthesis, ```()```, are treated as a literal ```(``` or ```)```<br>

To explain the second rule, ranges have a "shorthand" for generating ranges. To do this, we use ```[x-y]``` with ```x``` and ```y``` being the start and end of the range respectively. A direct example would be to shorten the range ```[abcdef]``` to ```[a-f]``` using this syntax. We can also do numbers as well like in the expression ```[0-5]``` which is equivalent to ```[012345]```. If we wanted to do a range for a multiple digit number, we could do something like, ```[1-4][0-3]```, which matches numbers like 10, 11, 12, 13 and 40, 41, 42, 43. Once we explore [quantifiers](#quantifiers), we will see a more useful way to do this but for now it works.
<br><br>
We can also use the carat character, ```^```, to denote an exclusive range. An exclusive range is a group of characters that includes every character EXCEPT the ones included in the range. An example of this would be ```[^abcd]``` which would match every character except the letters a, b, c, and d. ```^``` has this specific effect ONLY within ranges and has a different meaning outside of ranges.

#### Character classes

Character classes are essentially constant variables that can be referenced as a substitute for a range of characters. The most useful character class in my opinion is the period - ```.``` It denotes a range that matches with every character except line terminators like ```\n``` and ```\r```. Another really useful character class is the - ```\w``` - character class as it denotes an expression equivalent to - ```[A-Za-z0-9_]```.<br>
You can see the full list of character classes [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions/Character_Classes#types).

#### Conclusion

The most important aspect of ranges and character classes is that you save time writing long expressions and looking up specific groups of characters.<br>
If you understand the other parts of RegEx continue to the [full examples](#full-examples), otherwise continue to [Flags](#flags)

### Flags

Regular expressions by default only match the first substring found, and do not retain indexes for the substring matches within the returned value. With flags, we can alter our substring search to our needs, and we can even combine multiple flags. There are plenty of cases where you should or shouldn't use a specific flag so double check!

#### List of flags

```g```:  Finds ALL substrings matching the expression instead of just the first<br>
```i```:  Makes search case-insensitive<br>
```m```:  Searches a multi-line string line by line<br>
```s```:  The character class ```.``` now also matches newline characters<br>
```d```:  Returns the indeces for the matches in addition to the matches<br>
```y```:  Sticky search. Starts search at the expression's ```lastIndex``` property. [See more](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/sticky)<br>

#### Using flags

We can use flags by using the syntax ```/expression/flag``` for usage with RegEx literals and ```new RegExp(expression_string, flags)```. If we wanted to use the ```g``` flag, we could either do ```let exp = /word/g``` or ```let exp = new RegExp("word", "g")```. For multiple flags we simply extend the string like so - ```/word/gi```. In this case, we are using the global flag and also using the case-insensitive flag. This will return all expression matches while ignoring the difference between lower and uppercase letters.
<br>
Flags are extremely useful. We can now fully demonstrate the capability of ranges, the "or" operator, and character classes. This code demonstrates this capability -
```
let text = "The quick brown fox jumps over the lazy dog. L33t 5p34k"

// find all numbers 0-9
let exp = /[0-9]/g
let matches = text.match(exp)
console.log(matches)
// ["3", "3", "5", "3", "4"]

// find letters a-d + the letter s, without worrying about case
exp = /[a-dl]/gi
matches = text.match(exp)
console.log(matches)
// ["c", "b", "l", "a", "d", "L"]

// find all matching words
exp = /quick|fox|dog/g
matches = text.match(exp)
console.log(matches)
// ["quick", "fox", "dog"]
```
Multiline flag -
```
// search a multiline string using ^ and $
text = `The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy dog and more`

// without $ or ^ the multiline flag behaves almost identical to default 
let with_ = text.match(/g|l/mg)

// only matches "g" if it is at the end of a line
// use a group like we would use parenthesis in math, to seperate operations
// without group it would be look for any "g" OR an "l" at the end of a line
let without_ = text.match(/(g|l)$/mg)
console.log(with_, without_)
// ["l", "g", "l", "g"], ["g"]
```
Indices flag -
```
// indices flag
text = "The quick brown fox jumps over the lazy dog."
// hard to combine indices with global flag
exp = /jumps|lazy/d
// when using indices flag use exec instead of match
matches = exp.exec(text)
// extract indices
let indices = matches.indices[0]
// gets the indices for each occurence but matches with only the first
console.log(matches, indices)
// ["jumps"], [20, 25]
```
[See It](https://jsfiddle.net/benw_10/okr6sm5f/)<br><br>

### Assertions

### Quantifiers

### Character Escapes

### Full examples

#### Verify an email
```
// will match a full email address, its address, and its domain in that order
// null if email not valid
// ^ : matches with start of input
// ([a-z0-9_\.-]+) : 
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
[See It](https://jsfiddle.net/benw_10/Lof2ay0w/)<br><br>

## Author

Ben Wirth<br>
[GitHub Repo](https://github.com/benw10-1/bugTracker)<br>
[Website](https://ben-devs.com)
