# Exploring Regex with Funk: Tackling the "HTML Tag Matcher" Regular Expression

Welcome to FunkE Learning's regex tutorial! As an aspiring web developer, you're likely familiar with the intricate world of HTML tags. In this comprehensive tutorial, we'll delve into the intricacies of a regular expression (regex) designed to identify and dissect HTML tags. Regex, a sequence of characters that defines a search pattern for text, offers powerful pattern matching and validation capabilities. It's built upon a foundation of "literal characters" and "meta-characters." By the end of this tutorial, you'll gain a comprehensive understanding of how this regex functions, empowering you to confidently incorporate it into your coding endeavors.

## Summary

In this tutorial, we will dissect and comprehend the regular expression `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`, designed to match HTML tags. Our focus will be on breaking down each part of this regex, guiding you through its intricacies step by step. Let's break down each component step by step.

## Table of Contents

- [Anchors](#anchors)
- [Bracket Expressions](#bracket-expressions)
- [Characters](#characters) (Literal and Metacharacters)
- [Grouping Constructs](#grouping-constructs)
- [Character Classes](#character-classes)
- [Quantifiers](#quantifiers)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)
- [Backreferences](#backreferences)
- [Non-Capturing Groups](#non-capturing-groups)
- [Lookahead and Lookbehind](#lookahead-and-lookbehind)
- [Author](#author)

## Regex Components
### Characters
#### Literal Characters

In regular expressions, literal characters are used to specify exact characters that match themselves. Here are different types of literal parameters:
- **Digits:** From 0 to 9 are treated as literal characters in a regular expression. 
  - Example: The pattern `\d` matches literal digit.
- **Letters**: Both uppercase and lowercase letters are treated as literal characters.
  - Example: The pattern `[A-Za-z]` matches any uppercase or lowercase letter.
- **Whitespace:** Spaces, tabs, and line breaks are also treated as literal characters.
  - Example: The pattern `\s` matches any whitespace character.
- **Special Characters:** Many special characters like `$`, `+`, `(`, `[`, etc., can be treated as literal characters when they are escaped with a backslash `\`.
  - Example: The pattern `\(` matches an opening parenthesis or `\[` matches an opening square bracket.
- **Punctuation Marks**: Punctuation marks like `.` (period), `,` (comma), `;` (semicolon), etc., are treated as literal characters when they are escaped with a backslash `\`.
  - Example: The pattern `\.` matches a literal period.
- **Hyphen**: When used within square brackets `[]`, also known as character class, a hyphen `-` can be treated as a literal character if it's properly escaped with a backslash `\` or placed in a position where it doesn't indicate a range.
  - Example: The pattern `[\-]` matches a literal hyphen.
- **Underscore**: The underscore `_` is a literal character that doesn't have special meaning in most contexts. Usually indicating a break or space but in this case only represents underscore.
  - Example: The pattern `_` matches a literal underscore.

#### Metacharacter 
Metacharacters represent generalized search patterns with common parameters. Although there are subtle differences between various programming environments, the fundamental types of meta-characters include those for single character matching and position assertion.
- `\d` (Digit): means any single digit (0-9).
  - Example: The pattern `\d` matches "4" in "42" and "3" in "365".
- `\w` (Word): Represents characters A-Z, a-z, and 0-9.
  - Example: The pattern `\w` matches "A" in "Apple" and "3" in "cat3".
- `\s` (Space): Matches whitespace characters.
  - Example: The pattern `\s` matches spaces in "hello world".
- `.*` (Wildcard): Matches any number of any characters.
  - Example: The pattern `a.*b` matches "axxb", "ayyyb", and "azzzbbb".
- `$` (Money Sign): Matches the end of a line.
  - Example: The pattern `apple$` matches "pineapple" but not "apples".
- `\b` (Boundary): Matches a word boundary.
  - Example: The pattern `\bapple\b` matches "apple" in "apple pie" but not in "pineapple".
- `.` (Period): Matches any single character except for a newline.
  - Example: The pattern `a.b` matches "axb", "aab", "a4b", etc.
- `*` (Asterisk): Matches the preceding character/group 0 or more times.
  - Example: The pattern `ab*c` matches "ac", "abc", "abbc", "abbbc", and so on.
- `+` (Plus): Matches the preceding character/group 1 or more times.
  - Example: The pattern `ab+c` matches "abc", "abbc", "abbbc", and so on.
- `?` (Question Mark): Matches the preceding character/group 0 or 1 time.
- Example: The pattern `colou?r` matches both "color" and "colour".
- `|` (Pipe): Allows matching one pattern or another.
  - Example: The pattern `apple|banana` matches either "apple" or "banana".
- `[]` (Square Brackets): Defines a character class, matches any character from the set.
  - Example: The pattern `[aeiou]` matches any vowel character.
- `^` (Caret) Inside Square Brackets: Negates the character class.
  - Example: The pattern `[^0-9]` matches any non-digit character.
- `{}` (Curly Braces): Specifies the exact number of occurrences of the preceding character/group.
  - Example: The pattern `a{3}` matches "aaa".
    - `{ n }`—Matches the pattern exactly n number of times
    - `{ n, }`—Matches the pattern at least n number of times
    - `{ n, x }`—Matches between n and x times.
- `\` (Backslash): The backslash is used to escape special characters, making them literal, or to introduce various character escapes for special characters like `\d`, `\s`, etc.
  - Example: The pattern `\.` matches a literal period. Note: In JavaScript, you can create a regex object using literal notation or the RegExp constructor. For more details, refer to the [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) on the RegExp object.
- `()` (Round Brackets): Creates capturing or non-capturing groups and defines order of operations.
  - Example: The pattern `(a|b)c` matches either "ac" or "bc".

### Anchors
Anchors mark the start and end of a regex line. `^`(caret) indicates the beginning and `$` (money sign) indicates the end. These anchors ensure that our regex applies to the entire line, which is vital when handling HTML tags.

When working with regular expressions in the context of HTML tags, the use of anchors is essential to precisely target the tags within the entire content. By placing ^ at the beginning of the regex and $ at the end, you ensure that the regex matches the HTML tag patterns from the start to end.

Let's look back at our example of the HTML tag regex. see if you can spot the `^` and `$` asserting its the position at the beginning of the line and at the end.
```bash
/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/ 
```
*Note: The `/` (forward slash) at the beginning and end of the regular expression are often used in some programming languages to delimit the regular expression pattern. However, they are not part of the actual regular expression syntax.*

### Bracket Expressions
Bracket expressions, denoted by square brackets `( [] )`, allow us to define a set of characters or ranges that we want to match. The regular expression engine will match any single character within the specified range.

When dealing with HTML tags, bracket expressions capture specific character ranges commonly found in tag names, attribute names, or other parts of tags.

### Quantifiers
Quantifiers like +, *, and ? and {} provide flexibility in matching patterns. We'll dive into how these quantifiers play a role in our HTML tag regex.
#### Example of Brackets in HTML Tag Regex
Consider this portion of the HTML tag regex using bracket expressions:
```bash
[a-z]+ 
```
In this example, `[a-z]` within the bracket expression matches any lowercase letter. The + outside the brackets indicates that one or more lowercase letters should be matched. The `+` symbol is a quantifier that means one or more, meaning `[a-z]+` matches one or more characters that are lowercase. 

For Example:
- `<div>`: The tag name "div" meets the requirement of `[a-z]+` because it consists of lowercase letters.
- `<a>`: Similarly, the tag name "a" matches the bracket expression.

However,
- `<h2>`: The tag name "h2" **DOES NOT** meet the bracket requirement `[a-z]+` as it includes lowercase letters along with numbers.

---

Now, consider this portion of the HTML Tag regex following the bracket expression:
```bash
[^<]+ 
```
The regex pattern `[^<]+` is a character class that matches one or more characters that are not the less-than symbol `<`. The `^` symbol is used as a negation operator meaning "not." The `+` symbol is a quantifier that means "one or more," so `[^<]+` matches one or more characters that are not `<`. 

For example:
- Text Between Tags: The content "This is some text" matches the pattern `[a-z]+` because it consists of characters that are not `<`.
```bash
<p>This is some text</p>
```
- Attribute Values: The attribute value "image.jpg" matches the pattern `[a-z]+` because it's composed of characters that are not `<`.
```bash
<img src="image.jpg" alt="An example image">
```
However,

- Tag name: `<div>` does not match the pattern `[a-z]+` because it contains characters that are `<`, specifically the characters d, i, and v. The pattern `[^<]+` is designed to match any sequence of characters that do not include the less-than symbol `<`. It's often used to capture content between tags or within attribute values where the less-than symbol is not allowed.

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