# Regular Expressions

Progress: New
: No
Parent item: Module 5 -- Nov 19-Dec 1 -- Ethics, Regex, and Presentations (Module%205%20--%20Nov%2019-Dec%201%20--%20Ethics,%20Regex,%20and%20Pre%2026be7be659d98013b02cd928b5a109de.md)
Resources: https://regex101.com/
Practice: https://q.utoronto.ca/courses/394773/pages/m5-regular-expressions
Attempt myself: https://github.com/christinecheng1229/m5-regex

“conforms/matches” the Regex

a regex that matches more strings is “more **permissive**”

a regex that matches too few strings is “more **restrictive**”

![image.png](image%2032.png)

`[]` - choose **one** character from set of characters in the brackets

`*` - 0 or more multiples of *regex* (immediately) to the left

`+` - 1 or more multiples of *regex* (immediately) **to the left

`^` - anchor: must match from start of the string (can’t match a substring)

`$` - anchor: must match to the end of the string (can’t match a substring)

`?` - 0 or 1 instances 

`{`#`}` - # specifies the exact quantity of *regex* (immediately) to the left

`()` - forms a **grouping** of regex expressions

`.` - matches **every possible** character

`^` within `[]` - matches **everything but** character set in brackets

character classes: uses `\` as the escape character

`\d` - all digits (equiv. to `[0-9]`)

`\s` - any whitespace character

`\t` - tab character

`\n` - new line character

`\`# - # is the name of the grouping: determined by counting open brackets left-to-right 

→ allows for repetition of the **exact** grouping string previously used (v.s. previous repetition symbols repeat the **regex**)

**Escaping** a character means to get rid of its other meaning

TODO from lecture text file 

e.g., in Java:

```java

```

e.g., `[a-z]+\\[a-z]+` in Java:

```java
[a-z]+\\\\[a-z]+ // need to escape each backslash in the regex
```

ranges (e.g., `a-z`) are encoded with numerical values i.e., the ascii values associated with each of these symbols

thus, whenever using ranges, don’t do something like `a-Z` since there (likely) are other characters beside simply the lowercase and uppercase alphabet

- **Question 1:** Consider the regular expression: `[A-Z][0-9]+[A-Z]?` This regex matches which of the following Strings?
    
    **A.** `"A1"`
    
- **Question 2:** Consider the String: `"Hello123"` This conforms to which regular expression (regex)?
    
    **D.** `[A-Z][a-z]*[0-9]+`
    
- **Question 3:** Consider this regular expression`(\d\d)([A-Z]([a-z]))\1\3(\d){3}\2` Which of the following Strings conforms to this regular expression?
    
    **C.** `"88Az88z123Az"`
    
- **Question 4:**
    
    **C.** Use the `matcher` method from the `String` class.
    
    - ideal since you are already given a String, don’t need to separately create a Matcher
    - B. - not relevant since Matcher.group matches substrings
    - note all 3 methods work