---
title: 🧮 Regex
---

- https://regex101.com/
  > Online regex tester and debugger
- https://www.regular-expressions.info/
  > Regex Tutorial, Examples and Reference

### General tokens

`\n`
:   Matches a newline character.

`\r`
:   Matches a carriage return, unicode character `U+2185`.

`\t`
:   Matches a tab character.

`\f`
:   Matches a form-feed character.

`\0`
:   Matches a null character, most often visually represented in unicode using `U+2400` `␀`.

### Anchors

`^`
:   Matches the start of a string without consuming any characters.

`$`
:   Matches the end of a string without consuming any characters. 

`\A`
:   Matches the start of a string only. Unlike `^`, this is not affected by multiline mode.

`\Z`
:   Matches the very end of a string only. Unlike `$`, this is not affected by multiline mode.

`\b`
:   Matches, without consuming any characters, immediately between a character matched by `\w` and a character not matched by `\w` (in either order).

`\B`
:   Matches, without consuming any characters, at the position between two characters matched by `\w` or `\W`.

### Meta sequences

`.`
:   Matches any character other than newline (or including line terminators with the `/s` flag).

`a|b`
:   Matches either what is before the `|` or what is after it - in this case `a` or `b`.

`\s`
:   Matches any space, tab or newline character.

`\S`
:   Matches anything other than a space, tab or newline.

`\d`
:   Matches any decimal digit. Equivalent to `[0-9]`.

`\D`
:   Matches anything other than a decimal/digit.

`\w`
:   Matches any letter, digit or underscore. Equivalent to `[a-zA-Z0-9_]`.

`\W`
:   Matches anything other than a letter, digit or underscore. Equivalent to `[^a-zA-Z0-9_]`.

`\v`
:   Matches unicode vertical whitespace.

`\#`
:   Usually referred to as a `backreference`, this will match a repeat of the text matched and captured by the capture group `#` (number) specified.

`\xYY`
:   Matches the 8-bit character with the given hex value.

`\ddd`
:   Matches the 8-bit character with the given octal value.

### Quantifiers

`a?`
:   Matches an `a` character or nothing.

`a*`
:   Greedy quantifier.  
    Matches zero or more consecutive `a` characters (gready).

`a*?`
:   Lazy quantifier.  
    Matches as few characters as possible (lazy).

`a*+`
:   Possessive quantifier.
    Matches as many characters as possible; backtracking can't reduce the number of characters matched. Because it is greedy, it will match all the way to the last digit, leaving nothing else for the . to match.

`a+`
:   Matches one or more consecutive `a` characters.

`a{3}`
:   Matches exactly 3 consecutive `a` characters.

`a{3,}`
:   Matches at least 3 consecutive `a` characters.

`a{3,6}`
:   Matches between 3 and 6 (inclusive) consecutive `a` characters.

### Group constructs

`(?:...)`
:   A non-capturing group allows you to apply quantifiers to part of your regex but does not capture/assign an ID.

`(...)`
:   Isolates part of the full match to be later referred to by ID within the regex or the matches array. IDs start at 1.

`(?#...)`
:   Any text appearing in this group is ignored in the regex.

`(?P<name>...)`
:   This capturing group can be referred to using the given name instead of a number. Alternative notation for `(?<name>...)` and `(?'name'...)` when using a PCRE flavor.

`(?=...)`
:   Positive Lookahead.  
    Asserts that the given subpattern can be matched here, without consuming characters

`(?!...)`
:   Negative Lookahead.  
    Starting at the current position in the expression, ensures that the given pattern will not match. Does not consume characters.

`(?<=...)`
:   Positive Lookbehind.  
    Ensures that the given pattern will match, ending at the current position in the expression. The pattern must have a fixed width. Does not consume any characters.

`(?<!...)`
:   Negative Lookbehind.  
    Ensures that the given pattern would not match and end at the current position in the expression. The pattern must have a fixed width. Does not consume characters.

### Character classes

`[abc]`
:   Matches either an `a`, `b` or `c` character

`[^abc]`
:   Matches any character except for an `a`, `b` or `c`

`[a-z]`
:   Matches any characters between `a` and `z`, including `a` and `z`.

`[^a-z]`
:   Matches any characters except those in the range `a-z`.

`[a-zA-Z]`
:   Matches any characters between `a-z` or `A-Z`.
