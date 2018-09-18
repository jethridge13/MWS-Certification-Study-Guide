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
 * Used to modify site or app depending on a device's general type or specific characteristics
 * Media Type
   * all - Suitable for all devices.
   * print - Intended for page viewed on print preview mode
   * screen - Intended for screens
   * speech - Intended for speech synthesizers
 * Media Features
   * width - Width of viewport
   * height - Height of viewport
   * aspect-ratio - Width-to-height aspect ratio of the viewport
   * orientation - Orientation of the viewport
   * resolution - Pixel density of the output device
   * scan - Scanning process of the output device
   * grid - Grid or bitmap screen?
   * update - Devices update frequency
   * overflow-block - How does the output device handle content that overflows the viewport along the block axis?
   * overflow-inline - Can content that overflows the viewport along the inline axis be scrolled?
   * color - Number of bits per color component of output device
   * color-gamut - Approximate range of colors that are supported by the user agent and output device
   * color-index - Number of entries in the output device's color lookup table
   * display-mode - The display mode of the application as specified in the web app manifest's `display` member
   * monochrome - Bits per pixel in the output device's monochrome frame buffer
   * inverted-colors - Is the user agent or underlying OS inverting colors?
   * pointer - Is the pimrary input mechanism a pointing device?
   * hover - Does the primary input mechanism allow the user to hover over elements?
   * any-pointer - Is any input mechanism a pointing device?
   * any-hover - Does any available input mechanism allow the user to hover elements?
   * light-level - Light level of the environment
   * prefers-reduced-motion - The user prefers less motion on the page
   * prefers-reduced-transparency - The user prefered reduced transparency
   * prefers-contrast - Detects if the user has requested the system increase or decrease the amount of contrast between adjacent colors
   * prefers-color-scheme - Detect if the user prefers a light or dark color scheme
   * scripting - Detects whether scripting is available
 * Logical Operators
   * and - Used for combining multiple media features or joining media features and media types
   * not - Negates a media query
   * only - Used to apply a style only if an entire query matches, useful for preventing older browsers from applying selected styles
   * , - Combine multiple media queries into a single rule
 * Targeting media types
   * `@media print {...}
   * `@media screen, print {...}
 * Targeting media features
   * `@media (hover: hover) {...}`
   * `@media (max-width: 1280px) {...}`
 * Creating complex media queries
   * `@media (min-width: 30em) and (orientation: landscape) {...}`
 * Testing for multiple queries
   * `media (min-height: 680px), screen and (orientation: portrait) {...}`
 * Inverting a query's meaning
   * `@media not all and (monochrome) {...}` is evaluated as `@media not (all and monochrome)) {...}`
 * Improving compatibility with older browsers
   * `only` keyword prevents older browsers that do not support media queries with media features from applying given styles.
   * `@media (only screen and (color)) {...}`
 * Use `not()` around a media feature to negate that feature in the query
 * Test for multiple features with `or`
   * `@media (not (color)) or (hover) {...}`

### <a name="VideoAndAudio">[Video and audio content](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Video_and_audio_content)</a>

 * Audio and video on the web
   * `<audio>` and `<video>` tags introduced in HTML5
 * The `<video>` element
   * Example
     * ```HTML
       <video src="rabbit320.webm" controls>
          <p>Your browser doesn't support HTML5 video. Here is a <a href="rabbit320.webm">link to the video</a> instead.</p> 
       </video>
 
       ```
 
   * src - Path to the video
   * controls - Includes the browser's control interface. If not included, controls must be implemented using the JavaScript API
   * Fallback paragraph - Will be displayed if the browser does not support the `<video>` element
   * Check browser compatiblity with video file type to ensure maximum browser coverage
     * Include multiple sources to ensure compatiblity
     * ```HTML
       <video controls>
        <source src="rabbit320.mp4" type="video/mp4">
        <source src="rabbit320.webm" type="video/webm">
        <p>Your browser doesn't support HTML5 video. Here is a <a href="rabbit320.mp4">link to the video</a> instead.</p>
      </video>
      
      ```
 
   * Other `<video>` features
     * width and height - The width and height of the video player. Aspect ratio is preserved and extra space is given side blackbars.
     * autoplay - Makes the video play upon page load. DON'T USE THIS.
     * loop - Makes the video restart when finished. You should probably avoid this.
     * muted - Starts the video without sound.
     * poster - The video thumbnail that is displayed before the video plays
     * preload - `none | auto | metadata` - Enable buffering for the video
 * The `<audio>` element
   * Basic behavior is the exact same as the `<video>` element
   * Does not support width/height, poster attributes
 * Displaying video text tracks
   * `<track>` used to include subtitle information in WebVTT files
   * `<track kind="subtitles | captions | descriptions" src="example_en.vtt" srclang="en">`

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
