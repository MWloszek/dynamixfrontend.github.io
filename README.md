# DynamiX Front-End Guide

The following document outlines DynamiX's standards and general best practices for front-end development. These guidelines strongly encourage the use of existing, common, sensible patterns. They should be used to develop in your daily workflow.

This is a living document and new ideas are always welcome. Please contribute.


## Table of contents

1. [General principles](#general-principles)
2. [CSS](#css)
	* [Browser Support](#browser-support)
	* [Organization](#organization)
	* [Structure](#structure)
	* [Selectors](#selectors)
	* [Properties](#properties)
	* [Values](#values)
	* [Units](#units)
	* [Vendor Prefixes](#vendor-prefixes)
	* [Media Queries](#media-queries)
	* [Comments](#comments)
	* [CSS Tips & Tricks](#tips)
3. [Less](#less)
4. [HTML](#html) - Coming Soon
5. [JavaScript/jQuery](#js) - Coming Soon
6. [References](#references)

<a name="general-principles"></a>
## General principles

> "Part of being a good steward to a successful project is realizing that
> writing code for yourself is a Bad Idea™. If thousands of people are using
> your code, then write your code for maximum clarity, not your personal
> preference of how to get clever within the spec." - Idan Gazit

* All code in any code-base should look like a single person typed it, even when many people are contributing to it.
* Strictly enforce the agreed-upon style.
* If in doubt when deciding upon a style use existing, common patterns.


<a name="css"></a>
## CSS

<a name="browser-support"></a>
### Browser Support
#### Desktop
We support the latest versions of Chrome, Firefox, IE11, Edge, and Safari. 
The width container we develop to is 1600px. Please note, designs are built at 1280px, so develop at 1600px and ensure the site continues to match the design at 1280px. 

#### Mobile
We support the current and two prior versions of iOS and the mobile version of Chrome on Android.
The minimum screen size we develop to is 320px. 

<a name="organization"></a>
### Organization
* Each layout should have a unique .less file
* Less files should correspond with their PHP file: `layout-feature.php` -> `layout-feature.less`


<a name="structure"></a>
### Structure
* Use tabs to indent each property (preference 4 spaces wide)
* Each selector should be on its own line, ending in either a comma or opening curly brace
* When a group of selectors have a single matching property, group them and list the property/values on one line

**EXAMPLE**
```
.feature-header,
.feature-body,
.feature-footer {
	background-color: @light-gray;
	color: @blue;
}

.feature-grid-1 { background-color: @gray; }
.feature-grid-2 { background-color: @black; }
.feature-grid-3 { background-color: @blue; }
```

<a name="selectors"></a>
### Selectors
#### Do:
* Use classes for all styling
* Use lowercase and hyphen-separated words for naming selectors
* Attribute selectors must have quotes: `input[type="text"]`

#### Don't:
* Avoid universal selectors
* Avoid tag selectors: `.layout-feature h1` should be `.layout-feature-header`
* Do not use ID's for styling
* Do not over-qualify selectors: `div.feature-wrapper` should be `.feature-wrapper`


<a name="properties"></a>
### Properties - General Rules
* Properties should be followed by a colon then a space: `background-color:@blue` should be `background-color: @blue`
* All properties and values should be lowercase, except for font names
* All colors should be defined as a variable 
* Shorthand should be used as much as possible (background, font, list-style, padding, etc)
* Do not use shorthand when listing one property: `background: @blue` should be `background-color: @blue` 


### Properties - Ordering
All properties should be grouped by type. 

**EXAMPLE**

Comments are added for description sake and not necessary. Spacing between grouped type is optional.

```
.selector {
/* Display & Box Model */
	display: inline-block;
	width: 50%;
	padding: 15px 10px;
	border: 2px solid @gray;
	margin: 10px;

/* Layout & Positioning */
	position: absolute;
	top: 0;
	right: 0;
	z-index: 10;

/* Color */
	background-color: @blue;
	color: @white;

/* Text */
	font: 700 16px/1.2 "Open Sans", sans-serif;
	text-align: right;

/* Other/Misc */
	cursor: pointer;

/* Animations & Transitions */
	transition: all 300ms;
	transform: translateY(50%);
}
```


<a name="values"></a>
### Values
* Do not pad parantheses with spaces
* Always end values with a semicolon
* Use double quotes rather than single quotes and only when needed (font names when space separated)
* Font weights should be defined using numeric values: `bold` should be `700`
* Values that are 0 should be unitless: `margin: 0px;` should be `margin: 0;`
* `line-height` should be unitless unless defined at a specific pixel value
* Use a leading zero for decimal values: `opacity: .5;` should be `opacity: 0.5`
* Comma separated values for one property should be separated by a newline:

**EXAMPLE**
```
.selector {
	box-shadow: 1px 1px 1px 0 @black,
				2px 2px 2px 0 @gray;
}
```

<a name="units"></a>
### Units
* Use units consistently. If you must mix units in a shorthand declaration, add comments explaining why
* Avoid using [Magic Numbers](https://css-tricks.com/magic-numbers-in-css/), add comments if unavoidable

**Do:**
```
.selector {
	padding: 2em 0;
	margin: 2em 5%; // 2em to remain consistent with other layouts, 5% to match design
}
```

**Don't:**
```
.selector {
	padding: 10px 15% 3rem 2em;
}
```

<a name="vendor-prefixes"></a>
### Vendor Prefixes
Vendor prefixes are automatically added when Grunt builds the project. Be sure you are still verifying browser support. 


<a name="media-queries"></a>
### Media Queries
DynamiX sites are built responsively, not by any defined breakpoint. Our philosophy is that our sites should look great on any sized screen. 

* Media queries are nested within the property:

**EXAMPLE**
```
.feature-wrapper {
	width: 50%;
	@media screen and (max-width: 767px) {
		width: 100%;
	}
}

```

<a name="comments"></a>
### Comments
When in doubt, always comment. Silent comments in Less are in notated with two forward slashes. 

**EXAMPLES**

Single line comments for a brief note on a declaration 
```
.feature-header {
	width: ~"calc(100% - 60px)"; // 60px is left and right padding at 30px
}
```

Multiple line comments are wrapped in Less silent comments and extended astericks.
```
//****************************************************************************/
//  Header Section
//  or 
//  Multiple Line Comment block
//****************************************************************************/
```

<a name="tips"></a>
## CSS Tips & Tricks
### Flexbox and Browser Support

* `flex` descendants in IE11 do not respect `box-sizing: border-box`, so be sure to add a `max-width`

**EXAMPLE**
```
.flex-child {
	flex: 1 0 100%;
	max-width: 100%;
	padding: 0 1em;
	box-sizing: border-box;
}
```

<a name="less"></a>
## Less
### Color Variables
Colors are defined by six digit hex values and grouped in like color groups

**EXAMPLES**
```
@white: #ffffff;
@black: #000000;

@gray: #333333;
@light-gray: #eeeeee;

@blue: #0064ff;
```


<a name="html"></a>
## HTML - Coming Soon


<a name="js"></a>
## JavaScript/jQuery - Coming Soon


<a name="references"></a>
## References
* [Idiomatic CSS](https://github.com/necolas/idiomatic-css)
* [MDN CSS Best Practices](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Writing_efficient_CSS)
* [MDN Units Documentation](https://developer.mozilla.org/en-US/docs/Web/CSS/length)
