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
- [Put it all together](#put-it-all-together)
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
Grouping constructs in regular expressions serve to encapsulate and organize parts of the pattern. The primary way to group a section of a regex is by using parentheses `()` which creates a subexpression. Subexpressions allow you to treat multiple characters or elements as a single unit and apply quantifiers or other operations to them.

Let's take an example from the HTML tag regex and break down the grouping constructs:
```bash
/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/ 
```
- `([a-z]+):` This is a subexpression enclosed within parentheses. It captures and groups one or more lowercase letters, which represent the tag name.
- `([^<]+)*:` Another subexpression capturing one or more characters that are not `<`. The `*` quantifier outside the parentheses repeats this subexpression zero or more times, allowing for attributes or content between the opening tag and closing tag.
- `(?:>(.*)<\/\1>|\s+\/>):` This is a non-capturing group, indicated by `(?:...)`, which means it's used for grouping purposes but doesn't create a numbered capturing group. It includes two alternative subexpressions separated by `|`. The first part `>(.*)<\/\1>` captures the content between opening and closing tags, while the second part `\s+\/>` captures self-closing tags.

In between the subexpressions, we have a colon (:).

### Character Classes
Character classes provide a way to match specific types of characters within a regex pattern. Let's explore a few common character classes:
- `\d` : means any digit 0-9 single characters
- `\w` = A-Z,a-z,0-9 characters single characters w stands for word
- `\s` = whitespace single characters
- `.` = any character single characters

These character classes can be seen in our example HTML tag regex `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`

- `[a-z]+`: This uses the character class `[a-z]` to match any lowercase letter one or more times.
- `[^<]+`: Here, `[^<]` is a character class that matches any character that is not a `<`. The `+` quantifier means one or more times.
- `\s+`: The `\s` character class matches whitespace characters, and the `+` quantifier means one or more times.
- `.`: The period `.` in `(?:>(.*)<\/\1>|\s+\/>)` matches any single character except for a newline.

### The OR Operator
Using the OR operator `|`, the expression [abc] could be written as (a|b|c).

Examples in `(?:>(.*)<\/\1>|\s+\/>)` as explained above It includes two alternative subexpressions separated by `|`. The first part `>(.*)<\/\1>` captures the content between opening and closing tags, while the second part `\s+\/>` captures self-closing tags.

### Flags
We started this tutorial by explaining that as a literal, a regex must be wrapped in slash characters. The one exception to this rule is with the component known as flags. Flags are placed at the end of a regex, after the second slash, and they define additional functionality or limits for the regex.the six optioanl flags are as listed below:
- g—Global search: the regex should be tested against all possible matches in a string.
- i—Case-insensitive search: case should be ignored while attempting a match in a string
- m—Multi-line search: a multi-line input string should be treated as multiple lines

### Character Escapes
In regular expressions, the backslash (\) serves as an escape character, allowing you to use special characters literally instead of their typical regex interpretation. This is particularly useful when you need to match specific characters that coincide with regex metacharacters or components.

Example from `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`
Let's break down the example `(.*)<\/\1>|\s+\/>)` from the HTML tag regex:

- `<\/\1>`: In this part of the pattern, `\/` matches a literal forward slash character. However, `<\/\1>` uses the `\` character escape before the forward slash to ensure it's treated as a literal character and not the closing delimiter of the regex. The `\1` is a backreference to the first capturing group `([a-z]+)`, making sure the closing tag matches the opening tag, we will dive deeper into backreference next.

### Backreferences
Backreferences, such as \1, \2, and so on, allow you to refer back to previously captured groups in a regex pattern. They provide a powerful way to match repeating patterns and maintain consistency within the content you're searching for.

Example from `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/` using the `(.*)<\/\1>|\s+\/>)` snippet like above.

By utilizing backreferences, you're essentially saying "match what you've seen before." This is incredibly handy when dealing with repetitive structures like HTML tags. Backreferences maintain consistency in your pattern, ensuring that corresponding parts of the text align correctly and adhere to the desired format.

Understanding how to employ backreferences empowers you to create more dynamic and accurate regex patterns, especially in scenarios where you need to match recurring patterns with precision.

### Non-Capturing Groups
`(?:...)` group elements without capturing them as separate groups, which can be particularly useful when dealing with complex regex patterns. This feature proves incredibly handy when you're grappling with intricate regex patterns, allowing you to maintain structure without complicating the capturing process.

Demonstrated within the `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/` We can look at this code snippet `(.*)<\/\1>|\s+\/>)` from the HTML tag regex pattern for non-capturing groups:

- `(?:>(.*)<\/\1>|\s+\/>)`: Within this part of the pattern, the non-capturing group `(?: ... )` becomes a pivotal asset, accommodating two distinct alternatives split by the OR operator `|`.
  - `>(.*)<\/\1>`: The first alternative encapsulates content between opening and closing tags, with `.*` matching any characters enclosed. Remarkably, `\1` acts as a backreference to the initial capturing group, ensuring a seamless match between opening and closing tags.
  - `\s+\/>`: The second alternative seizes whitespace followed by a forward slash `/>`, an ideal match for self-closing tags.

### Put it all together
> WARNING
> The answer of our regex code appears below, don't read on until you have had a chance to decode it yourself.

## `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`
This regex is designed to match and dissect HTML tags, ensuring they are well-formed. Here's a breakdown of the components and their functionalities:
1. `^`: Anchors the pattern to the beginning of a line.
2. `<`: Matches the literal character "<".
3. `([a-z]+)`: Capturing group 1 that matches one or more lowercase letters, representing the tag name.
4. `([^<]+)*`: Capturing group 2 that matches zero or more sequences of characters that are not "<". This section captures attribute values or content between opening and closing tags.
5. `(?:>(.*)<\/\1>|\s+\/>)`: A non-capturing group that contains two alternatives separated by the OR operator |.
    - `>(.*)<\/\1>`: Capturing group 3 within the first alternative captures content between opening and closing tags. \1 backreferences the tag name to ensure matching opening and closing tags.
    - `\s+\/>`: The second alternative matches whitespace followed by a forward slash, matching self-closing tags.
6. `$`: Anchors the pattern to the end of a line.

In summary, this regex checks whether a line represents a complete HTML tag. It captures the tag name, attributes or content, and handles both normal and self-closing tags. The backreference \1 ensures that the opening and closing tags match appropriately.
## Examples of `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`
- Normal Opening and Closing Tag:
  - `<div>`This is a div`</div>`
- Self-Closing Tag:
  - `<img src="image.jpg" alt="An image"/>`
- Opening Tag with Attributes and Content:
  - `<a href="https://www.example.com">Visit Example</a>`
- Self-Closing Tag with Whitespace:
  - `<br />`
- Nested Tags:
  - `<div><p>`This is a paragraph`</p></div>`
- Tag with Multiple Attributes and Content:
  - `<input type="text" id="username" class="input-field" placeholder="Enter username" />`

These examples showcase various scenarios where the provided regex pattern effectively matches different types of HTML tags, capturing their tag names, attributes, and content in line with the specified parameters.

### Resources 

1. [MDN Web Docs for Regular Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions )
2. [Regular Expression Tutorial](https://coding-boot-camp.github.io/full-stack/computer-science/regex-tutorial)
3. [Eloquent JavaScript (Chapter 09)](https://eloquentjavascript.net/09_regexp.html) 

## Author
This tutorial was crafted by Emily Funk (FunkE), a beginner coder on a journey to strengthen her abilities in code. Funke hopes to have helped you decipher and leverage the "HTML Tag Matcher" regex for your web development endeavors.If you have any questions or need further assistance, feel free to reach out to FunkE through her [GitHub profile](https://github.com/4FunkE) or via email at 4funkecodes@gmail.com. I'm here to help and support you in any way I can. Have a FunkE day!