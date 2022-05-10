# Regex Is Pretty Cool Honestly

On this page, we will be reviewing the <strong>Regular Expressions</strong> (<strong>RegEx</strong>) and their usages. We will go over examples of <strong>RegEx</strong> and their applications as well as specific parts of the <strong>RegEx syntax</strong>.

## Summary

The specific components of <strong>RegEx</strong> we are going to be going through are groups, ranges, assertions, quantifiers, character classes, flags, and character escapes. Learning all of these aspects of <strong>RegEx</strong> will allow anyone to build extremely useful <strong>RegEx</strong> statements. I will also explain how multiple components can be compounded to form a more useful expression.

## Table of Contents
- [Introduction](#introduction)
- [Groups](#groups)
- [Ranges and Character Classes](#ranges-and-character-classes)
- [Quantifiers](#quantifiers)
- [Assertions](#assertions)
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

Groups are a way to seperate parts of a Regular Expression and evaluate them independently from the main expression. This means we can look for substrings within our original subtring. An example of such an expression is - ```/(pre)fix/``` - executed on the string . This expression will match the "pre" in "prefix" in addition to the entire word "prefix". RegEx looks for the substring "pre" as well as the entire substring "prefix". With the same logic, ```/(pre)(fix)/``` matches with "prefix", "pre", and "fix", and ```/pre(fix)/``` matches with "prefix" and "fix".

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
If you understand the other parts of RegEx continue to the [full examples](#full-examples), otherwise continue to [Character Escapes](#character-escapes)

### Character Escapes

Character escapes are ways that you can write literal characters instead of using their character class or token status. We escape a character by starting it with a ```\```. The most common usages for escape characters are when we want to match a literal period - ```\.``` - or a literal backslash - ```\\```. This applies to any character that would otherwise have a seperate meaning like ```*```, ```+```, etc.

#### Conclusion

While character escapes sometimes are not needed, it is good to remember HOW to escape a character.<br>
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

#### Conclusion

Flags are simple but important components of RegEx. They can be used to make searching large amounts of data easier<br>
If you understand the other parts of RegEx continue to the [full examples](#full-examples), otherwise continue to [Quantifiers](#quantifiers)

### Quantifiers

Quantifiers are probably the most useful component of RegEx. They move us past specificality and allow us to be more general with our searches. In summary, a quantifier is used to, well quantify, you can use a variety of syntax to declare HOW MANY of an expression to match. For example, the expression ```x{n}``` will match exactly "n" number of ocurrences of "x" if the occurence of "x" is subsequent, and ```x{n,}``` will match "x" a minimum number of "n" times if the occurence is subsequent. You can see a full list of quantifiers [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions/Quantifiers#types).

#### Really useful

We need quantifiers to match variable and flexible information. Now that we know what quantifiers can do, lets try finding all FULL numbers within a string.
```
let text = "1777 was a random year, while 2022 is a caotic year. 20 dollars is now 100 dollars."

// + is equivalent to {1,}
let exp = /[0-9]+/g
let matches = text.match(exp)

console.log(matches)
// ["1777", "2022", "20", "100"]
```
We can find both full numbers and numbers of a specific length - 
```
...
// specific length substring
exp = /[0-9]{4}/g
matches = text.match(exp)

console.log(matches)
// ["1777", "2022"]
```
Another small example would be to match any word seperated by spaces or other non-word characters - 
```
text = "Shorter text, for viewing."
// match all "words"
exp = /\w+/g
matches = text.match(exp)

console.log(matches)
// ["Shorter", "text", "for", "viewing"]
```
[See It] (https://jsfiddle.net/benw_10/ywhctp5k/) <br><br>

If you understand the other parts of RegEx continue to the [full examples](#full-examples), otherwise continue to [Assertions](#assertions)

### Assertions

An assertion is essentialy a boundry or condition that must be met to produce a match. The boundry character classes are ```^```, ```$```, ```\b```, and ```\B```.<br>
```^``` is used to denote the start of input (or the start of a line if using the multi-line flag) and ```$``` is used to denote the end of input (or the end of a line if using the multi-line flag). ```\B``` and ```\b``` will match a substring only if a word or non-word character is present in that position like in the expression - ```\b\w+\b``` - which is a generic way to seperate words by spaces, commas, etc.

#### Peeking around

Other groups of assertions are the lookahead and lookbehind assertions. We can use these to match a substring only if it is followed or preceded by an expression without matching the expression we are checking. These assertions also have a negative variant, which applies the same logic but only match if the expression is not present ahoad of or behind the base expression. For lookahead assertions we use the syntax - ```x(?=y)```. Here, "x" is only matched if followed directly by "y". The negative variant is - ```x(?!y)``` - where x is only matched if not followed directly by "y". For lookbehind assertions we use the syntax - ```(?<=y)x```. Here, "x" is only matched if preceded directly by "y". The negative variant is - ```(?<!y)x``` - where x is only matched if not preceded directly by "y".

These are useful for matching words starting with something without matching the whole word like here -
```
let text = "precompute, preprocess, postman, premake, prestage, random"
// looking behind for our "pre" substring, if it exists then check if it is followed directly by a comma or end of input to seperate each word, and then matching only word characters to remove whitespace 
let exp = /(?<=pre)\w+(?=,|$)/g
let matches = text.match(exp)

console.log(matches)
// ["compute", "process", "make", "stage"]
```
We can also use them to verify formats, parse JSON, arrays, etc. like here - 
```
// parse a comma/space seperated list into array
text = `"item1", 2, "item3", 4`

exp = /(?<=")[^",\s]+(?=")|(?<=\s|^)\d/g
matches = text.match(exp)

console.log(matches)
// ["item1", "2", "item3", "4"]
```
[See It](https://jsfiddle.net/benw_10/7rqtgezj/)<br><br>

#### Conclusion

Assertions are very useful if you want to match a string based on what comes before or after it<br>
If you understand the other parts of RegEx continue to the [full examples](#full-examples), otherwise you can go back to the table of contents [here](#table-of-contents)

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

#### Match a URL
```
// output format is [isURL, header, apex, domain, path]
let url_exp = /^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*(?:\/?)+$/

let me = "https://ben-devs.com"
console.log(me.match(url_exp))
// ["https://ben-devs.com/", "https://", "ben-devs", "com", undefined]

let gh = "https://github.com/benw10-1/regextutorial/"
console.log(gh.match(url_exp))
// ["https://github.com/benw10-1/regextutorial", "https://", "github", "com", "/benw10-1/regextutorial/"]

let invalid = "suminvalidsit#e.gmail"
console.log(invalid.match(url_exp))
// null
```
[See It](https://jsfiddle.net/benw_10/35yd6aeh/)<br><br>

#### Markup text
```
// text is text to be processed and strong is an array of words to markup
function markUp(text, strong = []) {
	// make sure our punctuation isn't already markup up
  let punc = /(?<!<.*>)[.,\/#!$%\^&\*;:{}=\-_`~()\"\'“”]+(?!<\/.*>)/g
  // use the replace function [String, replacer_func] to markup all punctuation without re-marking up a character
  text = text.replace(punc, (match) => {
    return `<span class="punc">${match.trim()}</span>`
  })
  strong.forEach(x => {
  	if (!x) return
    // same concept as punctuation, but instead we have the word itself. And to add to the word we find all non whitespace characters that follow the word
    let reg = new RegExp(`(?<!<.*>)${x}[^\\s$]*(?!<\/.*>)`, "g")
    text = text.replace(reg, (match) => {
    	return `<strong>${match}</strong>`
  	})	
  })

  return text
}
```
[See It](https://jsfiddle.net/benw_10/vhuzg17e/)<br><br>

#### Get SQL queries without comments
```
function arrayify(q) {
    // line terminators | single-line comments | multi-line comments
    let nocomment = q.replace(/[\t\r\n]|(--[^\r\n]*)|(\/\*[\w\W]*?(?=\*\/)\*\/)/g, "")
    // get queries from compressed SQL file
    return nocomment.match(/[^;]+(;|$)/g)
}
```
[See It](https://jsfiddle.net/benw_10/nqLhxpca/)<br><br>

## Author

Ben Wirth<br>
[GitHub Repo](https://github.com/benw10-1/bugTracker)<br>
[Website](https://ben-devs.com)
