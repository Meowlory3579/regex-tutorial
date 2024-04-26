# A Guide to Regular Expressions: Matching an Email Address

In this tutorial, we will explore a regular expression (regex) designed to match email addresses. Regular expressions are powerful tools for validating, extracting, and manipulating text based on patterns. The regex we'll discuss is specifically tailored to ensure a string conforms to the common structure of an email address.

## Summary

We will dissect the following regex pattern that matches standard email addresses:    

/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/  

This tutorial will break down each component of this regex, explaining how each part contributes to the overall functionality of matching a valid email format.  

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [Character Escapes](#character-escapes)
- [Author](#author)

## Regex Components
In regex, the pattern is treated as a literal, which requires enclosing it with slash characters ( / ).

### Anchors
^ and $

The ^ anchor specifies that the matching should start at the beginning of the string.  
The $ anchor ensures that the matching stops at the end of the string.  

Together, they enforce that the regex does not match just a part of the string but must match the whole string from start to finish.  

In the context of our regex pattern for matching an email address:  

The ^ anchor means that the email must start directly with the characters that form the username—specifically characters from the set [a-z0-9_\.-] without any preceding characters.      

The $ anchor ensures that the email string ends right after the domain extension, which matches the pattern [a-z\.]{2,6}. This ensures the email address doesn't contain any extraneous characters after the domain extension.  

### Quantifiers
\+ and {2,6}

Quantifiers define the boundaries for how many characters your regex should match, often specifying the minimum and maximum number of characters required within a given section of the string.  

The + quantifier attached to [a-z0-9_\.-], [\da-z\.-], and [a-z\.] means that the pattern must occur one or more times. This is crucial for matching parts of an email, such as the username, domain name, and domain extension.  

The {2,6} quantifier in the expression [a-z\.]{2,6} is used to match the domain extension. It applies to the bracket expression [a-z\.], which includes any lowercase letter or a period. The quantifier dictates that these characters must appear at least 2 times but not more than 6 times, defining acceptable lengths for the domain extension (like .com, .info, .museum). This quantification ensures that the regex can flexibly match domain extensions of various lengths while adhering to typical domain naming conventions.  

### Grouping Constructs
()

Parentheses facilitate the capturing of groups; in other words, they are used to group part of a regex pattern. This regex has three groups:  
([a-z0-9_\.-]+) captures the username.  
([\da-z\.-]+) captures the domain name.  
([a-z\.]{2,6}) captures the domain extension.  

### Bracket Expressions

Bracket expressions specify a set of characters from which a match must be made. They are enclosed in square brackets ( [] ), and any character inside them is a candidate for a match. Here's how the bracket expressions break down in our email matching regex:  

[a-z0-9_\.-] — The string can contain any lowercase letter from 'a' to 'z', any number from '0' to '9', and the special characters underscore ( _ ), period ( . ), or hyphen ( - ). The hyphen is typically used in regex to denote ranges, like 'a-z'. When it appears at the end of a bracket expression or is escaped, it represents itself, thus it doesn't denote a range here.  

[\da-z\.-] — This expression is similar but uses \d, which is a character class shorthand for any digit ('0' through '9'); this simplifies specifying all digits and combines them with lowercase letters and the special characters period and hyphen. Here, the period and the hyphen are included as specific characters by escaping the period and placing the hyphen at the end.  

[a-z\.] — Specifies that the string can include any lowercase letter from 'a' to 'z' and the period ( . ). The period is escaped to indicate that it is a literal character, not a wildcard (which in regex matches any character except newline).  

In the context of our email regex, [a-z0-9_\.-] matches any part of the email username, [\da-z\.-] matches the domain name, and [a-z\.] with a quantifier {2,6} at the end matches the domain extension. Each of these bracket expressions allows for various combinations of their included characters, ensuring flexibility in how each section of the email is structured. It's essential to recognize that these patterns do not require the string to meet all these criteria simultaneously; any single match within the brackets is sufficient.  

### Character Classes
\d

In regular expressions, character classes provide a concise way to match specific types of characters. One of the most commonly used classes is \d, which represents any digit from 0 to 9. This is particularly useful in patterns like our email regex, where \d is used within the bracket expression [\da-z\.-] to match any digit in the domain name. This simplifies the regex by avoiding the need to list all ten digits.  

### Character Escapes
\

In regex, the backslash ( \ ) is used to escape characters that otherwise have a special meaning in the regex syntax. For instance, the period ( . ) normally matches any character except newline, but in our email regex it's preceded by a backslash [a-z\.], making it match a literal period, which is crucial for accurately identifying sections like the domain extension.  

## Author

This tutorial was written by Mallory Howard (https://github.com/Meowlory3579).
