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

[Query Parameters keys](https://regexr.com/7hi0g)
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


Let's try to find a regex that matches the desired lookbehind.  It needs to match from the start of the url to the first question mark.  In other words, there is some number of non-question mark characters, followed by one question mark.

`/.*/`  This regualar expression matches literally anything.  The period '.' here represents any character, and the asterisk '*' means 0 or more of the preceding character.  We want 0 or more non-question mark characters.  Other quantifiers include

* `a+`: 1 or more
* `a?`: optional, 0 or 1 
* `a{n}`: exactly _n_
* `a{n,}`: _n_ or more
* `a{n,m}`: between _n_ and _m_
* `a+?`, `a{2,}`: "lazy" quantifiers, match as few as possible.

`/.*\?/`  Placing expressions next to each other simply means that they come after one another in that order.  Since the question mark has another meaning as a "lazy" quanitifier when located after an asterisk, it must be escaped with a backslash to mean the character itself.

`/[^?]*\?/`  The brackets are a way to group a set of characters together.  In this case, the carat '^' means this is a negated set.  So `[^?]` means any non-question mark character.  Since the question mark has no other meaning immediately after a carat, it is not necessary for it to be escaped.

`/^[^?]*\?/`  We need the lookbehind sequence to match starting at the beginning, in order to for the question mark to be the very first in the sequence.  So we need an *anchor* which matches a position, not a character in the string.  A carat '^' matches the beginning of the string, and a dollar sign '$' matches the end of the string.  Other anchors include `\b` for a word boundary, and `\B` for not a word boundary.  Note that the carat has different meanings in different contexts.

Now we have a sequence that matches exactly the url path plus the first question mark, indicating the start of the query parameters.  This could be the lookbehind for the very first key, but not the rest.  We need to add a sequence to include the characters between the first question mark and an ampersand '&'.

`/^[^?]*\?.*&/`  This is a good start, matching any number of characters, plus an ampersand.  But we want to make sure that we are not matching anything in the fragment identifier.

`/^[^?]*\?[^#]*&/`  Now the regex only allows non-hash '#' characters between the `?` and the `&`.

Now this sequence won't match the string before the first key anymore.  There are a few options to fix this.

`/^[^?]*\?[^#]*&?/`  First, we could use a quantifier after the ampersand, indicating there must only be either 0 or 1 of them.  This works for the first key since there are 0 non-hash characters and 0 ampersands, which are included by the quantifiers `*` and `?`.

`/^[^?]*\?([^#]*&)?/`  We can be a little more precise.  Quantifiers can refer to a group, as well.  Adding a '?' quantifier to the group `([^#]*&)` means to match exactly 0 or 1 of the whole sequence.


`/^[^?]*\?[^#]*=/`Now, for the lookbehind for the query parameter values, we want almost the same thing, except we want it to come after an equals sign.  Since all the values come after an equals sign, we don't need to add any special quantifiers.  



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

