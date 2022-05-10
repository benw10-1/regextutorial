# Regex Is Pretty Cool Honestly

On this page, we will be reviewing the <strong>Regular Expressions</strong> (<strong>RegEx</strong>) and their usages. We will go over examples of <strong>RegEx</strong> and their applications as well as specific parts of the <strong>RegEx syntax</strong>.

## Summary

The specific components of <strong>RegEx</strong> we are going to be going through are groups, ranges, assertions, quantifiers, character classes, flags, and character escapes. Learning all of these aspects of <strong>RegEx</strong> will allow anyone to build extremely useful <strong>RegEx</strong> statements. I will also explain how multiple components can be compounded to form a more useful expression.

## Table of Contents
- [Introduction](#groups)
- [Groups](#groups)
- [Ranges](#ranges)
- [Assertions](#assertions)
- [Quantifiers](#quantifiers)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

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
// Output: ["I'm"]
```
Without using [groups](#groups), [ranges](#ranges), or [flags](#flags), RegEx will simply look for the specified substring and return it.<br>
If it can't find the substring it will return null instead like here -
```
var exp = /I'm/;
exp.exec("Hi, some text");
// Output: null
```

### Groups

### Ranges

### Flags

### Assertions

### Quantifiers

### Character Classes

### Character Escapes

## Author

Ben Wirth<br>
[GitHub Repo](https://github.com/benw10-1/bugTracker)<br>
[Website](https://ben-devs.com)
