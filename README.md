<br/>
<p align="center">
<img src="https://i.imgur.com/bYwl7Vf.png" alt="Learn Regex">
</p><br/>

## What is Regular Expression? 什么是正则表达式？

> Regular expression is a group of characters or symbols which is used to find a specific pattern from a text. 

> 正则表达式是一组用来从一段文字中匹配一个特定模式的字符或符号。

A regular expression is a pattern that is matched against a subject string from left to right. The word "Regular expression" is a 
mouthful, you will usually find the term abbreviated as "regex" or "regexp". Regular expression is used for replacing a text within 
a string, validating form, extract a substring from a string based upon a pattern match, and so much more.

正则表达式是从左至右匹配主体字符串的一种模式。"Regular expression"是正则表达式的全程，很多时候，你会经常看到其缩写 "regex" 或 "regexp"。正则表达式用于从一个字符串中替换一段文字，表单验证，根据指定的匹配模式从字符串中提取出一段子字符串等等。

Imagine you are writing an application and you want to set the rules when user choosing their username. We want the username can 
contains letter, number, underscore and hyphen. We also want to limit the number of characters in username so it does not look ugly. 
We use the following regular expression to validate a username:

假设你正在开发一个应用，你想要用户在设置用户名的时候遵循特定的规则。我们希望用户名包含字母，数字，下划线和连接符，同时还希望限制用户名的长度使其看起来更加美观；我们就可以使用以下正则表达式来验证用户名:
<br/><br/>
<p align="center">
<img src="https://i.imgur.com/ekFpQUg.png" alt="Regular expression">
</p>

Above regular expression can accept the strings `john_doe`, `jo-hn_doe` and `john12_as`. It does not match `Jo` because that string 
contains uppercase letter and also it is too short.  

上述正则表达式可以匹配如下字符串：`john_doe`, `jo-hn_doe` 和 `john12_as`，但是它不匹配 `Jo`，因为字符串长度太短，并且含有大写字母。

## Table of Contents 目录

- [Basic Matchers](#1-basic-matchers)
- [Meta character](#2-meta-characters)
  - [Full stop](#21-full-stop)
  - [Character set](#22-character-set)
    - [Negated character set](#221-negated-character-set)
  - [Repetitions](#23-repetitions)
    - [The Star](#231-the-star)
    - [The Plus](#232-the-plus)
    - [The Question Mark](#233-the-question-mark)
  - [Braces](#24-braces)
  - [Character Group](#25-character-group)
  - [Alternation](#26-alternation)
  - [Escaping special character](#27-escaping-special-character)
  - [Anchors](#28-anchors)
    - [Caret](#281-caret)
    - [Dollar](#282-dollar)
- [Shorthand Character Sets](#3-shorthand-character-sets)
- [Lookaround](#4-lookaround)
  - [Positive Lookahead](#41-positive-lookahead)
  - [Negative Lookahead](#42-negative-lookahead)
  - [Positive Lookbehind](#43-positive-lookbehind)
  - [Negative Lookbehind](#44-negative-lookbehind)
- [Flags](#5-flags)
  - [Case Insensitive](#51-case-insensitive)
  - [Global search](#52-global-search)
  - [Multiline](#53-multiline)
- [Bonus](#bonus)

## 1. Basic Matchers 普通匹配

A regular expression is just a pattern of letters and digits that we use to perform search in a text.  For example, the regular expression 
`cat` means: the letter `c`, followed by the letter `a`, followed by the letter `t`. 

用于在文本中搜寻字母和数字的一种匹配模式。例如，正则表达式 `cat` 表示为：字母 `c` 紧跟着字母 `a` 在紧跟着字母 `t`。

<pre>
"cat" => The <a href="#learn-regex"><strong>cat</strong></a> sat on the mat
</pre>

[Test the regular expression](https://regex101.com/r/FOq5Nb/1)

The regular expression `123` matches the string "123". The regular expression is matched against an input string by comparing each 
character in the regular expression to each character in the input string, one after another. Regular expressions are normally
case-sensitive so the regular expression `Cat` would not match the string "cat".

正则表达式 `123` 匹配字符串"123"。正则表达式中的每个字符逐个与输入的字符串中的每个字符进行比较和匹配。正则表达式是区分大小写的，因此正则表达式 `Cat` 不会匹配字符串"cat"。

<pre>
"Cat" => The cat sat on the <a href="#learn-regex"><strong>Cat</strong></a>
</pre>

[Test the regular expression](https://regex101.com/r/jw4Vi6/1)

## 2. Meta Characters 元字符

Meta characters are the building blocks of the regular expressions.  Meta characters do not stand for themselves but instead are 
interpreted in some special way. Some meta characters have a special meaning that are written inside the square brackets. 
The meta characters are as follows:

元字符是正则表达式组成的一部分，它并不代表着自身，而是以一些特殊的方式来解释。有一些元字符在方括号内有着特殊的意义。元字符如下：

|Meta character|Description|
|:----:|----|
|.|Period matches any single character except a line break.|
|[ ]|Character class. Matches any character contained between the square brackets.|
|[^ ]|Negated character class. Matches any character that is not contained between the square brackets|
|*|Matches 0 or more repetitions of the preceding symbol.|
|+|Matches 1 or more repetitions of the preceding symbol.
|?|Makes the preceding symbol optional.|
|{n,m}|Braces. Matches at least "n" but not more than "m" repetitions of the preceding symbol.|
|(xyz)|Character group. Matches the characters xyz in that exact order.|
|&#124;|Alternation. Matches either the characters before or the characters after the symbol.|
|&#92;|Escapes the next character. This allows you to match reserved characters <code>[ ] ( ) { } . * + ? ^ $ \ &#124;</code>|
|^|Matches the beginning of the input.|
|$|Matches the end of the input.|

|元字符|具体描述|
|:----:|----|
|.|匹配除了换行符以外的所有字符。|
|[ ]|字符类。匹配任何包含在方括号内的所有字符。|
|[^ ]|反字符类。匹配任何不包括在方括号内的所有字符。|
|*|匹配 * 前的字符0次或者多次。|
|+|匹配 + 前的字符至少1次或者多次。|
|?|? 前的字符为匹配可选条件。|
|{n,m}|大括号，匹配 {} 前的字符至少 n 次但不超过 m 次。|
|(xyz)|字符组，按照括号内的字符顺序来匹配。|
|&#124;|或，匹配 &#124; 前的字符或其后的字符。|
|&#92;|转义符，允许你匹配类似一下字符 <code>[ ] ( ) { } . * + ? ^ $ \ &#124;</code>|
|^|匹配的开头。|
|$|匹配的结尾。|

## 2.1 Full stop 结尾符

Full stop `.` is the simplest example of meta character. The meta character `.` matches any single character. It will not match return 
or new line characters. For example, the regular expression `.ar` means: any character, followed by the letter `a`, followed by the 
letter `r`.

结尾符 `.` 是元字符里最简单的一个。 `.` 匹配任何字符，但不匹配换行符。例如，正则表达式 `.ar` 表示为：匹配任何包含字符 `a` 且紧跟着字符 `r`的字符串。

<pre>
".ar" => The <a href="#learn-regex"><strong>car</strong></a> <a href="#learn-regex"><strong>par</strong></a>ked in the <a href="#learn-regex"><strong>gar</strong></a>age.
</pre>

[Test the regular expression](https://regex101.com/r/xc9GkU/1)

## 2.2 Character set 字符集

Character sets are also called character class. Square brackets are used to specify character sets. Use a hyphen inside a character set to 
specify the characters' range. The order of the character range inside square brackets doesn't matter. For example, the regular 
expression `[Tt]he` means: an uppercase `T` or lowercase `t`, followed by the letter `h`, followed by the letter `e`.

字符集也称为字符类，其中方括号经常用于指定字符集。在字符集中使用连接符 `-` 来表示字符的范围，字符集中的字符顺序没有特定的意思，不影响匹配。例如，正则表达式 `[Tt]he` 表示：一个大写的 `T` 或者一个小写的 `t` ，紧跟着字母 `h` 和 `e` 。

<pre>
"[Tt]he" => <a href="#learn-regex"><strong>The</strong></a> car parked in <a href="#learn-regex"><strong>the</strong></a> garage.
</pre>

[Test the regular expression](https://regex101.com/r/2ITLQ4/1)

A period inside a character set, however, means a literal period. The regular expression `ar[.]` means: a lowercase character `a`, followed by letter `r`, followed by a period `.` character.

字符集中的句号仅仅表示为句号。正则表达式 `ar[.]` 表示：一个小写的字符 `a`，紧跟着一个字母 `r` 和字符句号 `.`。

<pre>
"ar[.]" => A garage is a good place to park a c<a href="#learn-regex"><strong>ar.</strong></a>
</pre>

[Test the regular expression](https://regex101.com/r/wL3xtE/1)

### 2.2.1 Negated character set 反字符集

In general, the caret symbol represents the start of the string, but when it is typed after the opening square bracket it negates the 
character set. For example, the regular expression `[^c]ar` means: any character except `c`, followed by the character `a`, followed by 
the letter `r`.

通常来说，插入符号代表字符串的开头，但当它位于方括号里时，它就表示为取反。比如，正则表达式 `[^c]ar` 表示为：匹配任何除了字符 `c` ，紧跟着字符 `a` 和 `r`的所有字符。 

<pre>
"[^c]ar" => The car <a href="#learn-regex"><strong>par</strong></a>ked in the <a href="#learn-regex"><strong>gar</strong></a>age.
</pre>

[Test the regular expression](https://regex101.com/r/nNNlq3/1)

## 2.3 Repetitions 重复

Following meta characters `+`, `*` or `?` are used to specify how many times a subpattern can occur. These meta characters act 
differently in different situations. 

`+` ， `*` ， `?` 通常用于指定子匹配模式匹配多少次。这些元字符在不同的场景下表示和不同的意思。

### 2.3.1 The Star 星号

The symbol `*` matches zero or more repetitions of the preceding matcher. The regular expression `a*` means: zero or more repetitions 
of preceding lowercase character `a`. But if it appears after a character set or class then it finds the repetitions of the whole 
character set. For example, the regular expression `[a-z]*` means: any number of lowercase letters in a row.

星号 `*` 匹配其前面的字符0次或多次。正则表达式 `a*` 表示为：重复0次或多次小写字母 `a*` ，但如果它出现字符集后，就会匹配字符集的里的所有字符。例如，正则表达式 `[a-z]*` 表示为：匹配任意小写字母。

<pre>
"[a-z]*" => T<a href="#learn-regex"><strong>he</strong></a> <a href="#learn-regex"><strong>car</strong></a> <a href="#learn-regex"><strong>parked</strong></a> <a href="#learn-regex"><strong>in</strong></a> <a href="#learn-regex"><strong>the</strong></a> <a href="#learn-regex"><strong>garage</strong></a> #21.
</pre>

[Test the regular expression](https://regex101.com/r/7m8me5/1)

The `*` symbol can be used with the meta character `.` to match any string of characters `.*`. The `*` symbol can be used with the 
whitespace character `\s` to match a string of whitespace characters. For example, the expression `\s*cat\s*` means: zero or more 
spaces, followed by lowercase character `c`, followed by lowercase character `a`, followed by lowercase character `t`, followed by 
zero or more spaces.

`*` 可以与 `.` 共用来匹配任意由 `.*` 组成的字符串。 `*` 与 空格符 `\s` 共用可以匹配任意包含空格符的字符串。例如，正则表达式 `\s*cat\s*` 表示为：0个或者多个空格符，紧跟着小写字符 `c` ， `a` ， `t` 和0个或多个空格符。

<pre>
"\s*cat\s*" => The fat<a href="#learn-regex"><strong> cat </strong></a>sat on the <a href="#learn-regex">con<strong>cat</strong>enation</a>.
</pre>

[Test the regular expression](https://regex101.com/r/gGrwuz/1)

### 2.3.2 The Plus 加号

The symbol `+` matches one or more repetitions of the preceding character. For example, the regular expression `c.+t` means: lowercase 
letter `c`, followed by any number of character, followed by the lowercase character `t`.

`+` 匹配其前面的字符至少一次或多次。例如，正则表达式 `c.+t` 表示为：小写字母 `c` 紧跟着任意长度的字符和一个字符 `t` 。

<pre>
"c.+t" => The fat <a href="#learn-regex"><strong>cat sat on the mat</strong></a>.
</pre>

[Test the regular expression](https://regex101.com/r/Dzf9Aa/1)

### 2.3.3 The Question Mark 问号

In regular expression the meta character `?` makes the preceding character optional. This symbol matches zero or one instance of 
the preceding character. For example, the regular expression `[T]?he` means: Optional the uppercase letter `T`, followed by the lowercase 
character `h`, followed by the lowercase character `e`.

在正则表达式中元字符 `?` 的出现将其前面的字符作为匹配可选条件，匹配0次或多次有其前面字符组成的字符。例如，正则表达式 `[T]?he` 表示为：匹配可选条件大写字母 `T` ，紧跟着小写字母 `h` 和 `e` 。

<pre>
"[T]he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in the garage.
</pre>

[Test the regular expression](https://regex101.com/r/cIg9zm/1)

<pre>
"[T]?he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in t<a href="#learn-regex"><strong>he</strong></a> garage.
</pre>

[Test the regular expression](https://regex101.com/r/kPpO2x/1)

## 2.4 Braces 大括号（花括号）

In  regular expression braces that are also called quantifiers are used to specify the number of times that a 
character or a group of characters can be repeated. For example, the regular expression `[0-9]{2,3}` means: Match at least 2 digits but not more than 3 (
characters in the range of 0 to 9).

在正则表达式中的大括号通常用于指定一个字符或一组字符可以重复多少次。例如，正则表达式 `[0-9]{2,3}` 表示为：在0之9之间至少匹配2个数字但不超过3个数字。

<pre>
"[0-9]{2,3}" => The number was 9.<a href="#learn-regex"><strong>999</strong></a>7 but we rounded it off to <a href="#learn-regex"><strong>10</strong></a>.0.
</pre>

[Test the regular expression](https://regex101.com/r/juM86s/1)

We can leave out the second number. For example, the regular expression `[0-9]{2,}` means: Match 2 or more digits. If we also remove 
the comma the regular expression `[0-9]{2}` means: Match exactly 2 digits.

我们可以去除第二个参数。例如，正则表达式 `[0-9]{2,}` 表示为：至少匹配2个数字或更多。如果我们将逗号 `,` 去除，正则表达式 `[0-9]{2}` 将表示为： 只匹配2个数字。

<pre>
"[0-9]{2,}" => The number was 9.<a href="#learn-regex"><strong>9997</strong></a> but we rounded it off to <a href="#learn-regex"><strong>10</strong></a>.0.
</pre>

[Test the regular expression](https://regex101.com/r/Gdy4w5/1)

<pre>
"[0-9]{2}" => The number was 9.<a href="#learn-regex"><strong>99</strong></a><a href="#learn-regex"><strong>97</strong></a> but we rounded it off to <a href="#learn-regex"><strong>10</strong></a>.0.
</pre>

[Test the regular expression](https://regex101.com/r/gqajq8/1)

## 2.5 Character Group 字符组

Character group is a group of sub-patterns that is written inside Parentheses `(...)`. As we discussed before that in regular expression 
if we put a quantifier after a character than it will repeat the preceding character. But if we put quantifier after a character group then 
it repeats the whole character group. For example, the regular expression `(ab)*` matches zero or more repetitions of the character "ab".
We can also use the alternation `|` meta character inside character group. For example, the regular expression `(c|g|p)ar` means: lowercase character `c`, 
`g` or `p`, followed by character `a`, followed by character `r`.

字符组是由一组子匹配模式组成的，遵循 `(...)` 的写法。在我们讨论其在正则表达式中的应用前，如果我们将一个量词放在一个字符后面，它将匹配相应次数的字符。但如果我们将量词放在一个字符组后面，它将重复匹配整个字符组。例如，正则表达式 `(ab)*` 匹配"ab"0次或多次。我们也可以在字符组中使用或元字符 `|` 。例如，正则表达式 `(c|g|p)ar` 表示为： 匹配小写字符 `c` 或 `g` 或 `p` ，并紧跟着字符 `a` 和 `r` 。 

<pre>
"(c|g|p)ar" => The <a href="#learn-regex"><strong>car</strong></a> is <a href="#learn-regex"><strong>par</strong></a>ked in the <a href="#learn-regex"><strong>gar</strong></a>age.
</pre>

[Test the regular expression](https://regex101.com/r/tUxrBG/1)

## 2.6 Alternation 或

In regular expression Vertical bar `|` is used to define alternation. Alternation is like a condition between multiple expressions. Now, 
you may be thinking that character set and alternation works the same way. But the big difference between character set and alternation 
is that character set works on character level but alternation works on expression level. For example, the regular expression 
`(T|t)he|car` means: uppercase character `T` or lowercase `t`, followed by lowercase character `h`, followed by lowercase character `e` 
or lowercase character `c`, followed by lowercase character `a`, followed by lowercase character `r`.

在正则表达式中，垂直符号 `|` 被用作定义或语法。或就像在不同的表达式中充当一个条件。现在你可能在想字符集和或语法不是做了相同的工作吗，其实或语法与字符集最大的不同就是字符集在字符层面发挥作用，而或语法在表达式的层面上工作。例如，正则表达式 `(T|t)he|car` 表示为：大写字符 `T` 或小写字符 `t` ，紧跟着小写字符 `h` 和 `e` 或 紧跟着小写字符 `c` ， `a` 和 `r` 。

<pre>
"(T|t)he|car" => <a href="#learn-regex"><strong>The</strong></a> <a href="#learn-regex"><strong>car</strong></a> is parked in <a href="#learn-regex"><strong>the</strong></a> garage.
</pre>

[Test the regular expression](https://regex101.com/r/fBXyX0/1)

## 2.7 Escaping special character 转义特殊字符

Backslash `\` is used in regular expression to escape the next character. This allows to to specify a symbol as a matching character 
including reserved characters `{ } [ ] / \ + * . $ ^ | ?`. To use a special character as a matching character prepend `\` before it. 
For example, the regular expression `.` is used to match any character except new line. Now to match `.` in an input string the regular
expression `(f|c|m)at\.?` means: lowercase letter `f`, `c` or `m`, followed by lowercase character `a`, followed by lowercase letter 
`t`, followed by optional `.` character.

正则表达式中的反斜杠 `\` 用于转移其下一个字符，它允许指定元字符作为匹配字符，包括如下保留字符 `{ } [ ] / \ + * $ ^ | ?` 。使用方法：只需要在需要指定匹配的字符前加上 `\` 即可。例如，正则表达式 `.` 用于匹配除了换行符以外的所有字符。假设现在需要在一个输入里进行正则表达式 `(f|c|m)at\.?` 匹配，此正则表达式表示为：小写字母 `f` 或 `c` 或 `m`，紧跟着小写字符 `a` 和 `t` ，最后 `.`  作为可选条件进行匹配。

<pre>
"(f|c|m)at\.?" => The <a href="#learn-regex"><strong>fat</strong></a> <a href="#learn-regex"><strong>cat</strong></a> sat on the <a href="#learn-regex"><strong>mat.</strong></a>
</pre>

[Test the regular expression](https://regex101.com/r/DOc5Nu/1)

## 2.8 Anchors 锚

In regular expressions, to check if the matching symbol is the starting symbol or ending symbol of the input string for this purpose
we use anchors. Anchors are of two types: First type is Caret `^` that check if the matching character is the start character of the 
input and the second type is Dollar `$` that checks if matching character is the last character of the input string.

在正则表达式中，为了知道相应的匹配模式是开头匹配还是末尾匹配，我们可以使用锚。锚有两种类型：第一种类型就是插入符号 `^` 用于检查待匹配的字符串是否符合其开头的匹配模式；第二种就是美元符号 `$` 用于检查待匹配的字符串是否符合其结尾的匹配模式。

### 2.8.1 Caret 插入符

Caret `^` symbol is used to check if matching character is the first character of the input string. If we apply the following regular 
expression `^a` (if a is the starting symbol) to input string `abc` it matches `a`. But if we apply regular expression `^b` on above 
input string it does not match anything. Because in input string `abc` "b" is not the starting symbol. Let's take a look at another 
regular expression `^(T|t)he` which means: uppercase character `T` or lowercase character `t` is the start symbol of the input string, 
followed by lowercase character `h`, followed by lowercase character `e`.

插入符号 `^` 用于检查待匹配的字符串是否符合其开头的匹配模式。如果我们采用如下正则表达式 `^a` （如果 a 是字符串的开头），输入的字符串 `abc` 将匹配 `a` 。但如果我们采用如下正则表达式 `^b` ，上述的字符串将不会匹配任何字符，因为 `abc` 的开头并不是"b"。让我们继续看下一个正则表达式 `^(T|t)he` ，其表示为：大写字母 `T` 或小写字母 `t` 作为匹配的开头，并紧跟着小写字母 `h` 和 `e` 。

<pre>
"(T|t)he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in <a href="#learn-regex"><strong>the</strong></a> garage.
</pre>

[Test the regular expression](https://regex101.com/r/5ljjgB/1)

<pre>
"^(T|t)he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in the garage.
</pre>

[Test the regular expression](https://regex101.com/r/jXrKne/1)

### 2.8.2 Dollar 美元符号

Dollar `$` symbol is used to check if matching character is the last character of the input string. For example, regular expression 
`(at\.)$` means: a lowercase character `a`, followed by lowercase character `t`, followed by a `.` character and the matcher 
must be end of the string.

美元符号 `$` 用于检查匹配的字符串的结尾是否匹配匹配模式。例如，正则表达式 `(at\.)$` 表示为：小写字母 `a` ，紧跟着小写字母 `t` 和 `.` ，且匹配的字符串必要要以次为结尾。

<pre>
"(at\.)" => The fat c<a href="#learn-regex"><strong>at.</strong></a> s<a href="#learn-regex"><strong>at.</strong></a> on the m<a href="#learn-regex"><strong>at.</strong></a>
</pre>

[Test the regular expression](https://regex101.com/r/y4Au4D/1)

<pre>
"(at\.)$" => The fat cat. sat. on the m<a href="#learn-regex"><strong>at.</strong></a>
</pre>

[Test the regular expression](https://regex101.com/r/t0AkOd/1)

##  3. Shorthand Character Sets

Regular expression provides shorthands for the commonly used character sets, which offer convenient shorthands for commonly used 
regular expressions. The shorthand character sets are as follows:

|Shorthand|Description|
|:----:|----|
|.|Any character except new line|
|\w|Matches alphanumeric characters: `[a-zA-Z0-9_]`|
|\W|Matches non-alphanumeric characters: `[^\w]`|
|\d|Matches digit: `[0-9]`|
|\D|Matches non-digit: `[^\d]`|
|\s|Matches whitespace character: `[\t\n\f\r\p{Z}]`|
|\S|Matches non-whitespace character: `[^\s]`|

## 4. Lookaround

Lookbehind and lookahead sometimes known as lookaround are specific type of ***non-capturing group*** (Use to match the pattern but not 
included in matching list). Lookaheads are used when we have the condition that this pattern is preceded or followed by another certain 
pattern. For example, we want to get all numbers that are preceded by `$` character from the following input string `$4.44 and $10.88`. 
We will use following regular expression `(?<=\$)[0-9\.]*` which means: get all the numbers which contains `.` character and preceded 
by `$` character. Following are the lookarounds that are used in regular expressions:

|Symbol|Description|
|:----:|----|
|?=|Positive Lookahead|
|?!|Negative Lookahead|
|?<=|Positive Lookbehind|
|?<!|Negative Lookbehind|

### 4.1 Positive Lookahead

The positive lookahead asserts that the first part of the expression must be followed by the lookahead expression. The returned match
only contains the text that is matched by the first part of the expression. To define a positive lookahead, parentheses are used. Within 
those parentheses, a question mark with equal sign is used like this: `(?=...)`. Lookahead expression is written after the equal sign inside 
parentheses. For example, the regular expression `(T|t)he(?=\sfat)` means: optionally match lowercase letter `t` or uppercase letter `T`, 
followed by letter `h`, followed by letter `e`. In parentheses we define positive lookahead which tells regular expression engine to match
`The` or `the` which are followed by the word `fat`. 

<pre>
"(T|t)he(?=\sfat)" => <a href="#learn-regex"><strong>The</strong></a> fat cat sat on the mat.
</pre>

[Test the regular expression](https://regex101.com/r/apqJZq/1)

### 4.2 Negative Lookahead

Negative lookahead is used when we need to get all matches from input string that are not followed by a pattern. Negative lookahead 
defined same as we define positive lookahead but the only difference is instead of equal `=` character we use negation `!` character 
i.e. `(?!...)`. Let's take a look at the following regular expression `(T|t)he(?!\sfat)` which means: get all `The` or `the` words from 
input string that are not followed by the word `fat` precedes by a space character.

<pre>
"(T|t)he(?!\sfat)" => The fat cat sat on <a href="#learn-regex"><strong>the</strong></a> mat.
</pre>

[Test the regular expression](https://regex101.com/r/sswCvQ/1)

### 4.3 Positive Lookbehind

Positive lookbehind is used to get all the matches that are preceded by a specific pattern. Positive lookbehind is denoted by 
`(?<=...)`. For example, the regular expression `(?<=(T|t)he\s)(fat|mat)` means: get all `fat` or `mat` words from input string that 
are after the word `The` or `the`.

<pre>
"(?<=(T|t)he\s)(fat|mat)" => The <a href="#learn-regex"><strong>fat</strong></a> cat sat on the <a href="#learn-regex"><strong>mat</strong></a>.
</pre>

[Test the regular expression](https://regex101.com/r/TZ8DOX/1/)

### 4.4 Negative Lookbehind

Negative lookbehind is used to get all the matches that are not preceded by a specific pattern. Negative lookbehind is denoted by 
`(?<!...)`. For example, the regular expression `(?&lt;!(T|t)he\s)(cat)` means: get all `cat` words from input string that 
are not after the word `The` or `the`.

<pre>
"(?&lt;!(T|t)he\s)(cat)" => The cat sat on <a href="#learn-regex"><strong>cat</strong></a>.
</pre>

[Test the regular expression](https://regex101.com/r/gleYg9/1)

## 5. Flags

Flags are also called modifiers because they modify the output of a regular expression. These flags can be used in any order or 
combination, and are an integral part of the RegExp.

|Flag|Description|
|:----:|----|
|i|Case insensitive: Sets matching to be case-insensitive.|
|g|Global Search: Search for a pattern throughout the input string.|
|m|Multiline: Anchor meta character works on each line.|

### 5.1 Case Insensitive

The `i` modifier is used to perform case-insensitive matching. For example, the regular expression `/The/gi` means: uppercase letter 
`T`, followed by lowercase character `h`, followed by character `e`. And at the end of regular expression the `i` flag tells the 
regular expression engine to ignore the case. As you can see we also provided `g` flag because we want to search for the pattern in 
the whole input string.

<pre>
"The" => <a href="#learn-regex"><strong>The</strong></a> fat cat sat on the mat.
</pre>

[Test the regular expression](https://regex101.com/r/dpQyf9/1)

<pre>
"/The/gi" => <a href="#learn-regex"><strong>The</strong></a> fat cat sat on <a href="#learn-regex"><strong>the</strong></a> mat.
</pre>

[Test the regular expression](https://regex101.com/r/ahfiuh/1)

### 5.2 Global search

The `g` modifier is used to perform a global match (find all matches rather than stopping after the first match). For example, the 
regular expression`/.(at)/g` means: any character except new line, followed by lowercase character `a`, followed by lowercase 
character `t`. Because we provided `g` flag at the end of the regular expression now it will find every matches from whole input 
string.

<pre>
"/.(at)/" => The <a href="#learn-regex"><strong>fat</strong></a> cat sat on the mat.
</pre>

[Test the regular expression](https://regex101.com/r/jnk6gM/1)

<pre>
"/.(at)/g" => The <a href="#learn-regex"><strong>fat</strong></a> <a href="#learn-regex"><strong>cat</strong></a> <a href="#learn-regex"><strong>sat</strong></a> on the <a href="#learn-regex"><strong>mat</strong></a>.
</pre>

[Test the regular expression](https://regex101.com/r/dO1nef/1)

### 5.3 Multiline

The `m` modifier is used to perform a multi-line match. As we discussed earlier anchors `(^, $)` are used to check if pattern is 
the beginning of the input or end of the input string. But if we want that anchors works on each line we use `m` flag. For example, the
regular expression `/at(.)?$/gm` means: lowercase character `a`, followed by lowercase character `t`, optionally anything except new 
line. And because of `m` flag now regular expression engine matches pattern at the end of each line in a string.

<pre>
"/.at(.)?$/" => The fat
                cat sat
                on the <a href="#learn-regex"><strong>mat.</strong></a>
</pre>

[Test the regular expression](https://regex101.com/r/hoGMkP/1)

<pre>
"/.at(.)?$/gm" => The <a href="#learn-regex"><strong>fat</strong></a>
                  cat <a href="#learn-regex"><strong>sat</strong></a>
                  on the <a href="#learn-regex"><strong>mat.</strong></a>
</pre>

[Test the regular expression](https://regex101.com/r/E88WE2/1)

## Bonus

* *Positive Integers*: `^\d+$`
* *Negative Integers*: `^-\d+$`
* *US Phone Number*: `^+?[\d\s]{3,}$`
* *US Phone with code*: `^+?[\d\s]+(?[\d\s]{10,}$`
* *Integers*: `^-?\d+$`
* *Username*: `^[\w\d_.]{4,16}$`
* *Alpha-numeric characters*: `^[a-zA-Z0-9]*$`
* *Alpha-numeric characters with spaces*: `^[a-zA-Z0-9 ]*$`
* *Password*: `^(?=^.{6,}$)((?=.*[A-Za-z0-9])(?=.*[A-Z])(?=.*[a-z]))^.*$`
* *email*: `^([a-zA-Z0-9._%-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4})*$`
* *IPv4 address*: `^((?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?))*$`
* *Lowercase letters only*: `^([a-z])*$`
* *Uppercase letters only*: `^([A-Z])*$`
* *URL*: `^(((http|https|ftp):\/\/)?([[a-zA-Z0-9]\-\.])+(\.)([[a-zA-Z0-9]]){2,4}([[a-zA-Z0-9]\/+=%&_\.~?\-]*))*$`
* *VISA credit card numbers*: `^(4[0-9]{12}(?:[0-9]{3})?)*$`
* *Date (MM/DD/YYYY)*: `^(0?[1-9]|1[012])[- /.](0?[1-9]|[12][0-9]|3[01])[- /.](19|20)?[0-9]{2}$`
* *Date (YYYY/MM/DD)*: `^(19|20)?[0-9]{2}[- /.](0?[1-9]|1[012])[- /.](0?[1-9]|[12][0-9]|3[01])$`
* *MasterCard credit card numbers*: `^(5[1-5][0-9]{14})*$`

## Contribution

* Report issues
* Open pull request with improvements
* Spread the word 
* Reach out to me directly at ziishaned@gmail.com or [![Twitter URL](https://img.shields.io/twitter/url/https/twitter.com/ziishaned.svg?style=social&label=Follow%20%40ziishaned)](https://twitter.com/ziishaned)

## License

MIT © [Zeeshan Ahmed](mailto:ziishaned@gmail.com)
