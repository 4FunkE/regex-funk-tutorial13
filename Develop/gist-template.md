# Exploring Regex with Funk: Tackling the "HTML Tag Matcher" Regular Expression

Welcome to Funk's regex tutorial, using FunkE learning! As aspiring web developer, you're no stranger to the world of HTML tags. In this comprehensive tutorial, we'll dive into the complexities of a regular expression (regex) tailored to match and dissect HTML tags. Regex is a powerful tools using a sequence of characters that defines a search pattern for text, using pattern matching and validation. Regex follows "literal characters" or "Meta-characters." By the end of this tutorial, you'll have a comprehensive understanding of how this regex works and be well-prepared to implement it in your coding adventures.

## Summary

Briefly summarize the HTML tag regex you will be describing and what you will explain for your tutorial. Include a code snippet of the regex.

In this tutorial, we will unravel and understand the regular expression `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`, designed to match HTML tags. Our focus will be on breaking down each part of this regex, guiding you through its intricacies step by step. Let's break down each component step by step.

## Table of Contents

- [Anchors `^` and `$`](#anchors)
- [Bracket Expressions](#bracket-expressions)
- [Quantifiers `+`](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)
- [Backreferences](#backreferences)
- [Non-Capturing Groups](#non-capturing-groups)
- [Lookahead and Lookbehind](#lookahead-and-lookbehind)
- [Author](#author)

- Literal Character `@`(literal search of specific parameters)
-, a, 1, !, @, #, $, %, 
Digits: Digits from 0 to 9 are treated as literal characters in a regular expression.

Example: The pattern \d matches any digit.

Letters: Both uppercase and lowercase letters are treated as literal characters.

Example: The pattern [A-Za-z] matches any uppercase or lowercase letter.

Whitespace: Spaces, tabs, and line breaks are also treated as literal characters.

Example: The pattern \s matches any whitespace character.

Special Characters: Many special characters like $, +, (, [, etc., can be treated as literal characters when they are escaped with a backslash \.

Example: The pattern \( matches an opening parenthesis.

Punctuation Marks: Punctuation marks like . (period), , (comma), ; (semicolon), etc., are also treated as literal characters.

Example: The pattern \. matches a literal period.

Hyphen: When used within a character class, a hyphen - can be treated as a literal character if it's properly escaped or placed in a position where it doesn't indicate a range.

Example: The pattern [\-] matches a literal hyphen.

Underscore: The underscore _ is a literal character that doesn't have special meaning in most contexts.

Example: The pattern _ matches a literal underscore.

- Metacharacter (vague/generic search with same parameters) there are sudlte difference between each program being used. types of meta are single quantify and position.
`\d` : means any digit 0-9 single characters
`\w` = A-Z,a-z,0-9 characters single characters w stands for word
`\s` = whitespace single characters
`.` = any character single characters
`*` = quantifier, 0 or more times
`+` = quantifier 1 or more times
`?` = quantifier 0 or 1 time
`{}`—Curly brackets can provide three different ways to set limits for a match:
    `{ n }`—Matches the pattern exactly n number of times
    `{ n, }`—Matches the pattern at least n number of times
    `{ n, x }`—Matches the pattern from a minimum of n number of times to a maximum of x number of times
`.*` = wildcard match a literal with any number of any characters
`^` = beginning
`$` = end
`\b` = word boundary
`/` = A regex is considered a literal, so the pattern must be wrapped in slash characters (/). Note: JavaScript provides two ways to create a regex object. The first, shown in our example, uses literal notation. The second is to use a RegExp constructor. The constructor function's parameters are not enclosed within slashes; instead, they use quotation marks. To learn more, review the MDN Web Docs on the RegExp object.

. (Period): This meta-character matches any single character except for a newline character.

Example: The pattern a.b matches "axb", "aab", "a4b", etc.

* (Asterisk): The asterisk meta-character matches the preceding character or group zero or more times.

Example: The pattern ab*c matches "ac", "abc", "abbc", "abbbc", and so on.

+ (Plus): The plus meta-character matches the preceding character or group one or more times.

Example: The pattern ab+c matches "abc", "abbc", "abbbc", and so on.

? (Question Mark): The question mark meta-character matches the preceding character or group zero or one time.

Example: The pattern colou?r matches both "color" and "colour".

| (Pipe): The pipe meta-character is used for alternation, allowing you to match one pattern or another.

Example: The pattern apple|banana matches either "apple" or "banana".

[] (Square Brackets): Square brackets define a character class, allowing you to match any one character from the set within the brackets.

Example: The pattern [aeiou] matches any vowel character.

^ (Caret) Inside Square Brackets: When used as the first character inside square brackets, it negates the character class, matching any character not listed.

Example: The pattern [^0-9] matches any non-digit character.

{} (Curly Braces): Curly braces are used to specify the exact number of occurrences of the preceding character or group.

Example: The pattern a{3} matches "aaa".

\ (Backslash): The backslash is used to escape special characters, making them literal, or to introduce various character escapes for special characters like \d, \s, etc.

Example: The pattern \. matches a literal period.

() (Round Brackets): Round brackets are used to create capturing groups or non-capturing groups, and they also establish the order of operations.

## Regex Components
### Anchors `^` and `$`
- Explain anchors The journey begins with a close look at ^ and $, the anchors that mark the start and end of the line. These anchors ensure our regex applies to the entire line, which is vital when handling HTML tags.
- give example of HTML tag regex using the anchors

### Bracket Expressions
Anything inside a set of square brackets ([]) represents a range of characters that we want to match. 
- give example of brackets in html tag regex 
- give examples of tags that meet the bracket reqirments and one that would not

### Quantifiers `+`
Quantifiers like +, *, and ? and {} provide flexibility in matching patterns. We'll dive into how these quantifiers play a role in our HTML tag regex.

... revisit entire html tag, paragraph about what is is actually searching for and give examples of tags that meet requirments.

### Grouping Constructs
The primary way you group a section of a regex is by using parentheses (()). Each section within parentheses is known as a subexpression.

In between the subexpressions, we have a colon (:).

### Character Classes
`\d` : means any digit 0-9 single characters
`\w` = A-Z,a-z,0-9 characters single characters w stands for word
`\s` = whitespace single characters
`.` = any character single characters

### The OR Operator
Using the OR operator (|), the expression [abc] could be written as (a|b|c).

### Flags
We started this tutorial by explaining that as a literal, a regex must be wrapped in slash characters. The one exception to this rule is with the component known as flags. Flags are placed at the end of a regex, after the second slash, and they define additional functionality or limits for the regex.the six optioanl flags are as listed below:
- g—Global search: the regex should be tested against all possible matches in a string.
- i—Case-insensitive search: case should be ignored while attempting a match in a string
- m—Multi-line search: a multi-line input string should be treated as multiple lines

### Character Escapes
The backslash (\) in a regex escapes a character that otherwise would be interpreted literally. For example, the open curly brace ({) is used to begin a quantifier, but adding a backslash before the open curly brace (\{) means that the regex should look for the open curly brace character instead of beginning to define a quantifier. This is common when looking for strings with special characters that are the same as a particular component of a regex.

### Backreferences
Explore how backreferences like \1, \2, etc., are used to match previously captured groups and maintain consistency within HTML tags.

### Non-Capturing Groups
Learn about non-capturing groups (?:...) and how they provide a way to group elements without capturing them as separate groups, which can be particularly useful when dealing with complex regex patterns.

### Lookahead and Lookbehind
Delve into lookahead (?=...) and lookbehind (?<=...) assertions. These constructs allow you to assert whether a certain pattern exists ahead or behind the current position without consuming characters, enabling more sophisticated matching strategies.

### Resources 

MDN Web Docs for Regular Expressions https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions 
Regular Expression Tutorial https://coding-boot-camp.github.io/full-stack/computer-science/regex-tutorial
Eloquent JavaScript (Chapter 09): Regular Expressions https://eloquentjavascript.net/09_regexp.html 


## Author
This tutorial was crafted by Emily Funk (FunkE), a beginner coder on a journey to strengthen her abilities in code. Funke hopes to have helped you decipher and leverage the "HTML Tag Matcher" regex for your web development endeavors.If you have any questions or need further assistance, feel free to reach out to FunkE through her [GitHub profile](https://github.com/4FunkE) or via email at 4funkecodes@gmail.com. I'm here to help and support you in any way I can. Have a FunkE day!