# DynamiX Front-End Guide

The following document outlines DynamiX's standards and general best practices for front-end development. These guidelines strongly encourage the use of existing, common, sensible patterns. They should be used to develop in your daily workflow.

This is a living document and new ideas are always welcome. Please contribute.

## Table of contents

1. [General principles](#general-principles)
2. [Project File Structure](#file-structure)
3. [CSS](#css)
	* [Browser Support](#browser-support)
	* [Structure](#structure)
	* [Selectors](#selectors)
	* [Properties](#properties)
	* [Values](#values)
	* [Units](#units)
	* [Vendor Prefixes](#vendor-prefixes)
	* [Media Queries](#media-queries)
	* [Comments](#comments)
	* [CSS Tips & Tricks](#tips)
4. [Less](#less)
5. [HTML](#html)
	* [Validation](#validation)
	* [Self-Closing Elements](#self-closing-elements)
	* [Quotes](#quotes)
	* [Indentation](#indentation)
	* [Images](#images)
6. [JavaScript/jQuery](#js) - Coming Soon
7. [PHP for the Front-End](#php)
8. [Pre-Launch Checklist](#prelaunch)
9. [References](#references)

<a name="file-structure"></a>
## Project File Structure
* Each layout should have a unique .less file and .js file if application
* Less and JS files should correspond with their PHP file: `layout-feature.php` -> `layout-feature.less` & `layout-feature.js`


> "Part of being a good steward to a successful project is realizing that
> writing code for yourself is a Bad Idea. If thousands of people are using
> your code, then write your code for maximum clarity, not your personal
> preference of how to get clever within the spec." - Idan Gazit

* All code in any code-base should look like a single person typed it, even when many people are contributing to it.
* Strictly enforce the agreed-upon style.
* If in doubt when deciding upon a style use existing, common patterns.

<a name="general-principles"></a>
## General principles

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

<a name="structure"></a>
### Structure
* Use tabs to indent each property (preference 4 spaces)
* Each selector should be on its own line, ending in either a comma or opening curly brace
* When a group of selectors have a single matching property, group them and list the property/values on one line

**EXAMPLE**
```
.layout-feature {
	.feature-header,
	.feature-body,
	.feature-footer {
		background-color: @light-gray;
		color: @blue;
	}

	.feature-grid-1 { background-color: @gray; }
	.feature-grid-2 { background-color: @black; }
	.feature-grid-3 { background-color: @blue; }
}
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
	* The exception to this is when tags are inside of a Content Editor/WYSIWYG 
* Do not use ID's for styling
* Do not over-qualify selectors: `div.feature-wrapper` should be `.feature-wrapper`


<a name="properties"></a>
### Properties - General Rules
* Properties should be followed by a colon then a space: `background-color:@blue` should be `background-color: @blue`
* All properties and values should be lowercase, except for font names
* All colors should be defined as a variable 
* Shorthand should be used as much as possible (background, list-style, padding, etc)
* Do not use shorthand when listing one property: `background: @blue` should be `background-color: @blue` 


### Properties - Ordering
All properties should be grouped by type. 

**EXAMPLE**

Comments are added for description sake and not necessary. Spacing between grouped type is optional.

```
.selector {
/* Layout & Positioning */
	position: absolute;
	top: 0;
	right: 0;
	z-index: 10;

/* Display & Box Model */
	display: inline-block;
	width: 50%;
	padding: 15px 10px;
	border: 2px solid @gray;
	margin: 10px;
	
/* Color */
	background-color: @blue;
	color: @white;

/* Text */
	font-size: 2em;
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
* Do not pad parentheses with spaces
* Always end values with a semicolon
* Use double quotes rather than single quotes and only when needed (font names when space separated)
* Font weights should be defined using numeric values: `bold` should be `700`
* Values that are 0 should be unitless: `margin: 0px;` should be `margin: 0;`
* `line-height` should be unitless unless defined at a specific pixel value
* Use a leading zero for decimal values: `opacity: .5;` should be `opacity: 0.5`
* Comma separated values for one property should be separated by a newline:

**Don't:**
```
.selector {
	transform: translateY( 50% );
	transition: all 300ms	
}
```

**Do:** 
```
.selector {
	transform: translateY(50%);
	transition: all 300ms;
}
```


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

* Media queries are written as `@media screen and` then the width/height property
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
When in doubt, always comment. Silent comments in Less are in notated with two forward slashes. All commented are removed when Grunt builds the project.

**EXAMPLES**

Single line comments for a brief note on a declaration 
```
.feature-header {
	width: ~"calc(100% - 60px)"; // 60px is left and right padding at 30px
}
```

Multiple line comments are wrapped in Less silent comments and extended asterisks.
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
* Match the `max-width` value to the `flex-basis` value.  

**EXAMPLE**
```
.flex-child {
	flex: 1 0 75%;
	max-width: 75%;
	padding: 0 1em;
	box-sizing: border-box;
}
```

<a name="less"></a>
## Less
### Nesting
Selectors should be nested only one level. 

**EXAMPLE**
```
.layout-feature {
	.layout-feature-header {
		width: 25%;
	}
}
```

### Color Variables
Colors are defined by six digit hex values and grouped in like color groups.

**EXAMPLES**
```
@white: #ffffff;
@black: #000000;

@gray: #333333;
@light-gray: #eeeeee;

@blue: #0064ff;
```

### Font Variables
All fonts should be defined as variables

**EXAMPLE**
```
@sans: "Open Sans", sans-serif;
@serif: "Merriweather", serif;
```

<a name="html"></a>
## HTML
<a name="validation"></a>
### Validation
* Each layout must be tested and pass validation on the [W3C Validator](https://validator.w3.org/nu/) 

<a name="self-closing-elements"></a>
### Self-Closing elements
* All tags that are self-closing must have a forward slash proceeded by one space. The correct method is: `<br />` not `<br/>`

<a name="quotes"></a>
### Quotes
To maintain consistency, all attributes with values must be quoted with double-quotes. If an attribute is the same as the value name, the value can be omitted. 

**EXAMPLE**
```
	<input type="text" name="email" disabled />
```

<a name="indentation"></a>
### Indentation
* Both HTML and PHP should follow indentation in a logical structure
* Use tabs to indent (preference 4 spaces)

**EXAMPLE** 
```
<ul>
	<?php foreach($articles as $article) { ?>
		<li><?= $article['header'] ?></li>
	<?php } ?>
</ul>
```

<a name="images"></a>
### Images
For most images you will use the following format:

`<img src="<?= buildImageSrc($image, $width, $height) ?>" alt="{alt tag here}" />`
or
`<div style="background-image: url('<?= buildImageSrc($image, $width, $height) ?>');"> </div>`

In the event that you have an image that needs retina-fication, such as a logo, you will use the following to generate an img tag with the srcset, class, and alt properties filled automatically:

`<?= buildRetinaImage($image, $width, $height, "alt tag here", "image-class") ?>`

"What if I need to resize or bound an image?!" Well, that is quite easy as well. You simply need to add another argument with the string corresponding to the functionality you desire.

Example: you wish to have an image that is "fit" instead of the default value of "crop"

`<img src="<?= buildImageSrc($image, $width, $height, "fit") ?>" alt="{alt tag here}" />`

Finally, by default every image generated has a quality coefficient of 80 set by default. If, for any reason, you need to modify that value, or if you need to add further cloudimage operations, you merely need to add another argument.

`<img src="<?= buildImageSrc($image, $width, $height, "fit", "q87.ctrans.tpng") ?>" alt="{alt tag here}" />`

This will make an image fit, with a quality coefficient of 87, and then also will transform the file to a PNG so the letterboxing (if any) is transparent. You can daisy-chain as many cloudimage operations as you would like, so long as they are delineated by periods.


<a name="js"></a>
## JavaScript/jQuery
![image of javascript](http://i.imgur.com/a1lSytU.gif "This is javascript")

<a name="php"></a>
## PHP for the Front-End

### Conditionals
PHP conditionals can be written a number of different ways, but as part of our goal of normalizing code practices we use `&&`/`||` instead of `AND`/`OR`, and we'll be using braces instead of colon notation.

Do:
```
if ($foo != $bar && $bar != $foo) {
	//this is a good conditional
}
```

Don't:
```
if ($foo != $bar AND $bar != $foo):
	//this is non-standard notation, and is thus bad
endif;
```

### Quick Echo format
PHP has a wonderful shorthand that allows a quick, single line (to the interpreter) echo of values. This format is _always_ followed by a PHP close tag, so the semi-colon will be omitted.

Do:
```
<?= $foo['bar'] ?>
```

Don't:
```
<?= $foo['bar']; ?>
```

#### Side Note
Except in the shorthand notation, always include the final `;` where needed. 

Do: 
```
<?php
	echo $foo;
?>
```

Don't:
```
<?php
	//this won't throw an exception, but is to be avoided.
	echo $foo
?>
```

<a name="prelaunch"></a>
## Pre-Launch Checklist
* Browser test. See the [browsers supported](#browser-support)
* Validate HTML via the [W3C Validator](https://validator.w3.org/nu/)
* Optimize S3 images
* Optimize stylesheets/images directory
* Speed test at [PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/)
	* Park the DOMAIN_NAME.pagespeed.dynamixlabs.com domain in SE/Octane then perform test on DOMAIN_NAME.pagespeed.dynamixlabs.com
	* Remove parked domain immediately after testing
* Implement [Google Tag Manager](https://tagmanager.google.com/)
	* Open a recent project, access the Admin menu, then select Export Container. Follow prompts. 
	* Open/create current site in Google Tag Manager (GTM)
	* Access the Admin menu, then select Import Container. Follow prompts.
	* Change Variables for the GA Code (taken from existing site) and Site Host
	* Change Outbound Links to correct URL
* Confirm analytic events is tracking properly:
	* Comment out top if statement in the header.php file:
	```
	<?php //if(isset($_SERVER['env']) && $_SERVER['env'] != 'development'){
		echo $site_analyticskey;
		echo "\n";
	//} ?>
	```
	* In GTM, click Publish


<a name="references"></a>
## References
* [Idiomatic CSS](https://github.com/necolas/idiomatic-css)
* [MDN CSS Best Practices](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Writing_efficient_CSS)
* [MDN Units Documentation](https://developer.mozilla.org/en-US/docs/Web/CSS/length)
