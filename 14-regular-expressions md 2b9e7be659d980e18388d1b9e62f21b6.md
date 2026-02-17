# 14-regular-expressions.md

Progress: New
: No
Parent item: Module 5 -- Nov 19-Dec 1 -- Ethics, Regex, and Presentations (Module%205%20--%20Nov%2019-Dec%201%20--%20Ethics,%20Regex,%20and%20Pre%2026be7be659d98013b02cd928b5a109de.md)
Resources: https://github.com/CSC207-UofT/207-course-notes/blob/master/14-regular-expressions.md

https://github.com/CSC207-UofT/207-course-notes/blob/master/code/regex/Demo.java

https://www.rexegg.com/regex-quickstart.php

https://jenkov.com/tutorials/java-regex/index.html

https://regexcrossword.com/

https://www.w3schools.com/java/java_regex.asp
More Resources/Practice: Regex.pdf, Regex_Practice_Quiz.pdf

- We use `[` and `]` to define a choice of symbols. So `[abc]` will match "a", "b", or "c".
- By inserting a hyphen (`-`) we can specify a range. So `[a-z]` will match any lower case letter such as "a", "h", or "x"

Anchors:

- `^` matches the start of a string (ie., pattern must start at the beginning of the string)
- `$` matches the end of a string (ie., pattern must end at the end of the string)

# Examples

- Postal codes in Toronto all start with `M` and then alternate between numbers and letters, with a space in the middle. For example, "M0A 1B2" is a Toronto postal code. To describe all Toronto postal codes, we can use the regular expression `M[0-9][A-Z] [0-9][A-Z][0-9]`.
- Java naming conventions for variables in this way: `^[a-z][a-zA-Z0-9]*$` →  a conforming string must consist of a first character from `a-z`, followed by zero or more lowercase letters, uppercase letters, or digits.

# Repetition: quantifiers & groups

| **Quantifier** | **meaning** | **Example** |
| --- | --- | --- |
| `*` | zero or more | `a*` matches the empty string, `a`, `aa`, ... |
| `+` | one or more | `a+` matches `a`, `aa`, ... |
| `?` | zero or one | `a?b` matches `ab` or `b` |
| `{x}` | `x` copies | `[ab]{2}` matches `aa`, `ab`, `ba`, or `bb` |
| `{x,}` | `x` or more copies | `[a]{2,}` matches `aa`, `aaa`, ... |
| `{x,y}` | between `x` and `y` copies | `[a]{2,4}` matches `aa`, `aaa`, or `aaaa` |

Groupings: To repeat the *exact same* matching characters. To do this, we need to specify a **group** with `(` and `)`. Each group is assigned a number based on the order in which its open bracket appears from left to right.

For example, `(([de])f)\2\1` will repeat both groups. The strings that match are: "dfddf" and "efeef".

- Group 1 corresponds to the `[de]f` part of the pattern
- Group 2 corresponds to the `[de]` part of the pattern

# Character Classes

- You can make your own character classes by using square brackets like `[q-z]` and `[AEIOU]`

| **character class** | **description** |  |
| --- | --- | --- |
| `.` | any character (except a newline) |  |
| `\d` | a digit `[0-9]` |  |
| `\D` | a non-digit `[^0-9]` |  |
| `\s` | a whitespace character |  |
| `\S` | a non-whitespace character |  |
| `\w` | a word character `[a-zA-Z_0-9]` | Note that the definition of `\w` includes the `_` character. |
| `\W` | a non-word character |  |