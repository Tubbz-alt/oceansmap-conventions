# OceansMap Conventions

This repository is used to guide and maintain a set of conventions for
developing OceansMap in a distributed environment.

Copyright 2017 RPS Group Plc
See LICENSE for details

<style>
.tip {
  background-color: #fffbd9;
  padding: 6px 8px 6px 10px;
  border-left: 6px solid #ffef70;
}

.note {
  background-color: #e5ecf9;
  padding: 6px 8px 6px 10px;
  border-left: 6px solid #36c;
}

</style>

This document is a modified version of Google's Javascript style guide. The
structure and language of the document is very similar to Google's but
modifications have been made where deemed suitable by the author(s). Google, in
no way, endorses or supports RPS or OceansMap.

The original Google Style guidelines can be found
[here](https://google.github.io/styleguide/jsguide.html)

# Table of Contents

1. [Introduction](#1-introduction)
  
  1. [Terminology Notes](#11-terminology-notes)

  2. [Guide Notes](#12-guide-notes)

2. [Source file basics](#2-source-file-basics)
  
  1. [File Name](#21-file-name)


# 1. Introduction

This document serves as the coding standards for source code in the JavaScript
programming language. 

Like other programming style guides, the issues covered span not only aesthetic
issues of formatting, but other types of conventions or coding standards as
well. However, this document focuses primarily on the hard-and-fast rules that
we follow universally, and avoids giving advice that isn't clearly enforceable
(whether by human or tool).

## 1.1 Terminology Notes

In this document, unless otherwise clarified:

1. The term comment always refers to implementation comments. We do not use the
   phrase documentation comments, instead using the common term "JSDoc" for
   both human-readable text and machine-readable annotations within `/** … */`.

2. This Style Guide uses [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt)
   terminology when using the phrases must, must not, should, should not, and
   may. The terms prefer and avoid correspond to should and should not,
   respectively. Imperative and declarative statements are prescriptive and
   correspond to must.

Other "terminology notes" will appear occasionally throughout the document.

## 1.2 Guide notes

Example code in this document is **non-normative**. That is, while the examples
follow OceansMap conventions, they may not illustrate the only stylish way to
represent the code. Optional formatting choices made in examples must not be
enforced as rules.

# 2. Source file basics

## 2.1 File Name

File names for classes should be
[PascalCase](https://en.wikipedia.org/wiki/PascalCase). The file name should
match the class name. For example, consider a file named `ExampleModel.js`:

```javascript
var ExampleModel = Backbone.Model.extend({
});

var ExampleCollection = Backbone.Collection.extend({
});
```

is legal. However, a filename of `example_model.js` would be illegal.

File names for modules that don't contain class definitions should be
`snake_case`.

## 2.2 File encoding: UTF-8

Source files are encoded in UTF-8


## 2.3 Special Characters

### 2.3.1 Whitespace characters

Aside from the line terminator sequence, the ASCII horizontal space character
(0x20) is the only whitespace character that appears anywhere in a source file.
This implies that

1. All other whitespace characters in string literals are escaped, and

2. Tab characters are not used for indentation.

### 2.3.2 Special escape sequances

For any character that has a special escape sequence (`\'`, `\"`, `\\`, `\b`,
`\f`, `\n`, `\r`, `\t`, `\v`), that sequence is used rather than the
corresponding numeric escape (e.g `\x0a`, `\u000a`, or `\u{a}`). Legacy octal
escapes are never used.

### 2.3.3 Non-ASCII characters

For the remaining non-ASCII characters, either the actual Unicode character
(e.g. ∞) or the equivalent hex or Unicode escape (e.g. `\u221e`) is used,
depending only on which makes the code **easier to read and understand**.

<p class="tip">
Tip: In the Unicode escape case, and occasionally even when the actual Unicode
characters are used, an explanatory comment can be very helpful.
</p>

| Example                                          | Discussion                                                                |
|--------------------------------------------------|---------------------------------------------------------------------------|
| `var units = 'μs';`                              | Best: perfectly clear even without a comment.                             |
| `var units = '\u03bcs'; // 'μs'`                 | Allowed, bu there's no reason to do this.                                 |
| `var units = '\u03bcs'; // Greek letter mu, 's'` | Allowed, but awkward and prone to mistakes.                               |
| `var  units = '\u03bcs'; `                       | Poor: the reader has no idea what this is.                                |
| `return '\ufeff' + content; // byte order mark`  | Good: use escapes for non-printable characters, and comment if necessary. |


# 3. Source file structure

A source file consists of, **in order**:

1. JSDoc string container
2. Filename
3. Description of the contents of the file
4. Any dependencies needed by the file
5. The file's implementation

**Exactly one blank lines** separate each section that is present, except the file's implementation which is preceeded **by exactly two lines**.

Example:

```javascript
/*
 * oceansmap/static/js/models/CatalogModel.js
 * 
 * Model definitition for a Catalog Model. This model represents a data
 * structure for rendering content about catalog records.
 *
 * Requires:
 *   - oceansmap/static/js/models/MappedInfoModel.js
 *   - oceansmap/static/js/models/ParameterModel.js
 *   - oceansmap/static.js/models/AlertModel.js
 */
```


# 4. Formatting

## 4.1 Braces

### 4.1.1 Braces are used for all control structures

Braces are required for all control structures (i.e. `if`, `else`, `for`, `do`,
`while`, as well as any others), even if the body contains only a single
statement. The first statement of a non-empty block must begin on its own line:

illegal:

```
// Illegal
if (someVeryLongCondition()) 
  doSomething();

// Very illegal
for (var i = 0; i < foo.length; i++) bar(foo[i]);
```

### 4.1.2 Nonempty blocks: K&R style

Braces follow the Kernighan and Ritchie style ("[Egyption brackets](https://blog.codinghorror.com/new-programming-jargon/)")
for _nonempty_ blocks and block-like constructs.

  - No line break before the opening brace
  - Line break after the opening brace.
  - Line break before the closing brace.
  - Line break after the closing brace _if_ that brace terminates a statement
    or the body of a function or class statement, or a class method.
    Specifically, there is _no_ line break after the brace if it is followed by
    `else`, `catch`, `while`, or a comma, semicolon, or right-parenthesis.


Example:

```javascript
var InnerClass = function() {};

/**
 * Example Method
 * @param {number} foo
 */
InnerClass.prototype.method = function(foo) {
  if (condition(foo)) {
    try {
      // Note: this might fail.
      something();
    } catch (err) {
      recover();
    }
  }
};
```

### 4.1.3 Empty blocks: may be concise

An empty block or block-like construct may be closed immediately after it is
opened, with no characters, space, or line break in between (i.e. `{}`),
**unless** it is a part of a *multi-block statement* (one that directly
contains multiple blocks: `if`/`else` or `try`/`catch`/`finally`).

Example:

```javascript
function doNothing() {}
```

Illegal:

```javascript
if (condition) {
  // ...
} else if (otherCondition) {} else {
  // ...
}

try {
  // ...
} catch (e) {}
```

## 4.2 Block indentation: +2 spaces

Each time a new block or block-like construct is opened, the indent increases
by two spaces. When the block ends, the indent returns to the previous indent
level. The indent level applies to both code and comments throughout the block.

### 4.2.1 Array literals: optionally "block-like"

Any array literal may optionally be formatted as if it were a "block-like construct." For example, the following are all valid (**not** an exhaustive list):

```javascript
var a = [
  0, 1, 2,
];

var b =
    [0, 1, 2];
    const c = [0, 1, 2];

someMethod(foo, [
  0,
  1,
  2,
], bar);
```

### 4.2.2 Object literals: optionally "block-like"


Any object literal may optionally be formatted as if it were a “block-like
construct.” The same examples apply as 4.2.1 Array literals: optionally
block-like. For example, the following are all valid (**not** an exhaustive list):

```
var a = {
  a: 0, b: 1
};

var b =
    {a: 0, b: 1};

var c = {a: 0, b: 1};

someMethod(foo, {
  a: 0,
  b: 1,
}, bar);

```

### 4.2.3 Class Literals

We do not currently support ECMA Script 6 syntax for class literals due to
[browser incompatibilities](https://kangax.github.io/compat-table/es6/). 

### 4.2.4 Function expressions

When declaring an anonymous function in the list of arguments for a function
call, the body of the function is indented two spaces more than the preceding
indentation depth.

Example:
```javascript

prefix.something.reallyLongFunctionName('whatever', function(a1, a2)  {
  // Indent the function body +2 relative to indentation depth
  // of the 'prefix' statement one line above.
  if (a1.equals(a2)) {
    someOtherLongFunctionName(a1);
  } else {
    andNowForSomethingCompletelyDifferent(a2.parrot);
  }
});

some.reallyLongFunctionCall(arg1, arg2, arg3)
    .thatsWrapped()
    .then(function(result) {
      // Indent the function body +2 relative to the indentation depth
      // of the '.then()' call.
      if (result) {
        result.use();
      }
    });
```

### 4.2.5 Switch statements

As with any other block, the contents of a switch block are indented +2.

After a switch label, a newline appears, and the indentation level is increased
+2, exactly as if a block were being opened. An explicit block may be used if
required by lexical scoping. The following switch label returns to the previous
indentation level, as if a block had been closed.

A blank line is optional between a `break` and the following case.

Example:

```javascript
switch (animal) {
  case Animal.BANDERSNATCH:
    handleBandersnatch();
    break;

  case Animal.JABBERWOCK:
    handleJabberwock();
    break;

  default:
    throw new Error('Unknown animal');
}
```

## 4.3 Statements

### 4.3.1 One statement per line

Each statement is followed by a line-break.

### 4.3.2 Semicolons are required

Every statement must be terminated with a semicolon. Relying on automatic semicolon insertion is forbidden.

## 4.4 Column Limit

To be discussed and determined later. For now try to keep statements under 80
except where it's not impossible (for example a long URL) or when doing so
would reduce code readability.

## 4.5 Line-wrapping

**Terminology note:** *line-wrapping* is defined as breaking a single
expression into multiple lines.

There is no comprehensive, deterministic formula showing *exactly* how to
line-wrap in every situation. Very often there are several valid ways to
line-wrap the same piece of code.

<p class="note">
Note: While the typical reason for line-wrapping is to avoid overflowing the
column limit, even code that would in fact fit within the column limit may be
line-wrapped at the author's discretion.
</p>

<p class="tip">
Tip: Extracting a method or local variable may solve the problem without the need to line-wrap.
</p>

### 4.5.1 Where to break

The prime directive of line-wrapping is: prefer to break at a **higher syntactic level**. Also:

1. When a line is broken at an operator the break comes after the symbol. (Note
   that this is not the same practice used for Java)
2. A method or constructor name stays attached to the open parenthesis (`(`)
   that follows it.
3. A comma (`,`) stays attached to the token that precedes it

Preferred:

```javascript
this.foo =
    foo(
        firstArg,
        1 + someLongFunctionName());
```

Discouraged:

```javascript
this.foo = foo(firstArg, 1 +
    someLongFunctionName());
```

In the preceding example, the syntactic levels from highest to lowest are as
follows: assignment, outer function call, parameters, plus, inner function
call.

<p class="note">
Note: The primary goal for line wrapping is to have clear code, not necessarily code that fits in the smallest number of lines.
</p>

### 4.5.2 Indent continuation lines at least +4 spaces

When line-wrapping, each line after the first (each *continuation line*) is indented at least +4 from the original line, unless it falls under the rules of block indentation.

When there are multiple continuation lines, indentation may be varied beyond +4
as appropriate. In general, continuation lines at a deeper syntactic level are
indented by larger multiples of 4, and two lines use the same indentation level
if and only if they begin with syntactically parallel elements.


## 4.6 Whitespace

### 4.6.1 Vertical whitespace

A single blank line appears:

1. Between consecutive methods in a class or object literal

  1. Exception: A blank line between two consecutive properties definitions in
     an object lietral (with no other code between them)  is optional. Such
     blank lines are used as needed to create *logical groupings* of fields.

2. Within method bodies, sparingly to create *logical groupings* of statements.
   Blank lines at the start or end of a function body are not allowed.

3. *Optionally* before the first or after the last method in a class or object
   literal (neither encouraged nor discouraged).

4. As required by other sections of this document.

*Multiple* consecutive line blanks are permitted, but never required.


### 4.6.2 Horizontal Whitespace

Use of horizontal whitespace depends on location, and falls into three broad
categories: *leading* (at the start of a line), *trailing* (at the end of a line),
and *internal*. Leading whitespace (i.e., indentation) is addressed elsewhere.
**Trailing whitespace is forbidden**.

1. Separating any reserved word (such as `if`, `for`, or `catch`) from an open
   parenthesis (`(`) that follows it on that line.

2. Separating any reserved word (such as `else` or `catch`) from a closing
   curly brace (`}`) that precedes it on that line.

3. Before any open curly brance (`{`), with two exceptions:

   1. Before an object literal that is the first argument of a function or the first element in an array literal (e.g. `foo({a: [{c: d}]})`)

4. On both sides of any binary or ternary operator.

5. After a comma (`,`) or semicolon (`;`). Note that spaces are *never* allowed before these characters.
6. After the colon (`:`) in an object literal.
7. On both sides of the double slash (`//`) that begins an end-of-line comment. Here, multiple spaces are allowed, but not required.
8. After an open-JSDoc comment character and on both sides of the close
   characters (e.g. for short-form type declarations or casts: `this.foo = /** @type {number} */ (bar);` 
   or `function(/** string */ foo) {`).

### 4.6.3 Rectangle Rule

All code should follow the Rectangle Rule.

<p class="tip">
  <i>
    When a source file is formatted, each subtree gets its own bounding
    rectangle, containing all of that subtree's text and none of any other
    subtree's
  </i>
</p>

What does this mean? Take the well formatted example below, and draw a
rectangle around just the subexpression `x / currentEstimate`:

```javascript
currentEstimate = 
    (currentEstimate + x / currentEstimate)
        / 2.0f;
```

This is possible—good! But in the badly formatted example, there is no
rectangle containing just that subexpression and nothing more—bad!

```javascript
currentEstimate = (currentEstimate + x
        / currentEstimate) / 2.0f;
```

In the well formatted example, every subtree has its own rectangle; for
instance, the right-hand side (RHS) of the assignment has its own rectangle in
the well formatted example, but not in the other. This promotes readability by
exposing program structure in the physical layout; the RHS is in just one
place, not partly in one place and partly another.

### 4.6.4 Horizontal alignment: discouraged

**Terminology Note:** *Horizontal alignment* is the practice of adding a
variable number of additional spaces in your code with the goal of making
certain tokens appear directly below certain other tokens on previous lines.

This practice is permitted, but it is **generally discouraged**. It is not even
required to *maintain* horizontal alignment in places where it was already
used.

Here is an example without alignment, followed by one with alignment. Both are
allowed, but the latter is discouraged.

```javascript
{
  tiny: 42, // this is great
  longer: 435, // this too
};

{
  tiny:   42,  // permitted, but future edits
  longer: 435, // may leave it unaligned
};
```

<p class="tip">
Tip: Alignment can aid readability, but it creates problems for future
maintenance. Consider a future change that needs to touch just one line. This
change may leave the formerly-pleasing formatting mangled, and that is allowed.
More often it prompts the coder (perhaps you) to adjust whitespace on nearby
lines as well, possibly triggering a cascading series of reformattings. That
one-line change now has a blast radius. This can at worst result in pointless
busywork, but at best it still corrupts version history information, slows down
reviewers and exacerbates merge conflicts.
</p>

### 4.6.5 Function arguments

Prefer to put all function arguments on the same line as the function name. If
doing so would exceed the 80-column limit, the arguments must be line-wrapped
in a readable way. To save space, you may wrap as close to 80 as possible, or
put each argument on its own line to enhance readability. Indentation should be
four spaces. Aligning to the parenthesis is allowed, but discouraged. Below are
the most common patterns for argument wrapping:

```javascript
// Arguments start on a new line, indented four spaces. Preferred when the
// arguments don't fit on the same line with the function name (or the keyword
// "function") but fit entirely on the second line. Works with very long
// function names, survives renaming without reindenting, low on space.
doSomething(
    descriptiveArgumentOne, descriptiveArgumentTwo, descriptiveArgumentThree) {
  // …
}

// If the argument list is longer, wrap at 80. Uses less vertical space,
// but violates the rectangle rule and is thus not recommended.
doSomething(veryDescriptiveArgumentNumberOne, veryDescriptiveArgumentTwo,
    tableModelEventHandlerProxy, artichokeDescriptorAdapterIterator) {
  // …
}

// Four-space, one argument per line.  Works with long function names,
// survives renaming, and emphasizes each argument.
doSomething(
    veryDescriptiveArgumentNumberOne,
    veryDescriptiveArgumentTwo,
    tableModelEventHandlerProxy,
    artichokeDescriptorAdapterIterator) {
  // …
}
```

## 4.7 Grouping parentheses: recommended

Optional grouping parentheses are omitted only when the author and reviewer
agree that there is no reasonable chance that the code will be misinterpreted
without them, nor would they have made the code easier to read. It is *not*
reasonable to assume that every reader has the entire operator precedence table
memorized.

Do not use unnecessary parentheses around the entire expression following
`delete`, `typeof`, `void`, `return`, `throw`, `case`, `in`, or `of`.

Parentheses are required for type casts: `/** @type {!Foo} */ (foo)`.

## 4.8 Comments

This section addresses *implementation comments*. JSDoc is addressed separately.


### 4.8.1 Block comment style

Block comments are indented at the same level as the surrounding code. They may
be in `/* … */` or `//`-style. For multi-line `/* … */` comments, subsequent lines
must start with `*` aligned with the `*` on the previous line, to make comments
obvious with no extra context. “Parameter name” comments should appear after
values whenever the value and method name do not sufficiently convey the
meaning.


```javascript
/*
 * This is
 * okay.
 */

// And so
// is this.

/* This is fine, too. */

someFunction(obviousParam, true /* shouldRender */, 'hello' /* name */);
```

Comments are not enclosed in boxes drawn with asterisks or other characters.

Do not use JSDoc (`/** … */`) for any of the above implementation comments.

```javascript
TODO(username): comment
TODO(b/buganizer_id): comment
```

```javascript
TODO(tashana): Remove this code after the UrlTable2 has been checked in.
TODO(b/6002235): remove the "Last visitors" feature
```

# 5. Language Features

# 6. Naming

# 7. JSDoc

# 8. Policies

# 9. Appendices

