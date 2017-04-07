# OceansMap Conventions

This repository is used to guide and maintain a set of conventions for
developing OceansMap in a distributed environment.

Copyright 2017 RPS Group Plc
See LICENSE for details

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

<style>
.tip {
  background-color: #fffbd9;
  padding: 6px 8px 6px 10px;
  border-left: 6px solid #ffef70;
}

</style>
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

# 5. Language Features

# 6. Naming

# 7. JSDoc

# 8. Policies

# 9. Appendices

