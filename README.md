# DynamiX Front-End Standards Guide

The following document outlines Dynamix's standards for front-end development. These guidelines strongly encourage the use of existing, common, sensible patterns. They should be used to develop in your daily workflow.

This is a living document and new ideas are always welcome. Please contribute.


## Table of contents

1. [General principles](#general-principles)
2. [Whitespace](#whitespace)
3. [Comments](#comments)
4. [CSS](#css)
5. [HTML](#html)
6. [JavaScript/jQuery](#js)

<a name="general-principles"></a>
## 1. General principles

> "Part of being a good steward to a successful project is realizing that
> writing code for yourself is a Bad Idea™. If thousands of people are using
> your code, then write your code for maximum clarity, not your personal
> preference of how to get clever within the spec." - Idan Gazit

* Don't try to prematurely optimize your code; keep it readable and
  understandable.
* All code in any code-base should look like a single person typed it, even
  when many people are contributing to it.
* Strictly enforce the agreed-upon style.
* If in doubt when deciding upon a style use existing, common patterns.


<a name="whitespace"></a>
## 2. Whitespace

Only one style should exist across the entire source of your code-base. Always be consistent in your use of whitespace. Use whitespace to improve readability.

* Use spaces for indentation and remain consistant with the number of characters used per indentation level.
  (Preference: 4 spaces)

Tip: configure your editor to "show invisibles" or to automatically remove end-of-line whitespace.


<a name="comments"></a>
## 3. Comments

Well commented code is extremely important. Take time to describe components,
how they work, their limitations, and the way they are constructed. Don't leave
others in the team guessing as to the purpose of uncommon or non-obvious
code.

Comment style should be simple and consistent within a single code base.

* Place comments on a new line above their subject.
* Keep line-length to a sensible maximum, e.g., 80 columns.
* Use "sentence case" comments and consistent text indentation.

Example:

```css
/* Basic comment */
```


<a name="css"></a>
## 4. CSS


<a name="html"></a>
## 5. HTML


<a name="js"></a>
## 6. JavaScript/jQuery


Based on a work at
[github.com/necolas/idiomatic-css](https://github.com/necolas/idiomatic-css).
