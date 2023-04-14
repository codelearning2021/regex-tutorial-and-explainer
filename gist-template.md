# Title (replace with your title)

Introductory paragraph (replace this with your text)

## Summary

This Github Gist exists to explain and break down the parts to the following regular expression or Regex:<br>

```
/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/
```

The purpose of the regex here used for this document as an example checks and validates an HTML tags. Each section will provide a definition and talk about its use in the above regular expression.


## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)

- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)

- [Look-ahead and Look-behind](#look-ahead-and-look-behind)


## Regex Components

^ - matches the beginning of the string.
< - matches a literal "<" character.
([a-z]+) - captures one or more lowercase letters between the "<" and the following space or ">" character. This represents the name of the HTML tag.
([^<]+)* - matches zero or more characters that are not "<", followed by any number of repetitions of this pattern. This represents the attributes of the HTML tag.
(?:>(.*)<\/\1>|\s+\/>) - matches either the contents of the HTML tag or a self-closing tag. This is a non-capturing group, denoted by the "(?:...)" syntax. It contains two alternatives separated by the "|" character:
>(.*)<\/\1> - matches the ">" character followed by any number of characters (including newlines) until a closing tag "</" with the same name as the opening tag (captured in group 1) is found, followed by a ">". The contents of the tag are captured in group 2.
\s+\/> - matches one or more whitespace characters followed by a "/>" character, representing a self-closing tag.
$ - matches the end of the string.
So, this regular expression can be used to match an HTML tag with its attributes and contents. For example, it can match the following string:

'''
<div class="gist1">
  Here is the actual textual content.
</div>
'''

In this case, the opening tag <div id="my-div"> will be matched by the regular expression, with "div" captured in group 1, "class="div1"" captured in group 2, and "This is some text inside a div." captured in group 3.


### Anchors

Anchors are special characters that will match a pattern only if it appears at a specific position in the input string. There are two types of anchors, the caret (^) anchor which matches the beginning of a line or string, and the dollar sign anchor ($) for matching the end of a line or string.<br>

The use of ^ here in the above Regex matches the beginning of the string and then searches for the literal character <, the beginning of any html tag.<br>

The use of $ at the very end here is meant to match the end of the string, indicating the previous pattern (end tag).<br>


### Quantifiers

Quantifiers are special characters that allow you to specify the amount of times a character or group of characters should be matched in any string. Easy way to remember is that "quantity" shares the root word. The quantifiers used in the above regex are:<br>

"*" matches **zero** or more occurrences of the preceding character or group.<br>

"+" matches **one or more** occurrences of the preceding character or group.<br>

"?" matches **zero or one** occurrence of the preceding character or group.<br>

"{n}" matches **exactly n** occurrences of the preceding character or group.<br>

"{n,}" matches **at least n** occurrences of the preceding character or group.<br>

"{n,m}" matches **between n and m** occurrences of the preceding character or group.<br>

In our given Regex html example, the quantifiers are as follows:

```
/^<([a-z]+)([^<]+)*
```

This uses the + quantifier twice - one or more characters need to match in the preceding group.

```
(?:>(.*)<\/\1>|\s+\/>)$/

```

The ? is here to match either 0 or 1 occurrence of the preceding character/group, either the contents of the HTML tag or a self-closing tag.<br>

Finally the first * matches zero or more characters that are not "<", followed by any number of repetitions of this pattern.<br>

```
>(.*)<\/\1>
```

The above uses * in matching the ">" character followed by any number of characters (including newlines) until a closing tag "</" with the same name as the opening tag (captured in group 1) is found, followed by a ">". The contents of the tag are captured in group 2.


### OR Operator

The OR operator is written as (|). It allows multiple alternative patterns to equally match, such as this|that, "this or that."<br>

```
(?:>(.*)<\/\1>|\s+\/>)
```

It's used her to match either the contents of the HTML tag or a self-closing tag.

### Character Classes

Enclosing a set of characters within square brackets ([]) allows that set of characters to define a pattern.<br>


```[a-z]```

Here, "[a-z]" matches any lowercase letter from "a" to "z" between the "<" and the following space or ">" character. This defines the HTML tag.

### Flags

Flags modify the behavior of a pattern match. Flags will have one or more letters placed after the final delimiter of a regular expression.<br>

Some flags and what they indicate are i (case-insensitive), g (global), m (multiline), s (dotall), u (unicode), y (sticky). Flags can be used individually or in combination with other flags.


### Grouping and Capturing

Grouping and capturing are ways to specify and pull out smaller patterns or subpatterns from a larger pattern.<br>

Grouping use parentheses, (). This creates a group that can be treated as a single unit within the larger pattern.<br>

Capturing remembers part of the input string that matches the group. They can be extracted separately.<br>

All examples can be found throughout this particular Regex. Consider: <br>

```
/^<([a-z]+)
([^<]+)*
(?:>(.*)<\/\1>|\s+\/>)
```

The first two are captured groups while the final group is non-capturing, given that it begins with a ?.<br>


### Bracket Expressions

Bracket expressions define a set of characters that can be matched by a single pattern. They are similar to character classes but provide more flexibility in specifying the set of characters that will be matched.<br>

Bracket expressions are denoted by enclosing a set of characters or character ranges within square brackets ([]).<br>

 <!-- For example, the regular expression [abc] matches any one of the three characters "a", "b", or "c". -->

You can also use character ranges within a bracket expression to match a range of characters. For example, the regular expression [a-z] matches any lowercase letter from "a" to "z", while the regular expression [A-Z] matches any uppercase letter from "A" to "Z".

In addition to specifying individual characters and ranges, bracket expressions also support a number of special characters that match particular sets of characters. Some of the most commonly used special characters include:

. - Matches any character except newline characters.

\d - Matches any digit character (equivalent to [0-9]).

\s - Matches any whitespace character (spaces, tabs, newlines, etc.).

\w - Matches any word character (letters, digits, and underscores).

^ - Negates the bracket expression, matching any character that is not in the set.

For example, the regular expression [^a-z\s] matches any character that is not a lowercase letter or whitespace character.

Bracket expressions are a powerful tool for defining complex sets of characters to be matched by a regular expression.

### Greedy and Lazy Match

In regular expressions, greedy and lazy matches refer to the behavior of quantifiers when used to match multiple occurrences of a pattern.

By default, quantifiers are greedy, meaning they match as many occurrences of the pattern as possible while still allowing the overall pattern to match. For example, the regular expression a.*b would match the entire string "aabcdb", because the .* quantifier matches the longest possible sequence of characters between the "a" and "b".

Lazy matches, on the other hand, match as few occurrences of the pattern as possible while still allowing the overall pattern to match. Lazy matches are denoted by adding a question mark (?) after the quantifier. For example, the regular expression a.*?b would match only the substring "aab", because the .*? quantifier matches the shortest possible sequence of characters between the "a" and "b".

Lazy matches are useful when you want to match only the shortest possible substring that satisfies a pattern. They can also be used to avoid catastrophic backtracking, which can occur when a greedy quantifier causes the regular expression engine to explore a large number of possible matches before finding a successful match.

In general, it's a good practice to use lazy matches only when you specifically need them, as they can be less efficient than greedy matches in some cases.




### Boundaries

Boundaries are special characters that match the position **between** characters, rather than the characters themselves. They allow you to specify where a match should occur in relation to other characters in the input string.<br>

There types of boundaries in regular expressions are word boundaries (/b) and line boundaries (^ and $).



Word boundaries: \b
Word boundaries match the position between a word character (as defined by the \w character class) and a non-word character. For example, the regular expression \bcat\b would match the word "cat" only when it appears on its own, and not as part of another word like "scattered" or "category".

Line boundaries: ^ and $
Line boundaries match the beginning (^) or end ($) of a line in the input string. For example, the regular expression ^hello would match the word "hello" only when it appears at the beginning of a line.

Lookahead and lookbehind boundaries: (?=) and (?<=)
Lookahead and lookbehind boundaries are used to specify a pattern that must occur immediately before ((?<=)) or after ((?=)) the current position, without including that pattern in the match itself. For example, the regular expression \d(?=px) would match any digit that is immediately followed by the characters "px", without including "px" in the match.

Boundary characters are useful for creating more precise regular expressions that match specific patterns in the input string. By using boundaries, you can control where a match can occur in relation to other characters, and avoid matching unintended patterns that might be similar but not exactly what you're looking for.




### Back-references

Back-references (such as /1) are a way to reuse any part of a pattern that has been earlier matched in the same regular expression.<br>

A back slash is used here in the Regex example to refer back to the first "group" that was within the first html tag, as this should match the closing tag as well:

```
<\/\1>
```

### Look-ahead and Look-behind

In regular expressions, look-ahead and look-behind allow you to match a pattern only if it is followed (look-ahead) or preceded (look-behind) by another pattern but **NOT** in that pattern in the match itself. You can recognize them by the (?=...) for positive look-ahead, (?!=...) for negative look-ahead, (?<=...) for positive look-behind, and (?<!...) for negative look-behind, whereas ... is the pattern to match.<br>

This Regex doesn't make use of either look-ahead or look-behind.

## Author

Nate Johnson here, working on coding while working full time. Looking to stay relevant in IT by expanding upon my ever-growing, relevant skill set.