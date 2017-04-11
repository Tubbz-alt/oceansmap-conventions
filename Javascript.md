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

    2. [File encoding: UTF-8](#22-file-encoding-utf-8)
    3. [Special Characters](#23-special-characters)

3. [Source file structure](#3-source-file-structure)

4. [Formatting](#4-formatting)

    1. [Braces](#41-braces)
    2. [Block indentation: +2 spaces](#42-block-indentation-2-spaces)
    3. [Statements](#43-statements)
    4. [Column Limit](#44-column-limit)
    5. [Line-wrapping](#45-line-wrapping)
    6. [Whitespace](#46-whitespace)
    7. [Grouping parentheses: recommended](#47-grouping-parentheses-recommended)
    8. [Comments](#48-comments)

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

## 5.1 Local variable declarations

### 5.1.1 Use of `const` and `let`

We do not currently support ECMA Script 6 syntax for class literals due to
[browser incompatibilities](https://kangax.github.io/compat-table/es6/). 

### 5.1.2 One variable per declaration

Every local variable declaration declares only one variable: declarations such as `let a = 1, b = 2;` are not used.

### 5.1.3 Declared when needed, initialized as soon as possible

Local variables are **not** habitually declared at the start of their
containing block or block-like construct. Instead, local variables are declared
close to the point they are first used (within reason), to minimize their
scope.

### 5.1.4 Declare types as needed

JSDoc type annotations may be added either on the line above the declaration, or else inline before the variable name.

Example:

```javascript
const /** !Array<number> */ data = [];

/** @type {!Array<number>} */
const data = [];
```

<p class="tip">
Tip: There are many cases where the compiler can infer a templatized type but
not its parameters. This is particularly the case when the initializing literal
or constructor call does not include any values of the template parameter type
(e.g., empty arrays, objects, `Map`s, or `Set`s), or if the variable is modified in
a closure. Local variable type annotations are particularly helpful in these
cases since otherwise the compiler will infer the template parameter as
unknown.
</p>

## 5.2 Array literals

### 5.2.1 Use trailing commas

Include a trailing comma whenever there is a line break between the final element and the closing bracket.

Example:

```javascript
var values = [
  'first value',
  'second value',
];
```

### 5.2.2 Do not use the variadic `Array` constructor

The constructor is error-prone if arguments are added or removed. Use a literal instead.

Illegal:

```javascript
var a1 = new Array(x1, x2, x3);
var a2 = new Array(x1, x2);
var a3 = new Array(x1);
var a4 = new Array();
```

This works as expected except for the third case: if `x1` is a whole number
then `a3` is an array of size `x1` where all elements are `undefined`. If `x1`
is any other number, then an exception will be thrown, and if it is anything
else then it will be a single-element array.

Instead, write

```javascript
var a1 = [x1, x2, x3];
var a2 = [x1, x2];
var a3 = [x1];
var a4 = [];
```

Explicitly allocating an array of a given length using `new Array(length)` is allowed when appropriate.

### 5.2.3 Non-numeric properties

Do not define or use non-numeric properties on an array (other than `length`).
Use a `Map` (or `Object`) instead.

### 5.2.4 Dstructuring

We do not currently support ECMA Script 6 syntax for class literals due to
[browser incompatibilities](https://kangax.github.io/compat-table/es6/). 


### 5.2.5 Spread operator

We do not currently support ECMA Script 6 syntax for class literals due to
[browser incompatibilities](https://kangax.github.io/compat-table/es6/). 


## 5.3 Object literals

### 5.3.1 Use trailing commas

Include a trailing comma whenever there is a line break between the final property and the closing brace.

### 5.3.2 Do not use the `Object` constructor

While `Object` does not have the same problems as `Array`, it is still disallowed for consistency. Use an object literal (`{}` or `{a: 0, b: 1, c: 2}`) instead.

### 5.3.3 Do not mix quoted and unquoted keys

Object literals may represent either structs (with unquoted keys and/or symbols) or dicts (with quoted and/or computed keys). Do not mix these key types in a single object literal.

Illegal:

```javascript
{
  a: 42, // struct-style unquoted key
  'b': 43, // dict-style quoted key
}
```

### 5.3.4 Computed property names

Computed property names (e.g. `{['key' + foo()]: 42}`) are allowed, and are
considered dict-style (quoted) keys (i.e., must not be mixed with non-quoted
keys) unless the computed property is a symbol (e.g., `[Symbol.iterator]`). Enum
values may also be used for computed keys, but should not be mixed with
non-enum keys in the same literal.

### 5.3.5 Method shorthand

We do not currently support ECMA Script 6 syntax for class literals due to
[browser incompatibilities](https://kangax.github.io/compat-table/es6/). 

### 5.3.6 Shorthand properties

We do not currently support ECMA Script 6 syntax for class literals due to
[browser incompatibilities](https://kangax.github.io/compat-table/es6/). 

### 5.3.7 Destructuring

We do not currently support ECMA Script 6 syntax for class literals due to
[browser incompatibilities](https://kangax.github.io/compat-table/es6/). 

### 5.3.8 Enums

Enumerations are defined by adding the `@enum` annotation to an object literal.
Additional properties may not be added to an enum after it is defined. Enums
must be constant, and all enum values must be deeply immutable.

```javascript
/**
 * Supported temperature scales.
 * @enum {string}
 */
var TemperatureScale = {
  CELSIUS: 'celsius',
  FAHRENHEIT: 'fahrenheit',
};

/**
 * An enum with two options.
 * @enum {number}
 */
var Option = {
  /** The option used shall have been the first. */
  FIRST_OPTION: 1,
  /** The second among two options. */
  SECOND_OPTION: 2,
};
```

## 5.4 Classes

TBD

## 5.5 Functions

### 5.5.1 Top-level functions

Exported functions may be declared locally and exported separately. Non-exported functions are encouraged and should not be declared @private.

Examples:

```javascript
/** @return {number} */
function helperFunction() {
  return 42;
}
/** @return {number} */
function exportedFunction() {
  return helperFunction() * 2;
}
/**
 * @param {string} arg
 * @return {number}
 */
function anotherExportedFunction(arg) {
  return helperFunction() / arg.length;
}
```

### 5.5.2 Nested functions and closures

Functions may contain nested function definitions. If it is useful to go give teh function a name, it should be assigned to a local `var`.

### 5.5.3 Arrow functions

We do not currently support ECMA Script 6 syntax for class literals due to
[browser incompatibilities](https://kangax.github.io/compat-table/es6/). 

### 5.5.4 Generators

We do not currently support ECMA Script 6 syntax for class literals due to
[browser incompatibilities](https://kangax.github.io/compat-table/es6/). 

### 5.5.5 Parameters

Function parameters must be typed with JSDoc annotations in the JSDoc preceding
the function’s definition, except in the case of same-signature `@overrides`,
where all types are omitted.

For anonymous functions (unnamed function expressions), parameter
types may be specified inline, immediately before the parameter name. This is
not allowed for other functions, including class methods and those that are
assigned to variables or properties, in which case the parameter and/or return
type annotations must be specified on the field, variable, or method.

Illegal:

```javascript
var func = function(/** number */ foo) {
  return 2 * foo;
});
```

Better:

```javscript
/**
 * @param {number} foo
 */
var func = function(foo) {
  return 2 * foo;
});
```

### 5.5.5.1 Default Parameters

We do not currently support ECMA Script 6 syntax for class literals due to
[browser incompatibilities](https://kangax.github.io/compat-table/es6/). 

#### 5.5.5.2 Rest parameters

We do not currently support ECMA Script 6 syntax for class literals due to
[browser incompatibilities](https://kangax.github.io/compat-table/es6/). 

### 5.5.6 Retruns

Function return types must be specified in the JSDoc directly above the
function definition, except in the case of same-signature `@override`s where
all types are omitted.

### 5.5.7 Generics

TBD

### 5.5.8 Spread operator

We do not currently support ECMA Script 6 syntax for class literals due to
[browser incompatibilities](https://kangax.github.io/compat-table/es6/). 

## 5.6 String literals

### 5.6.1 Use single quotes

Ordinary string literals are delimited with single quotes (`'`), rather than double quotes (`"`).

<p class="tip">
  Tip: if a string contains a single quote character, consider using a template string to avoid having to escape the quote.
</p>

Ordinary string literals may not span multiple lines.


### 5.6.2 Template strings

We do not currently support ECMA Script 6 syntax for class literals due to
[browser incompatibilities](https://kangax.github.io/compat-table/es6/). 

### 5.6.3 No line continuations

Do not use *line continuations* (that is, ending a line inside a string literal
with a backslash) in either ordinary or template string literals. Even though
ES5 allows this, it can lead to tricky errors if any trailing whitespace comes
after the slash, and is less obvious to readers.

Illegal:
```javascript
var longString = 'This is a very long string that far exceeds the 80 \
    column limit. It unfortunately contains long stretches of spaces due \
    to how the continued lines are indented.';
```

Instead, write:

```javascript
var longString = 'This is a very long string that far exceeds the 80 ' +
    'column limit. It does not contains long stretches of spaces since ' +
    'the concatenated strings are cleaner.';
```

## 5.7 Number literals

Numbers may be specified in decimal, hex, octal, or binary. Use exactly `0x`,
`0o`, and `0b` prefixes, with lowercase letters, for hex, octal, and binary,
respectively. Never include a leading zero unless it is immediately followed by
`x`, `o`, or `b`.

### 5.8 Control structures

### 5.8.1 For loops

The only for loop supported, due to browser support, is the classic ES5 for loop.

```javscript

for(var i = 0; i < items.length; i++) {
  var item = items[i];
  // ...
}
```

### 5.8.2 Exceptions

Exceptions are an important part of the language and should be used whenever
exceptional cases occur. Always throw `Error`s or subclasses of `Error`: never
throw string literals or other objects. Always use new when constructing an
`Error`.

Custom exceptions provide a great way to convey additional error information
from functions. They should be defined and used whenever the native `Error`
type is insufficient.

Prefer throwing exceptions over ad-hoc error-handling approaches (such as
passing an error container reference type, or returning an object with an error
property).

#### 5.8.2.1 Empty catch blocks

It is very rarely correct to do nothing in response to a caught exception. When it truly is appropriate to take no action whatsoever in a catch block, the reason this is justified is explained in a comment.

```javascript
try {
  return handleNumericResponse(response);
} catch (ok) {
  // it's not numeric; that's fine, just continue
}
return handleTextResponse(response);
```

Illegal:

```javascript
   try {
    shouldFail();
    fail('expected an error');
  }
  catch (expected) {}
```

<p class="tip">
Tip: Unlike in some other languages, patterns like the above simply don’t work since this will catch the error thrown by fail. Use assertThrows() instead.
</p>

### 5.8.3 Switch statements

Terminology Note: Inside the braces of a switch block are one or more statement
groups. Each statement group consists of one or more switch labels (either
`case FOO:` or `default:`), followed by one or more statements.

#### 5.8.3.1 Fall-through: commented

Within a switch block, each statement group either terminates abruptly (with a
`break`, `return` or thrown exception), or is marked with a comment to indicate
that execution will or might continue into the next statement group. Any
comment that communicates the idea of fall-through is sufficient 
(typically `// fall through`). This special comment is not required in the last
statement group of the switch block.

Example:

```javascript
switch (input) {
  case 1:
  case 2:
    prepareOneOrTwo();
    // fall through
  case 3:
    handleOneTwoOrThree();
    break;
  default:
    handleLargeNumber(input);
}
```

#### 5.8.3.2 The `default` case is present

Each switch statement includes a `default` statement group, even if it contains no code.

## 5.9 this

Only use `this` in class constructors and methods. Any other uses of `this`
must have an explicit `@this` declared in the immediately-enclosing function's
JSDoc.

Never use `this` to refer to the global object, the context of an `eval`, the
target of an event, or unnecessarily `call()`ed or `apply()`ed functions.

## 5.10 Disallowed features

### 5.10.1 with

Do not use the with keyword. It makes your code harder to understand and has been banned in strict mode since ES5.

### 5.10.2 Dynamic code evaluation

Do not use `eval` or the `Function(...string)` constructor (except for code loaders). These features are potentially dangerous and simply do not work in CSP environments.

### 5.10.3 Automatic semicolon insertion

Always terminate statements with semicolons (except function and class declarations, as noted above).

### 5.10.4 Non-standard features

Do not use non-standard features. This includes old features that have been
removed (e.g., `WeakMap.clear`), new features that are not yet standardized
(e.g., the current TC39 working draft, proposals at any stage, or proposed but
not-yet-complete web standards), or proprietary features that are only
implemented in some browsers. Use only features defined in the current ECMA-262
or WHATWG standards. (Note that projects writing against specific APIs, such as
Chrome extensions or Node.js, can obviously use those APIs). Non-standard
language “extensions” (such as those provided by some external transpilers) are
forbidden.

### 5.10.5 Wrapper objects for primitive types

Never use `new` on the primitive object wrappers (`Boolean`, `Number`, `String`, `Symbol`), nor include them in type annotations.

Illegal:

```javascript
var /** Boolean */ x = new Boolean(false);
if (x) alert(typeof x);  // alerts 'object' - WAT?
```

Example:

```javascript
var /** boolean */ x = Boolean(0);
if (!x) alert(typeof x);  // alerts 'boolean', as expected
```

### 5.10.6 Modifying builting objects

Never modify builtin types, either by adding methods to their constructors or
to their prototypes. Avoid depending on libraries that do this. Note that the
JSCompiler’s runtime library will provide standards-compliant polyfills where
possible; nothing else may modify builtin objects.

Do not add symbols to the global object unless absolutely necessary (e.g.
required by a third-party API).


# 6. Naming

## 6.1 Rules common to all identifiers

Identifiers use only ASCII letters and digits, and, in a small number of cases noted below, underscores and very rarely (when required by frameworks like Angular) dollar signs.

Give as descriptive a name as possible, within reason. Do not worry about
saving horizontal space as it is far more important to make your code
immediately understandable by a new reader. Do not use abbreviations that are
ambiguous or unfamiliar to readers outside your project, and do not abbreviate
by deleting letters within a word.

```javascript
priceCountReader      // No abbreviation.
numErrors             // "num" is a widespread convention.
numDnsConnections     // Most people know what "DNS" stands for.
```

Illegal:

```javscript
n                     // Meaningless.
nErr                  // Ambiguous abbreviation.
nCompConns            // Ambiguous abbreviation.
wgcConnections        // Only your group knows what this stands for.
pcReader              // Lots of things can be abbreviated "pc".
cstmrId               // Deletes internal letters.
kSecondsPerDay        // Do not use Hungarian notation.
```

## 6.2 Rules by identifier type

### 6.2.1 Package names

OceansMap does not use packages.

### 6.2.2 Class names

Class, interface, record, and typedef names are written in `UpperCamelCase` or
`PascalCase`.  Unexported classes are simply locals: they are not marked
`@private` and therefore are not named with a trailing underscore.

Type names are typically nouns or noun phrases. For example, `Request`, `ImmutableList`, or `VisibilityMode`. Additionally, interface names may sometimes be adjectives or adjective phrases instead (for example, `Readable`).

### 6.2.3 Method names

Method names are written in `lowerCamelCase`. Private methods' names must end with a trailing underscore.

Method names are typically verbs or verb phrases. For example, `sendMessage` or
`stop_`. Getter and setter methods for properties are never required, but if
they are used they should be named `getFoo` (or optionally `isFoo` or `hasFoo`
for booleans), or `setFoo(value)` for setters.


### 6.2.4 Enum names

Enum names are written in `UpperCamelCase`, similar to classes, and should generally be singular nouns. Individual items within the enum are named in `CONSTANT_CASE`.

### 6.2.5 Constant names

Constant names use `CONSTANT_CASE`: all uppercase letters, with words separated
by underscores. There is noreason for a constant to be named with a trailing
underscore, since private static properties can be replaced by (implicitly
private) module locals.

### 6.2.6 Non-constant field names

Non-constant field names (static or otherwise) are written in `lowerCamelCase`, with a trailing underscore for private fields.

These names are typically nouns or noun phrases. For example, `computedValues` or `index_`.

### 6.2.7 Parameter names

Parameter names are written in `lowerCamelCase`. Note that this applies even if the parameter expects a constructor.

One-character parameter names **ARE STRICTLY FORBIDDEN**

**Exception**: When required by a third-party framework, parameter names may begin with a `$`. This exception does not apply to any other identifiers (e.g. local variables or properties).


### 6.2.8 Local variable names

Local variable names are written in `lowerCamelCase`, except for module-local
(top-level) constants, as described above. Constants in function scopes are
still named in `lowerCamelCase`. Note that `lowerCamelCase` applies even if the
variable holds a constructor.

### 6.2.9 Template parameter names

We do not currently support ECMA Script 6 syntax for class literals due to
[browser incompatibilities](https://kangax.github.io/compat-table/es6/). 

## 6.3 Camel case: defined

Sometimes there is more than one reasonable way to convert an English phrase
into camel case, such as when acronyms or unusual constructs like IPv6 or iOS
are present. To improve predictability, this style guide specifies the following
(nearly) deterministic scheme.

1. Convert the phrase to plain ASCII and remove any apostrophes. For example, Müller's algorithm might become Muellers algorithm.
2. Divide this result into words, splitting on spaces and any remaining punctuation (typically hyphens).
    1. Recommended: if any word already has a conventional camel case appearance in common usage, split this into its constituent parts (e.g., AdWords becomes ad words). Note that a word such as iOS is not really in camel case per se; it defies any convention, so this recommendation does not apply.
3. Now lowercase everything (including acronyms), then uppercase only the first character of:
    1. … each word, to yield upper camel case, or
    2. … each word except the first, to yield lower camel case
4. Finally, join all the words into a single identifier.

Note that the casing of the original words is almost entirely disregarded.

Examples:

| Prose form            | Correct           | Incorrect         |
|-----------------------|-------------------|-------------------|
| XML HTTP request      | XmlHttpRequest    | XMLHTTPRequest    |
| new customer ID       | newCustomerId     | newCustomerID     |
| inner stopwatch       | innerStopwatch    | innerStopWatch    |
| supports IPv6 on iOS? | supportsIpv6OnIos | supportsIPv6OnIOS |
| YouTube importer      | YouTubeImporter   | YoutubeImporter*  |

\*Acceptable, but not recommended.

<p class="note">
Note: Some words are ambiguously hyphenated in the English language: for example nonempty and non-empty are both correct, so the method names checkNonempty and checkNonEmpty are likewise both correct.
</p>


# 7. JSDoc

[JSDoc](https://developers.google.com/closure/compiler/docs/js-for-compiler) is used on all classes, fields, and methods.

## 7.1 General form

The basic formatting of JSDoc blocks is as seen in the example:

```javascript
/**
 * Multiple lines of JSDoc text are written here,
 * wrapped normally.
 * @param {number} arg A number to do something to.
 */
function doSomething(arg) { … }
```

or in this single-line example:

```javascript
/** @const @private {!Foo} A short bit of JSDoc. */
this.foo_ = foo;
```

If a single-line comment overflows into multiple lines, it must use the
multi-line style with `/** and */` on their own lines.

Many tools extract metadata from JSDoc comments to perform code validation and
optimization. As such, these comments must be well-formed.

## 7.2 Markdown

JSDoc is written in Markdown, though it may include HTML when necessary.

Note that tools that automatically extract JSDoc (e.g. [JsDossier](https://github.com/jleyba/js-dossier)) will often ignore plain text formatting, so if you did this:

Illegal:

```javascript
/**
 * Computes weight based on three factors:
 *   items sent
 *   items received
 *   last timestamp
 */
```

it would come out like this:

```
Computes weight based on three factors: items sent items received last timestamp
```

Instead, write a Markdown list:

```javascript
/**
 * Computes weight based on three factors:
 *  - items sent
 *  - items received
 *  - last timestamp
 */
```

## 7.3 JSDoc tags

This style guide allows a subset of JSDoc tags. See 9.1 JSDoc tag reference for
the complete list. Most tags must occupy their own line, with the tag at the
beginning of the line.

Illegal:

```javascript
/**
 * The "param" tag must occupy its own line and may not be combined.
 * @param {number} left @param {number} right
 */
function add(left, right) { ... }
```

Simple tags that do not require any additional data (such as `@private`,
`@const`, `@final`, `@export`) may be combined onto the same line, along with
an optional type when appropriate.

```javascript
/**
 * Place more complex annotations (like "implements" and "template")
 * on their own lines.  Multiple simple tags (like "export" and "final")
 * may be combined in one line.
 * @export @final
 * @implements {Iterable<TYPE>}
 * @template TYPE
 */
class MyClass {
  /**
   * @param {!ObjType} obj Some object.
   * @param {number=} num An optional number.
   */
  constructor(obj, num = 42) {
    /** @private @const {!Array<!ObjType|number>} */
    this.data_ = [obj, num];
  }
}
```

There is no hard rule for when to combine tags, or in which order, but be consistent.

For general information about annotating types in JavaScript see 
[Annotating JavaScript for the Closure Compiler](https://github.com/google/closure-compiler/wiki/Annotating-JavaScript-for-the-Closure-Compiler)
and [Types in the Closure Type System](https://github.com/google/closure-compiler/wiki/Types-in-the-Closure-Type-System).


## 7.4 Line wrapping

Line-wrapped block tags are indented four spaces. Wrapped description text may be lined up with the description on previous lines, but this horizontal alignment is discouraged.

```javascript
/**
 * Illustrates line wrapping for long param/return descriptions.
 * @param {string} foo This is a param with a description too long to fit in
 *     one line.
 * @return {number} This returns something that has a description too long to
 *     fit in one line.
 */
exports.method = function(foo) {
  return 5;
};
```

Do not indent when wrapping a `@fileoverview` description.

## 7.5 Top/file-level comments

A file may have a top-level file overview. A copyright notice , author
information, and default 
[visibility level](https://google.github.io/styleguide/jsguide.html#visibility-annotations)
are optional. File overviews are generally recommended whenever a file consists
of more than a single class definition. The top level comment is designed to
orient readers unfamiliar with the code to what is in this file. If present, it
may provide a description of the file's contents and any dependencies or
compatibility information. Wrapped lines are not indented.

Example:

```javascript
/**
 * @fileoverview Description of file, its uses and information
 * about its dependencies.
 * @package
 */
```

## 7.6 Class comments

Classes, interfaces and records must be documented with a description and any
template parameters, implemented interfaces, visibility, or other appropriate
tags. The class description should provide the reader with enough information
to know how and when to use the class, as well as any additional considerations
necessary to correctly use the class. Textual descriptions may be omitted on
the constructor. `@constructor` and `@extends` annotations are not used with the
class keyword unless the class is being used to declare an `@interface` or it
extends a generic class.


```javascript
/**
 * A fancier event target that does cool things.
 * @implements {Iterable<string>}
 */
class MyFancyTarget extends EventTarget {
  /**
   * @param {string} arg1 An argument that makes this more interesting.
   * @param {!Array<number>} arg2 List of numbers to be processed.
   */
  constructor(arg1, arg2) {
    // ...
  }
};

/**
 * Records are also helpful.
 * @extends {Iterator<TYPE>}
 * @record
 * @template TYPE
 */
class Listable {
  /** @return {TYPE} The next item in line to be returned. */
  next() {}
}
```

<p class="note">
Note: this example uses ES6 syntax which is not currently supported.
</p>

## 7.7 Enum and typedef comments

Enums and typedefs must be documented. Publci enums and typedefs must have a
non-empty description. Individual enum items may be documented with a JSDoc
comment on the preceding line.

```javascript
/**
 * A useful type union, which is reused often.
 * @typedef {!Bandersnatch|!BandersnatchType}
 */
var CoolUnionType;


/**
 * Types of bandersnatches.
 * @enum {string}
 */
var BandersnatchType = {
  /** This kind is really frumious. */
  FRUMIOUS: 'frumious',
  /** The less-frumious kind. */
  MANXOME: 'manxome',
};
```
Typedefs should be limited to defining aliases for unions or complex function
or generic types, and should be avoided for record literals (e.g. `@typedef`
`{{foo: number, bar: string}}`) since it does not allow documenting individual
fields, nor using templates or recursive references. Prefer `@record` for
anything beyond the simplest `@typedef`’d record literal.

## 7.8 Method and function comments

Parameter and return types must be documented. The `this` type should be
documented when necessary. Method, parameter, and return descriptions (but not
types) may be omitted if they are obvious from the rest of the method’s JSDoc
or from its signature. Method descriptions should start with a sentence written
in the third person declarative voice. If a method overrides a superclass
method, it must include an `@override` annotation. Overridden methods must
include all `@param` and `@return` annotations if any types are refined, but should
omit them if the types are all the same.


```javascript
/** This is a class. */
class SomeClass extends SomeBaseClass {
  /**
   * Operates on an instance of MyClass and returns something.
   * @param {!MyClass} obj An object that for some reason needs detailed
   *     explanation that spans multiple lines.
   * @param {!OtherClass} obviousOtherClass
   * @return {boolean} Whether something occurred.
   */
  someMethod(obj, obviousOtherClass) { ... }

  /** @override */
  overriddenMethod(param) { ... }
}

/**
 * Top-level functions follow the same rules.  This one makes an array.
 * @param {TYPE} arg
 * @return {!Array<TYPE>}
 * @template TYPE
 */
function makeArray(arg) { ... }
```

<p class="note">
  Note: the above example includes ES6 syntax which is not supported in OceansMap
</p>

Anonymous functions do not require JSDoc, though parameter types may be
specified inline if the automatic type inference is insufficient.

```javascript
promise.then(
    function(/** !Array<number|string> */ items) {
      doSomethingWith(items);
      return /** @type {string} */ (items[0]);
    });
```

## 7.9 Property comments

Property types must be documented. The description may be omitted for private
properties, if name and type provide enough documentation for understanding the
code.

Publicly exported constants are commented the same way as properties. Explicit
types may be omitted for `@const` properties initialized from an expression with
an obviously known type.

<p class="tip">
Tip: A <pre>@const</pre> property’s type can be considered “obviously known” if it is
assigned directly from a constructor parameter with a declared type, or
directly from a function call with a declared return type. Non-const properties
and properties assigned from more complex expressions should have their types
declared explicitly.
</p>


```javascript
/** My class. */
class MyClass {
  /** @param {string=} someString */
  constructor(someString = 'default string') {
    /** @private @const */
    this.someString_ = someString;

    /** @private @const {!OtherType} */
    this.someOtherThing_ = functionThatReturnsAThing();

    /**
     * Maximum number of things per pane.
     * @type {number}
     */
    this.someProperty = 4;
  }
}

/**
 * The number of times we'll try before giving up.
 * @const
 */
MyClass.RETRY_COUNT = 33;
```

<p class="note">
  Note: the above example includes ES6 syntax which is not supported in OceansMap
</p>

## 7.10 Type annotations

Type annotations are found on `@param`, `@return`, `@this`, and `@type` tags,
and optionally on `@const`, `@export`, and any visibility tags. Type
annotations attached to JSDoc tags must always be enclosed in braces.

## 7.10.1 Nullability

The type system defines modifiers `!` and `?` for non-null and nullable,
respectively. Primitive types (`undefined`, `string`, `number`, `boolean`, `symbol`, and
`function(...): ...`) and record literals (`{foo: string, bar: number}`) are
non-null by default. Do not add an explicit `!` to these types. Object types
(`Array`, `Element`, `MyClass`, etc) are nullable by default, but cannot be
immediately distinguished from a name that is `@typedef`’d to a
non-null-by-default type. As such, all types except primitives and record
literals must be annotated explicitly with either `?` or `!` to indicate whether
they are nullable or not.

## 7.10.2 Type Casts

In cases where type checking doesn't accurately infer the type of an
expression, it is possible to tighten the type by adding a type annotation
comment and enclosing the expression in parentheses. Note that the parentheses
are required.

```javascript
/** @type {number} */ (x)
```

## 7.10.3 Template Parameter Types

Always specify template parameters. This way compiler can do a better job and it makes it easier for readers to understand what code does.

Bad:

```javascript
/** @type {!Object} */ var users;
/** @type {!Array} */ var books;
/** @type {!Promise} */ var response;
```

Good:

```javascript
/** @type {!Object<string, !User>} */ var users;
/** @type {!Array<string>} */ var books;
/** @type {!Promise<!Response>} */ var response;

/** @type {!Promise<undefined>} */ var thisPromiseReturnsNothingButParameterIsStillUseful;
/** @type {!Object<string, *>} */ var mapOfEverything;
```

Cases when template parameters should not be used:

- `Object` is used for type hierarchy and not as map-like structure.

## 7.11 Visibility annotations

Visibility annotations (`@private`, `@package`, `@protected`) may be specified in a
`@fileoverview` block, or on any exported symbol or property. Do not specify
visibility for local variables, whether within a function or at the top level
of a module. All `@private` names must end with an underscore.


# 8. Policies

The policies section describes patterns and practices within use of OceansMap.

## 8.1 Nested Anonymous Functions

Anonymous functions should not be nested inside function arguments.

Illegal:

```javascript
var bestItems = _.map(
    _.filter(itmes, function(item) {
      return item.property === "thing" && shouldFilter;
    }), function(item) {
      return {name: item.name, value: item.value};
    });

```

Example:

```javascript
/** 
  * An array of ItemModels where the property is "thing".
  * @type {Array<ItemModel>} 
  */
var filteredItems = _.filter(items, function(item) {
  return item.property === "thing" && shouldFilter;
});

/** 
  * An array of objects containing name and value of the filtered ItemModels.
  * @type {Array<Object>} 
  */
var bestItems = _.map(filteredItems, function(item) {
  return {name: item.name, value: item.value};
});
```

## 8.2 Inline Conditionls

Inline conditionals are allowed but discouraged for readability reasons.

```javascript
var itemCount = items && items.length ? items.length : 0;
```

Is a little bit harder to read than:

```javascript
var itemCount = 0;

if (items && items.length) {
  itemCount = items.length;
}
```

Albeit the latter is more verbose but more clear.

Using conditionals where the values returned by the evaluation of the conditionals are JavaScript expressions are **strictly forbidden**.

Illegal:

```javscript
// Illegal because of the operator
var itemCount = items && items.length ? items.length + 2 : 0;
```

## 8.3 RegEx Comparisons

Regular Expression (RegEx) comparisons through the `.test()` method should be
done sparingly and only when strictly needed. RegEx operations are not highly
optimized and where done carelessly could decrease performance.

Illegal:

```javascript
if (!/geojson/.test(catalogModel.get('type'))) {
  // ...
}
```

Instead use `indexOf` in this case

```javascript

if (catalogModel.get('type').indexOf('geojson') < 0) {
  // ...
}
```


# 9. Appendices

