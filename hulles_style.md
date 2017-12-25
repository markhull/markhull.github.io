---
layout: page
title: Hulles Java Style Guide
permalink: /style/
published: true
---

This is the official **Hulles Java™ Style Guide**, accept no substitute. It is based on 
[Google's Java Guide](https://google.github.io/styleguide/javaguide.html),
which is reproduced below, along with the differences between Hulles' and Google's style.

## Divergence From Google's Guide

These are the differences between Hulles Java Style and Google Java Style; the differences are also hightlighted
below in the reproduced Google document.

4.2 Block indentation s/b **+4** spaces, vs. +2 in Google.

4.5.2 Continuation lines are indented **8** spaces

4.8.2.2 Local variables are **ALWAYS** declared at the start of their containing block or block-like construct. 
Local variable declarations do not typically have initializers, but are preferably initialized in the statements 
immediately following the local variable declarations. Initializers like `true`, `false`, `null` are okay in the declarations.
Java `super` statements can precede variable declarations in constructors (because they have to ).

4.8.4.1 Indentation is **+4** spaces, see 4.2 above.

4.8.5 Using a single parameterless annotation together with the first line of the signature is not allowed.

4.8.7 *[same as Google, included here for reference]* Class and member modifiers, when present, appear in the order 
recommended by the Java Language Specification: 

 **`public protected private abstract default static final transient volatile synchronized native strictfp`**



