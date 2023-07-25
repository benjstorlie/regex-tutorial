https://gist.github.com/benjstorlie/052e6c08b1828ee3c3b48cd1393238f7

# URL Query Parameters Regular Expression



## Summary

Briefly summarize the regex you will be describing and what you will explain. Include a code snippet of the regex. Replace this text with your summary.

## Table of Contents

- [Lookaround](#lookarounds)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components

https://developer.mozilla.org/en-US/docs/Learn/Common_questions/Web_mechanics/What_is_a_URL

[Query Parameters Fields](https://regexr.com/7hi0g)
[Query Parameters Values](https://regexr.com/7hi0j)

`/(?<=(^[^\?]*\?)(|[^#]*&))[^=#]+(?==)/g`

`/(?<=(^[^\?]*\?)([^#]+=))[^&#]+(?=(&|#|$))/g`

To find just the query parameters, we need to use lookarounds, expressions that match strings before or after the main pattern.

Since the question mark (?), ampersand (&) and equals sign (=) are reserved characters in a url, specifically for query parameters, we don't have to worry about matching them in the url path (the main part of the url prior to the question mark).

Describing what pattern we want to match in words, the keys should be:

* after the first question mark '?'
* preceded by either the first question mark, or an ampersand '&'
* ending at an equals sign '='

and the values should be:

* after the first question mark '?'
* preceded by an equals sign '='
* ending at either an ampersand '&', the end of the input string, or '#' indicating the end of the query string and start of the anchor.

### Lookarounds

### Quantifiers

### Grouping Constructs

### Bracket Expressions

### Character Classes

### The OR Operator

### Flags

### Character Escapes

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)

