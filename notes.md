# Advanced Css and Sass Project 1: Natours Website

Website for a fictional nature tours company

Course Notes: (https://www.udemy.com/course/advanced-css-and-sass/)
by Jonas Schmedmann (https://www.udemy.com/course/advanced-css-and-sass/#instructor-1)

MDN: https://developer.mozilla.org/en-US/docs/Web

## Lesson 6) Building the Header - Part 1
"Percentages ... are defined relative to the value of the **parent element's** corresponding parameter"
  (https://www.udemy.com/course/advanced-css-and-sass/learn/lecture/8274486#questions/9667946)

### Basic Reset

Use the universal selector to apply certain non-inheritable rules to all elements.

### Font Properties

Define on the "body" selector. Font properties are generally inheritable,
and inheritance is more efficient than applying properties via the universal selector.

### `background-image`
- Applies one or more background images on an element
- multiple images can be specified, separated by commas, with the first image on "top"
  (closest to user)
- `url()` function to specify pathname of the image
- `linear-gradient()` function specifies a color gradient
- [MDN Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/background-image)

### `background-size`
- Sets the size of the element's background image
- Can take 1 or 2 values:
    - One-value applies to image width, implies value of `auto` for height
    - Two-value syntax: width, height
- Valid values:
    - `auto`: scales image in corresponding direction to maintain intrinsic proportions
    - `cover`: scales image (preserving aspect ratio) to smallest possible size to fill container, leaving no empty
      space, cropping as necessary
    - `contain`: scales image (preserving aspect ration) as large as possible, without cropping or stretching. Empty
      space will be covered by tiling, unless `backoungrd-repeat` is set to `no-repeat`
    - &lt;length&gt;: Stretches image to specified length; negative values not allowd
    - &lt;percentage&gt; Stretches image to specified percentage of the *background positioning area*
- [MDN Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/background-size)

### `background-position`
- sets the initial position for each background image
- relative to position layer set by `background-origin`
- [MDN Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/background-position)

### `clip-path`
- clips what is seen in the element
- defines a clipping region
- parts of the element inside the region are shown; outside are not
- [Online CSS clip-path maker](bennettfeely.com/clippy) 

### `url()`
- Used to include a file
- parameter: absolute, relative, blob or data URL; quotes optional, unless it contains whitespace, etc
- [MDN Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/clip-path)

### `linear-gradient()`
- Creates an image consisting of a progressive transition between two or more colors along a straight line
- [MDN Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/gradient/linear-gradient) 

### `polygon()`
- Creates a polygon by specifying one or more pairs of coordinates
- [MDN Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/basic-shape/polygon)


## Lesson 7) Building the Header - Part 2
- position: absolute
    - top/bottom and left/right are relative to first positioned ancestor,
      so add position to the ancestor (traditionally we use "relative" for ancestor)
- centering:
    - position: absolute;
    - top: 50%;
    - left: 50%;
    - transform: translate(-50%, -50%);
    - 50% in top and left refer to 50% of the size of the container.
    - 50% in translate refers to 50% of the size of the element itself.
- `<h1>` is the most important element for SEO, so the entire title should be included,
  even if the entire title is not displayed uniformly. So break it into spans and
  style the spans.

### Lesson 8) Creating Cool CSS Animations

- animations: transitions vs keyframes
- define animation frames with @keyframes <animation-name>, and percentage steps
- declare animation properties on the element to animate
- add "backface-visibility: hidden" property on parent (?)

### Lesson 9) Building a Complex Animated Button - Part 1

- pseudo-class: special state (eg: link, active, hover)
- position: inline-block is treated as text, so it can be centered by putting text-align: center on the parent
- transform property used for lots of animations
- transforms are relative to base state, not to other any other (eg, "current") state

### Lesson 10) Building a Complex Animated Button - Part 2

- pseudo-elements are not "real" elements, in the DOM, but act like elements
- ::after requires content and display properties, even if empty, or it won't appear
- ::after acts as a child of the target element
- animation-fill-mode to set initial state of an animation

### Lesson 12) Three Pillars of HTML and CSS (Never Forget Them!)

1) Responsive Design:
    - every website should work correctly across different devices and display sizes
    - responsive images
    - correct units (font sizes, element dimensions)
    - desktop-first vs mobile-first
2) Maintainable and scalable code
    - clean, easy to understand, extensible, reusable
    - CSS file organization
    - class names
    - HTML structure
3) Web Performance
    - faster, smaller

- minimize HTTP requests
- compress code, images
- CSS preprocessor

### Lesson 13) How CSS Works Behind the Scenes: An Overview

- What happens when an HTML page is loaded?
    - browser parses the HTML into a DOM
    - CSS files are loaded and parsed into CSSOM
        - resolve conflicting CSS declarations (cascade)
        - process final CSS values: ie, percentages and other relative units converted to pixels. Can only be done in
          the
          context of a physical device
    - DOM + CSSOM compose the render tree
    - Browser renders the page using the visual formatting model

### Lesosn 14) How CSS Is Parsed, Part 1: The Cascade and Specificity

- CSS Rule: <selector> <declaration-block>
- declaration block is a list of 0 or more declarations;
- declaration is a property and declared value
- cascade: process of resolving multiple conflicting rules to a given element
- declarations can come from author, user or browser
- cascade: importance > specificity > declaration order
    - importance:
        - user !important
        - author !important
        - author declarations
        - user declarations
        - browser (default) declarations
    - specificity:
        - inline
        - IDs
        - classes, pseudo-classes, attributes
        - elements, pseudo-elements
    - declaration order
        - last one declared is the one applied
- The universal selector has no specificity (0,0,0,0)
- 3rd-party stylesheets should be included first, so that author stylesheets are declared after

### Lesson 16) How CSS Is Parsed, Part 2: Value Processing

- All units are eventually converted to pixels
- Processing order:
    - declared value: value(s) declared in a rule; multiple rules may apply (pre-cascae)
      _ cascaded value: value determined after the cascade (user agent values included here)
    - specified value: property default, if no cascade
        - may be the "initial value" (not the same as user agent value)
        - for inheritable properties, value of the parent element's property
    - computed value: converting relative to absolute (important for inheritance); keywords also converted in this step
    - used value: final calculations, based on layout (such as percentages)
    - actual value: what the browser can actually render
- EVERY CSS property needs a value, even if it's not declared explicitly
- Converting from relative to absolute (px):
    - % (font): percentage of parent element's font size
    - % (length): percentage of parent element's COMPUTED WIDTH
    - em (font): multiple of PARENT's computed font size
    - em (length): multiple of CURRENT element's computed font size
    - rem: multiple of root font size
    - vh: 1% of viewport height
    - vw: 1% of viewport width

### Lesson 17) How CSS Is Parsed, Part 3: Inheritance

- For inheritable properties, if a child element does not have a cascaded value,
  then the SPECIFIED value of the child is the COMPUTED value of the parent.
- Properties related to FONT are usually inherited
- Other properties usually are not
- The keyword "inherit" forces inheritance of a property
- the keyword "initial" resets a property back to its initial value

### Lesson 18) Converting from px to rem: An Effective Workflow

- The ROOT FONT SIZE
    - default value provided by the browser, usually 16px.
    - can be overridden by the user, such as increased to compensate for poor eyesight
    - can be further overridden by the CSS author in the "html" selector
- The "rem" measurement equals the root font size.
- We want a root font size of 10px, for easy math.
- We COULD set the root font size directly to 10px in the "html" selector".
- However, specifying a root font size in absolute values (ie, px) is bad practice, as it overrides any value set by the
  user. Rather, therefore, set the root font size as a percentage, which refers to a percentage of the browser's root
  font size (whether default or user-set). We want 10px, and assuming a 16px browser font size, we need to specify
  62.5%. If the user adjusts the default root font size, all measurements specified in "rem" units will adjust
  accordingly.
- box-sizing
    - instead of specifying box-sizing value of "border-box" in the universal selector, specify a value of "inherit".
      This
      wil cause the box-sizing property to become inheritable (which it generally is not).
    - Then, specify a box-sizing property of "border-box" in the "body" selector, and all children will then inherit
      border-box for this property.
    - This is considered better practice (?) in the CSS community.
- Apparently, the universal selector does not apply to ::before and ::after psuedo-elements, so include *::before and
  *::after explicitly in the reset rule.

### Lesson 19) How CSS Renders a Website: the Visual Formatting Model

- def: algorithm that calculates boxes and determines the layout of these boxes, for each element in the render tree,
  in order to determine the final layout of the page.
- box model
    - fill area: content and padding, for background color or images (do not cover margin)
    - element dimensions margin + border + padding + content dimensions (natural or specified)
    - Specifying a value of "border-box" for the "box-sizing" property of an element will cause the box model to use the
      specified height and width to refer to both the content and the padding and border
- display types:
    - block (includes flex, list-item and table): 100% of parent width; stacked vertically; line-breaks before and after
    - inline: content distributed in lines; occupy only content's space; no line-breaks; height/width properties do not
      apply; only left and right paddings and margins (no top/bottom)
    - inline-block: technically inline elements, using only content space and have no line breaks; act as block-level on
      the "inside", so height/width and padding/margin work as block-level lements
- positioning:
    - normal flow: static or relative positioning; elements laid out in source order
    - floats: removed from normal flow; shifted to left/right as far as possible to edge of containing box, or another
      floated element; text and inline element wrap around the float; container does not adjust height to the float,
      necessitating "clear-fix" hack
    - absolute: absolute and relative positioning; element removed from normal flow; no impact on surrounding content or
      elements (can even overlap - resolved via stacking context); positioned w/ top, bottom, left, right.
- stacking context: determines order overlapping elements are rendered; various CSS properties create new stacking
  contexts: z-index, opacity != 1, transform, filter, et al; absolute and relative positioning can also affect
  stacking order; higher stacking context appears above lower ones.

### Lesson 20) CSS Architecture, Components and BEM

- BEM: Block-element modifier.
    - Block: stand-alone component, meaningful on its own: .block {}
    - Element: part of a block, no meaning on its own: .block__element {}
    - Modifier: Different version of a block or element: .block__element--modifier {}
    - Results in very low CSS specificities.
- Architect: how to arrange CSS files
    - various models, including 7-1: 7 folders for partial SASS files, imported by 1 main SASS file compiled into a
      single style sheet: base, components, layout, pages, theme, abstract, vendors

### Lesson 23) What is Sass?

- CSS preprocessor
- features: variables, nesting, operators, partials and imports, mixins, functions, extends, control directives
- Two syntaxes:
    - SASS (original): white-space sensitive
    - SCSS ("Sassy" CSS): curly braces to denote blocks

### Lesson 25) First Steps with Sass: Mixins, Extends and Functions

A mixin does not translate into CSS per se; rather, the mixin definition is copied
wherever the mixin is @included:

```scss
@mixin

<
mixin-name >

(
<
args >

)
{
<
mixin
code
;
>
}

@include
<
mixin-name >
```

A function returns a value:

```scss
@function fn-name(args) {
    ...
    @return val;
}
```

extend writes the rules ONCE; copies the extended rule(s) ahead of the single copy.
only use extend if the extended items are related; otherwise, use a mixin

```scss
%extend-name {
    rules;
}

@extend extend-name;
```

### Lesson 28) NPM Scripts: Let's Write and Compile Sass Locally

"scripts": {
"compile:sass": "node-sass sass/main.scss css/style.css -w"
},

### Lesson 29) The Easiest Way of Automatically Reloading a Page on File Changes

$> npm install live-server -g
$> live-server

### Lesson 32) Implementing the 7-1 Architecture with Sass

sass

- abstracts
    - _functions
    - _mixins
    - _variables
- base
- _base
- _animations
- _typography
- _utilities
- components
    - _button
    - et al
- layout
    - _header
    - et al
- pages
    - _home
    - et al

### Lesson 33) Review: Response Design Principles and Layout Types

- Responsive design: makes websites usable on all types of devices
- 4 principles of responsive design:
    - fluid layout: floats, flexbox (1-d layouts), css grid (for 2-d layouts)
        - allows page to adapt to viewport width (and sometimes height).
        - Use %, or vh/vw instead of px for elements that should adapt to viewport
        - use max-width instead of width
    - responsive units
        - use rem instead of px for most lengths
        - makes it easy to scale entire layout up or down automatically
    - flexible images
        - by default, images don't scale automatically as viewport width changes
        - always use % and max-width for image dimensions
    - media queries
        - to change CSS styles on certain viewport widths (called breakpoints)

### Lesson 34) Building a Custom Grid with Floats

- defined a .row class and a bunch of .col- classes.
- .row uses a clearfix.
- .col-* float left.
- CSS calc() function (as opposed to Sass calculation) can mix units.
- Sass calculation computed at compile time.
- CSS calc() computed at render time.

### Lesson 35) Building the About Section - Part 1

- Used linear-gradient background image, -webkit-background-clip and color transparent to display text with a linear
  gradient
- Skew transforms.

### Lesson 36) Building the About Section - Part 2

- http://codingheroes.io/resources

Chapter 37) Building the About Section - Part 3

- Built a composition of 3 images overlapping
- used the "outline" CSS property, including "outline-offset"

### Lesson 38) Building the "Features" Section

- include icon font
    - icons at linea.io
    - Different browsers read different font formats (.eot, .svg, .ttf, .woff)
- Skewed section design
    - another way of achieving the affect achieved in chapter 6 with the clip path property.
- direct child selector ">"

### Lesson 39) Building the "Tours" Section - Part 1

- Used rotateY(), perspective and backface-visibility to animate a card flipping along the vertical axis
- Perspective does not work in current version of Firefox (103.0.2) once absolute positioning is incorporated

### Lesson 40) Building the "Tours" Section - Part 2

- Styled the front of one of the cards in the "Tours" section
- used CSS property "background-blend-mode" to blend background image and linear gradient.

### Lesson 42) Building the Stories Section - Part 1

- agenda:
    - make text flow around shapes with "shape-outside" and "float" properties
    - how to apply a filter to images
    - how to create a background video covering an entire section
    - how to use the `<video>` HTML element
    - how and when to use the "object-fit" property
- Used "shape-outside" property on a figure to flow adjacent text around that figure
    - requires defined dimensions (height, width)
- Used "clip-path" property with circle() function to define which part of the figure should be shown

### Lesson 43) Building the Stories Section - Part 2

- apply transitions to an image on hover.
- "filter" property to blur and darken the image

### Lesson 44) Building the Stories Section - Part 3

- Adding a background video `<video>` element
- autoplay, muted, loop attributes
- instead of the "src" attribute, nest `<source>` elements in the `<video>`
- two video formats to ensure it works in "all" browsers (not IE old)
- "object-fit" property "sets how the content of a replaced element, such as an `<img>` or `<video>`, should be resized
  to fit its container."
- stock video from coverr.co

### Lesson 45) Building the Booking Section: Agenda

- solid-color gradients
- general and adjacent sibling selectors
- ::input-placeholder pseudo-element
- :focus, :invalid, :placeholder-shown and :checked pseudo-classes
- custom radio buttons

### Lesson 45) Building the Booking Section - Part 1

- Used linear-gradient to apply two semi-transparent colors over background image, at an angle
- Laid out a form; no styling yet

### Lesson 46) Building the Booking Section - Part 2

- Initial form styling
- Unlike most elements, "input" elements do not automatically inherit font family. Instead,
  browser applies a default font. Specifying a value of "inherit" for the "font-family"
  property for input elements "corrects" this.
- general sibling selector: '~''
- adjacent sibling selector: '+'
- HTML structured with `<input>` before the <label> to make use of adjacent sibling selector
- input:placeholder-shown + label to style label when the input's placeholder is visible
    - "opacity: 0" - element not visible, but still on the page.
    - "visibility: hidden" - element not on page, but cannot be animated
    - both achieve same effect but with different side effects, both of which are needed.

### Lesson 47) Building the Booking Section - Part 3

- Styling the radio buttons
- Radio buttons cannot be styled, so we have to roll our own
- Hide the input control, but since it is connected to the label, clicking the label still selects the radio button

### Lesson 48) Building the Footer

No new concepts

### Lesson 49) Building the Navigation - Part 1

Animating "solid-color gradients"

- linear-gradient(): progressive transition between two or more colors along a straight line.
- background-size: sets size of element's background image: `contain`, `cover,` length or percentage
- background-position: initial position for the image: `top`, `bottom`, `left`, `right`, `center`, percentage, length

```scss
a {
    &:link, &:visited {
        background-image: linear-gradient(120deg, $color-1 0%, $color-1 50%, $color-2 %50%);
        background-size: 220%;
        transition: background-position .4s;
    }

    &:hover,
    &:active {
        background-position: 100%
    }
}
```

### Lesson 50) Building the Navigation - Part 2

"checkbox hack":

- checkbox or radio button w/ associated label.
- Checkbox `display: none`;
- label still receives click events
- style the `:checked` pseudo class
  Animate the background and nav elements w/ `transition` property

```scss
input[type=checkbox] {
    display: none;

    &:checked ~ {

    }
}
```

custom animation timing functions using cubic bezier curves

- cubic-bezier() function
- _ref: http://cubic-bezier.com_

```scss
&__background {
    transition: transform .8s cubic-bezier(.86, 0, 0.07, 1);
}

&__nav {
    transition: all .8s cubic-bezier(.68, -.55, .265, 1.55);
}

&__checkbox:checked ~ &__background {
    transform: scale(80);
}

&__checkbox:checked ~ &__nav {
    opacity: 1;
    width: 100vw;
}
```

### Lesson 51) Building the Navigation - Part 3

`transform-origin` describes where the transformation happens.
By default transform Happens in the center of the element.

### Lesson 52) Building a Pure CSS Popup - Part 1

How to build a nice popup with only CSS

- How to use the `:target` pseudo-class

**Adjacent boxes with equal height**  
Displaying adjacent elements as "table-cell" will make their heights the same,
regardless of content size.

```scss
parent {
    display: table;

    child {
        display: table-cell; /* These elements behave like <td> HTML elements. */
        vertical-align: middle; /* Or whatever alignment works */
    }
}
```

**CSS text columns**
Use the CSS `column-count` property. Browser will distribute content equally between the columns.

```css
container {
    column-count: 3;
    column-gap: 2rem; /* 1em default */
    column-rule: 1px solid gray; /* a line between columns */
}
```

**Hyphenating words in text content**  
Use the CSS `hyphens` property. Requires `lang` attribute in `<html>` element.

```css
content {
    hyphens: auto;
}
```

### Lesson 53) Building a Pure CSS Popup - Part 2

How to use the `:target` pseudo-class

- an anchor tag uses the ID of an element as its href: eg, `href="#signup-form"`
- when an element becomes a target, the `:target` pseudo-class becomes available:

```scss
&:target {
    ...
}
```

### Lesson 54) Section Intro

Focus on making site responsive.
Covers advanced techniques for responsive design: media queries for screen width, resolution, touch capabilities,
responsive images, feature queries

### Lesson 55) Mobile-First vs Desktop-First and Breakpoints

Media queries: no importance or specificity; conflicts resolved by order: final applicable query takes precedence

**Desktop first**  Optimize for large screen; add media queries for smaller screens (max-width queries)

```css

```

**Mobile first**  Optimize for small screen; add media queries for larger screens (min-width queries)  
Pros:

- forces us to reduce apps to absolute essentials
- smaller, faster, more efficient products
- prioritizes content over aesthetics

Cons:

- desktop version might feel empty, simplistic
- might be more difficult/counter-intuitive
- less creative freedom
- clients might be accustomed to desktop versions for prototypes
- do the app users even use mobile?

- **Selecting Breakpoints**
- bad: select based on the dimensions of the single most populate device in each category
- good: select based on the dimensions of the largest (mobile-first) or smallest (desktop-first) device in each category
- perfect: select based on where your design breaks (but it can be difficult)
- ref: https://gs.statcounter.com/screen-resolution-stats

### Lesson 56) Let's Use the Power of Sass Mixins to Write Media Queries

- Sass mixin to write media queries
- @content and @if Sass directives
- Using Chrome DevTools for responsive design

@content directive passes a block of code to a mixin

Define the mixin with increasing breakpoints for desktop-first,
decreasing breakpoints for mobile-first

```scss
/* $breakpoint argument choices: 
* phone
* tab-port
* tab-land
* big-desktop
*
* 1em = 16px
*/
@mixin respond($breakpoint) {
    @if $breakpoint == phone {
        @media (max-width: 37.5em) {
            @content
        }; // 600px
    }
    @if $breakpoint == tab-port {
        @media (max-width: 56.25em) {
            @content
        }; // 900px
    }
    @if $breakpoint == tab-land {
        @media (max-width: 75em) {
            @content
        }; // 1200px
    }
    @if $breakpoint == big-desktop {
        @media (min-width: 112.5em) {
            @content
        }; //1800px
    }
}
```

Then, where media queries are required, @include the mixin passing the breakpoint as a parameter;
the content of the media query will be passed automatically to the mixin. For example:

```scss
html {
    font-size: 62.5%;
    @include respond(phone) {
        font-size: 50%;
    }
    @include respond(tab-port) {
        font-size: 55%;
    }
    @include respond(tab-land) {
        font-size: 60%;
    }
    @include respond(big-desktop) {
        font-size: 75%;
    }
}
```

### Lesson 57) Writing Media Queries - Base, Typography and Layout

ORDER: Base + typography > general layout + grid > page layout > components
In grid systems, column width is typically set to 100% for smaller screens
since they don't have the horizontal real estate to support multiple adjacent columns.


### Lecture 58) Writing Media Queries - Tours, Stories and Booking Sections
The cards in the Tours section flip over when user hovers over them.  
But touch-screen devices don't have a "hover" state.
So the cards must be styled differently for these devices.
We use media queries to do this.

But for some sections, this will be a huge re-write, not just simply tweaking existing rules.
So we put the whole media query as a separate, stand-alone section,
copying all the original CSS and removing what is not needed.
