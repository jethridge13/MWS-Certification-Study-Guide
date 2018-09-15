# MWS-Certification-Study-Guide

## Table of Contents

* [About](#About)
* [Basic Website Layout and Styling](#Basic)
  * [Responsive Web Design](#ResponsiveWebDesign)
  * [A Complete Guide to Flexbox](#Flexbox)
  * [Using media queries](#MediaQueries)
  * [Video and audio content](#VideoAndAudio)
  * [Responsive Images by Google](#ResponsiveImages)
  * [Supporting both TouchEvent and MouseEvent](#TouchAndMouse)
  * [Touch events](#Touch)
* [Front End Networking](#Front)
* [Accessibility](#A11y)
* [Progressive Web Apps](#PWA)
* [Performance Optimization and Caching](#Perf)
* [Testing and Debugging](#Test)
* [ES2015 Concepts and Syntax](#ES2015)
* [Mobile Web Forms](#Forms)

---

## <a name="About">About</a>
  
This repo is a collection of my personal notes taken while studying for [Google's Mobile Web Specialist Certification exam](https://developers.google.com/training/certification/mobile-web-specialist/).
I am posting it here for several reasons. 

1. Somebody may be searching for information much like I was and may find this information help them in their own decision to take the exam.
2. Posting this on GitHub is a good solution for being able to access my notes remotely and I can track my progress via the commit history.
I can also use the commit history to hold myself accountable to staying consistent.
3. I'm fond of markdown syntax for taking notes.

The topics for the guide are taken from the official study guide found [here](https://developers.google.com/training/certification/mobile-web-specialist/StudyGuide_MobileWebSpecialist.pdf).

---

## <a name="Basic">Basic Website Layout and Styling</a>
### <a name="ResponsiveWebDesign">[Responsive Web Design](https://developers.google.com/web/fundamentals/design-and-ux/responsive/)</a>
 * Design to cover screen sizes of many different devices
  * Always include meta viewport tag
    * Control the width and scaling of the browser’s viewport
    * `width=device-width` to match screen’s width in device-independent pixels
    * `initial-scale=1` establish 1:1 relationship between CSS pixels and device-independent pixels
    * Avoid disabling user scaling for better accessibility
  * Use CSS media queries for responsiveness
    * Use `min-width` over `min-device-width`
    * Use relative sizes
    * `@media` and `media` html attribute
      * Example: `<link rel="stylesheet" href="small-screen.css" media="(min-width: 325px)">`
      * Example: `@media (min-width: 425px) { /* Styles go here */ } `
    * `@import` is possible but discouraged
    * Using `min-device-width` is strongly discouraged.
      * `min-width` is based on browser window. `min-device-width` is screen size. This is often not reported correctly. Also does not support screen resizing.
    * How to choose breakpoints
      * Don't define breakpoints based on device classes
      * Do create breakpoints based on content
      * Design for the smallest screen size you are supporting first
        * Start small and then work up, adding breakpoints as more screen size is added
      * Keep lines of text to 70-80 lines max
      * Pick minor breakpoints when necessary
      * Optimize text for reading
      * *Never* hide content just because you can't fit it on screen
      
### <a name="Flexbox">[A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)</a>
 * Background
   * Give the container the ability to alter its items' width, height, and order to best fill the available space.
 * Basics & Terminology
   * **main axis** - The primary axis along which flex items are laid out. Depends on `flex-direction` property
   * **main-start | main-end** - Items are placed within the container from `main-start` to `main-end`
   * **main size** - The items' width or height, whichever is the main dimension
   * **cross axis** - Perpendicular to the `main axis`
   * **cross-start | cross-end** - Flex lines are filled with items and placed into the container from `cross-start` to `cross-end`
   * **cross size** - The width or height of a flex item, whichever is in the cross dimension
 * Properties for the Parent (flex container)
   * display - `display: flex /* or infline-flex */` Defines a flex container.
   * flex-direction - `flex-direction: row | row-reverse | column | column-reverse;` Establishes the main axis and direction.
     * Default is row, left to right. 
   * flex-wrap - `flex-wrap: nowrap | wrap | wrap-reverse;` Determine overflow properties of the container
     * Default is nowrap, all items will be on one line.
     * wrap will wrap on multiple lines, top to bottom. wrap-reverse is the same except bottom to top.
   * flex-flow - `flex-flow: <'flex-direction'> || <'flex-wrap'>` Shorthand for flex-direction and flex-wrap properties
   * justify-content - `justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly;`
   Determines how the content is spaced along the main axis. Distributes free space.
     * flex-start (Default) Items are packed toward the start line
     * flex-end: Items are packed toward the end line
     * center: Items are centered along the line
     * space-between: Items are evenly distributed in the line, first item on start line, last item on end line
     * space-around: Items are distributed with equal space on both sides.
     * space-evenly: Items are distributed so that the spacing between any two items is equal.
     
   ![justify-content image](https://css-tricks.com/wp-content/uploads/2013/04/justify-content-2.svg)
   * align-items `align-items: flex-start | flex-end | center | baseline | strecth;` Defines how items are laid out along the cross axis on the current line.
     * flex-start (Default) Top margin placed on the cross-start line
     * flex-end: Bottom margin placed on the cross-end line
     * center: Items centered on the cross-axis
     * baseline: Baseline of items aligned
     * stretch: Stretch to fill the container
     
   ![align-items image](https://css-tricks.com/wp-content/uploads/2014/05/align-items.svg)
   
   * align-content `align-content: flex-start | flex-end | center | space-between | space-around | strecth;`
   Defines how extra space in the cross-axis is handled. 
   Has no effect if there is only one line of flex items.
     * flex-start: Lines packed to the start of the container
     * flex-end: Lines packed to the end of the container
     * center: Lines packed to the center of the container
     * space-between: Lines evenly distributed with the first line at the start and the last one at the end.
     * space-around: Lines evenly distributed with equal space around each line
     
   ![align-content image](https://css-tricks.com/wp-content/uploads/2013/04/align-content.svg)
     
 * Properties for the Children
    * order `order: <integer>;` The order in which the item will appear in the list.
    * flex-grow `flex-grow: <number>;` The ratio for how much space the item should take up.
      * Defaults to 0
      * All items set to 1 will attempt to share all space evenly
      * An item with flex-grow of 2 will attempt to take up twice the amount of space as an item using 1
    * flex-shrink `flex-shrink: <number>;` Defines the ability to shrink if necessary. Defaults to 1.
    * flex-basis `flex-basis: <length> | auto;` Defines the default size of an element before the remaining space is distributed.
    
    ![flex-basis image](https://www.w3.org/TR/css-flexbox-1/images/rel-vs-abs-flex.svg)
    
    * flex `flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]` Shorthand for flex-grow, flex-shrink, and flex-basis combined.
    * align-self `align-self: auto | flex-start | flex-end | center | baseline | stretch;` Overrides default alignment set by parent's `align-items` value.
    
  * Prefixing Flexbox
    * Due to evolving Flex spec, prefixes are required to support the widest range of browser.
    * Autoprefixer can manage this automatically    

### <a name="MediaQueries">[Using media queries](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries)</a>

### <a name="VideoAndAudio">[Video and audio content](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Video_and_audio_content)</a>

### <a name="ResponsiveImages">[Responsive Images by Google](https://www.udacity.com/course/responsive-images--ud882)</a>

### <a name="TouchAndMouse">[Supporting both TouchEvent and MouseEvent](https://developer.mozilla.org/en-US/docs/Web/API/Touch_events/Supporting_both_TouchEvent_and_MouseEvent)</a>

### <a name="Touch">[Touch events](https://developer.mozilla.org/en-US/docs/Web/API/Touch_events)</a>
      
## <a name="Front">Front End Networking</a>

## <a name="A11y">Accessibility</a>

## <a name="PWA">Progressive Web Apps</a>

## <a name="Perf">Performance Optimization and Caching</a>

## <a name="Test">Testing and Debugging</a>

## <a name="ES2015">ES2015 Concepts and Syntax</a>

## <a name="Forms">Mobile Web Forms</a>
