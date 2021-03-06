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
  * [Introduction to fetch()](#IntroToFetch)
  * [Using fetch](#UsingFetch)
  * [David Walsh's blog on fetch](#Walsh)
  * [Jake Archibald's blog on fetch](#ArchibaldFetch)
  * [JavaScript Promises: an Introduction](#Promises)
  * [HTTP access control (CORS)](#CORS)
* [Accessibility](#A11y)
  * [Web Fundamentals - Accessibity](#A11yFundamentals)
  * [Web Accessibility](#UdacityA11y)
  * [Mobile Accessibility](#MobileA11y)
  * [Using tabindex](#TabIndex)
  * [Focus](#Focus)
  * [Skip Navigation Links](#SkipNavLinks)
  * [ARIA](#ARIA)
* [Progressive Web Apps](#PWA)
  * [Progressive Web Apps](#PWAOverview)
  * [Progressive Web Apps Training](#PWATraining)
  * [Web Fundamentals - The App Shell Model](#AppShellModel)
  * [Your First Progressive Web App](#FirstPWA)
  * [Using Service Workers](#SW)
* [Performance Optimization and Caching](#Perf)
  * [Using Web Workers](#WebWorkers)
  * [Offline Web Applications by Google](#GoogleOfflineWebApps)
  * [Web Fundamentals - Performance](#PerformanceFundamentals)
  * [The Offline Cookbook](#OfflineCookbook)
  * [Cache - MDN](#Cache)
  * [Storage](#Storage)
  * [Local Storage And How To Use It On Websites](#LocalStorage)
  * [IndexedDB API](#IndexedDB)
  * [Get Started with Analyzing Network Performance in Chrome DevTools](#DevTools)
* [Testing and Debugging](#Test)
  * [Get Started with Debugging JavaScript in Chrome DevTools](#JSDevTools)
  * [Diagnose and Log to Console](#Console)
  * [Debugging Service Workers](#DebugSW)
* [ES2015 Concepts and Syntax](#ES2015)
  * [JavaScript Promises: an Introduction](#ES6Promises)
  * [Promise](#Promise)
  * [Template literals](#TemplateLiterals)
  * [Arrow Functions](#ArrowFunctions)
  * [Default Parameters](#Defaults)
  * [For...of](#ForOf)
  * [Map](#Map)
  * [Set](#Set)
* [Mobile Web Forms](#Forms)
  * [Create Amazing Forms](#AmazingForms)
  * [Constraint Validation](#ConstraintValidation)
  * [Client-Side Form Validation with HTML5](#ClientSideValidation)
  * [Data form validation](#DataFormValidation)
  * [HTML Forms](#HTMLForms)

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
Users expect responsive and visually engaging websites regardless of the device. A web
application's layout and styling must respond to the current display, while continuing to provide
intuitive functionality. You'll be asked to show you can use HTML, CSS, and JavaScript to build
a web application’s responsive layout and style that includes:
* DOM elements that are accessed and manipulated using only JavaScript without the
overhead of libraries or frameworks (such as jQuery)
* Appropriate document type declaration and viewport tags
* A responsive grid-based layout using CSS
* Media queries that provide fluid breakpoints across different screen sizes
* Multimedia tags to display video or play audio
* Responsive images that adjust for the dimensions and resolution of any mobile device
* Touch and mouse events that contain large hit targets on the front end and work
regardless of platform
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
Note: These notes are my notes taken while taking the Mobile Web Specialist Nanodegree course by Udacity, which includes these courses as part of the program.
* Landscape and Portrait
  * “Don’t assume the viewport size will always stay the same”
* Less Well Known CSS Units
  * vh - viewport height - 100vh = 100% height
  * vw - viewport width
  * vmin - viewport height or width, whatever is less
  * vmax - viewport height or width, whatever is greater
* Raster and Vector
  * Raster - photographs and other images in pixels
  * Vector - Adobe illustrator, vector graphics, svg
  * Vector image can be any size
* Quiz: Raster or Vector Banner?
  * Answer: Vector - scales without quality degredation
* Quiz: Raster and Vector Identification
  * Answer: 
    * Chrome Logo: Vector
    * Kitten Photo: Raster
    * Flag of Mexico: Vector
    * Repeated Background: Vector
    * Gradient Background: Vector
* File Formats
  * JPEG - Artifacting along edges
    * Use for pictures
  * Vector - smaller file sizes
    * Use whenever possible
    * If not possible, use PNG
* Quiz: Spot the Differences
  * Answer: Actual (natural) size
  * Avoid sending images that have resolutions higher than their display resolution
    * Caveat: High DPI displays, future lesson
* Quiz: Spot the DIfferences 2
  * Answer: Compression Level
* Image Compression
  * PageSpeed Insights - Google Dev benchmarker
    * Can even use in terminal
  * Grunt-pagespeed also available
* Quiz: Project Part 1
  * Responsive Blog Project Part 1
  * Code notes
    * Set body max-width to 800px, img max-width to 100%
    * Gruntfile set images to 800px, quality 50
* Performance
  * Aim to reduce the number of image requests
  * Need to reduce file sizes and number of requests
* Text Problems
  * Text and graphics - overlay text on pictures if necessary
  * Use fonts to have good design without graphics
* CSS Techniques
  * CSS for shadows
  * Gradients
  * Rounded corners
  * Animations
  * Processing and rendering cost for cool effects, take into consideration
* CSS background images
  * CSS as background to avoid using a big image
  * CSS transition to resize image cropping
  * Display images based on viewport size
* Quiz: CSS background image techniques
  * Answer
    * Cover: The image is sized so that it is as small as possible while still completely filling its container.
    * Contain: The image is sized so that it is as large as possible while still being completely visible inside its container.
* Symbol characters
  * Use symbols from fonts instead of images
* Quiz: Unicode Treble Clef
  * Charset must be set to UTF-8 to use unicode character set
  * Answer: &#119070; (Treble clef HTML code)
  * Copy and paste the symbol instead of the code when possible - easier supported
* Icon Fonts
  * Zocial - icon font
  * Fonts which are just lists of symbols
  * Resizable, recolorable, reshadowable
* Inlining images with SVG and data URIs
  * SVG are awesome
  * Data-URI: inline included image
  * Crazy code but reduces HTTP requests
* Quiz: Strategy Quiz 1
  * Answer: vector, external or inline
    * Inline because shape is simple
    * External because it can be reused and cached
* Quiz: Strategy Quiz 2
  * Answer: .jpg, inline or external
    * Inline reduces requests
* Quiz: Strategy Quiz 3
  * Answer: Vector, external
    * External for use on multiple pages, caching
* Quiz: Strategy Quiz 4
  * .svg, external
* Quiz: Project Part 2
  * utf-8 must be all lower case in meta tag
  * Weloveiconfonts.com imported in CSS
* Srcset
  * srcset - alternate photo serving based on variable
  * window.devicePixelRatio
  * If srcset isn’t supported, uses default src instead
  * W unit - use this picture based on this width
* Sizes Attribute
  * Browser does not know image display size - CSS is parsed after request
  * Sizes attribute tells the browser the image display size
  * Sizes attribute can include media query-like variables
* Quiz: srcset Quiz
  * srcset using Device Pixel Ratio
    * `<img src=”src_path” srcset=”src_path nx, …”>` where n is the DPR
    * `<img src="image_2x.jpg" srcset="image_2x.jpg 2x, image_1x.jpg 1x" alt="a cool image">`
    * src is included as a fallback
  * srcset using Image Width
    * `<img src=”src_path” srcset=”src_path nw, …”>` where n is the width of the image in pixels
    * `<img src="image_200.jpg" srcset="image_200.jpg 200w, image_100.jpg 100w" alt="a cool image">`
    * src is included as a fallback
* Quiz: srcset and sizes
  * Use the sizes tag like a media query to tell the browser how the image will be displayed relative to the viewport width
  * ```HTML 
  
      <img  src="images/great_pic_800.jpg"
      sizes="(max-width: 400px) 100vw, (min-width: 401px) 50vw"
      srcset="images/great_pic_400.jpg 400w, images/great_pic_800.jpg 800w"
      alt="great picture">
      
    ```
    
  * sizes defaults to 100vw if not found
  * Answer note: Second media query note required because defaults to 100vw if not specified
* The Picture Element
  * Picture element can provide alternate sources for image files depending on browser support
    * For example, webp and jpeg files
  * Include img element inside picture element as a fallback
* The Full Monty
  * Picture element can be used with media queries
  * Picturefill polyfill adds in srcset and other cool things
* Accessibility
  * Use alt tags for support with screen readers
* Quiz: Accessibility Promise
  * Responsibility matters!
* Quiz: Project Part 3
  * Different crops for different browser widths
  * Picture element has two children: source and img, img is always last, is fallback
  * source can use srcset

### <a name="TouchAndMouse">[Supporting both TouchEvent and MouseEvent](https://developer.mozilla.org/en-US/docs/Web/API/Touch_events/Supporting_both_TouchEvent_and_MouseEvent)</a>

* Event firing
  * The browser may fire both touch events and mouse events in response to the same user input
  * If the browser fires both touch and mouse events because of a single user input, the browser *must* fire a `touchstart` event before any mouse events.
    * Calling `preventDefault()` in a touch handler will thus prevent event propagation and stop the mouse event
* Event order
  * The following order is typical, according to standard
    * `touchstart`
    * `touchmove` (if applicable)
    * `touchend`
    * `mousemove`
    * `mousedown`
    * `mouseup`
    * `click`
  * If `touchstart`, `touchmove`, or `touchend` is cancelled during an interaction, no mouse or click events will be fired.
  Thus, the sequence of events would be as follows:
    * `touchstart`
    * `touchmove` (if applicable)
    * `touchend`

### <a name="Touch">[Touch events](https://developer.mozilla.org/en-US/docs/Web/API/Touch_events)</a>

* Definitions
  * Surface - The touch-sensitive surface.
  * Touch point - A point of contact with the surface.
* Interfaces
  * TouchEvent - An event that occurs when the state of touches on the surface changes
  * Touch - Represents a single point of contact between the user and the touch surface
  * TouchList - A group of touches, used when multiple touches are active at once (For example, using multiple fingers)
* Start handler with `touchstart` event
* Handle movement with `touchmove` event
* End handler with `touchend` event
* `touchcancel` sent when handle event hits other UI or otherwise needs to be cancelled
* Link contains significant code examples and it is recommended to follow the full example
      
## <a name="Front">Front End Networking</a>

Because user engagement depends on reliable and effective network requests, you'll be asked
to show you can use JavaScript to set up reliable front end networking protocols by:
* Requesting data using `fetch()`
* Checking response status, then parsing the data into usable format
* Rendering response data to a page
* Configuring POST requests to a database with `method` and `body` parameters
* Using correctly configured cross-origin resource sharing protocol (CORS) fetch requests,
depending on the server's response headers
* Handling `fetch()` request errors with promise chaining
* Diagnosing network issues using debugging and development tools

Note: There is much overlap in what the sources cover. To avoid redundant notes, each new section will only include new content.

### <a name="IntroToFetch">[Introduction to fetch()](https://developers.google.com/web/updates/2015/03/introduction-to-fetch)</a>

* `fetch()` is so much better than XMLHttpRequest please never use XMLHttpRequest ever again
* [Link to polyfill](https://github.com/github/fetch)
* Basic request
  * `fetch('url').then(response => response.json()).then(data => console.log(data))`
  * Handle the response with a promise
  * Response could also have an error, so add a `.catch()` to the end
* [Response object](https://fetch.spec.whatwg.org/#responses)
  * headers, status, statusText, type, url, etc.
* Mode
  * Define a mode such that only certain requests will resolve
  * same-origin - Only succeeds if request is of the same origin
  * cors - will allow requsts for assets on same-origin and cross-origin
  * cors-with-forced-preflight - Will perform a preflight check before making the request
  * no-cors - Make requests to other origins that do not have CORS headers for an `opaque` response. Probably ignore this, not implemented in the window gloabl scope.
  * `fetch('example.com', {mode: 'cors'})`
* POST Request
  * `fetch(url, method: 'post', headers: { "Content-type": "application/x-www-form-urlencoded; charset=UTF-8" }, body: 'foo=bar'})`
* Sending Credentials with a Fetch Request
  * Used for sending a request with credentials such as cookies
  * `fetch(url, { credentials: 'include' })`
* FAQ
  * How do I cancel a fetch() request?
    * Currently, you can't but it is being discussed
  * Is there a polyfill?
    * [Yes!](https://github.com/github/fetch)
  * Why is "no-cors" supported in service workers but not the window?
    * Security concern. More info [here](https://bugs.chromium.org/p/chromium/issues/detail?id=457157&q=fetch%20no-cors&colspec=ID%20Pri%20M%20Week%20ReleaseBlock%20Cr%20Status%20Owner%20Summary%20OS%20Modified)
 
### <a name="UsingFetch">[Using fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)</a>

* Differences between `fetch()` and `jQuery.ajax()`
  * `fetch()` won't reject on HTTP error status. Will resolve normally with `ok` set to `false`
  * `fetch()` won't send or receive cookies from the server by default.
* Uploading JSON data
  
  ```JavaScript
  fetch(url, {
  method: 'POST',
  body: JSON.stringify(data0, // data can be string or object
  headers: { 'Content-Type': 'application/json' }})
  ```
  
* Files can be uploaded by appending a file input to a form and then submitting that
* A `Request()` object can be used as the `fetch()` argument instead of a url
* A `Headers()` object can also be used
  * Guard - A guard can be set on the header to restrict the immutability
    * none - default, allow maximum amount of mutability
    * request - guard for a headers object obtained from a request (`Request.headers`)
    * request-no-cors - guard for a headers object obtained from a `Request.mode-no-cors` request
    * response - guard for a Headers obtained from a response (`Response.headers`)
    * immutable - Used for service workers, read-only
* Response objects
  * `Response.status` - The HTML response code (integer)
  * `Response.statusText` - The response status string that corresponds to the status code
  * `Response.ok` - `true` if response is in the 200 range signifying a successful request, otherwise `false`
* `fetch()` can be detected for browser compatiblity by checking for `Headers`, `Request`, `Response`, or `fetch()` on the `Window` or `Worker` scope.
This can be useful for detecting when to add the polyfill.

### <a name="Walsh">[David Walsh's blog on fetch](https://davidwalsh.name/fetch)</a>

* Customizing Request - the following options can be included in the `fetch()` call
  * method - `GET`, `POST`, `PUT`, `DELETE`, `HEAD`
  * url - URL of the request
  * headers - associated `Headers()` object
  * referrer - referrer of the request
  * mode - `cors`, `no-cors`, `same-origin`
  * credentials - should cookies be included? `omit`, `same-origin`
  * redirect - `follow`, `error`, `manual`
  * integrity - subresource intergrity value
  * cache - cache mode (`default`, `reload`, `no-cache)
* Extra Response methods 
  * `clone()` - Creates a clone of the Response
  * `error()` - Returns the error associated with the Response object
  * `redirect()` - Creates a new response with a different URL
  * `arrayBuffer()` - Returns a promise that resolves with an ArrayBuffer
  * `blob()` - Returns a promise that resolves with a Blob
  * `formData()` - Returns a promise that resolves with a FormData object
  * `json()` - Returns a promise that resolves with a JSON object
  * `text()` - Returns a promise that resolves with a USVString


### <a name="ArchibaldFetch">[Jake Archibald's blog on fetch](https://jakearchibald.com/2015/thats-so-fetch/)</a>

* Can get access to the low-level body stream
* Streaming data from the response drains the stream, and thus cannot be read again
  * This is why the response needs to be cloned if wanting to perform more operations on it after calling `.json()` on it
* What's missing?
  * Request aborting - potentially fixable
  * Progress events
  * Synchronous events - Are not included and never will be because sync requests are awful

### <a name="Promises">[JavaScript Promises: an Introduction](https://developers.google.com/web/fundamentals/primers/promises)</a>

* Terminology
  * fulfilled - The action relating to the promise succeeded
  * rejected - The action relating to the promise failed
  * pending - The promise has neither been fulfilled or rejected yet
  * settled - The promise as either been fulfilled or rejected
* Basic syntax
  * Declaring a promise
  
    ```
    var promise = new Promise(function(resolve, reject) {
      // do a thing, possibly async, then…

      if (/* everything turned out fine */) {
        resolve("Stuff worked!");
      }
      else {
        reject(Error("It broke"));
      }
    });
    ```
  
  * Using a promise

    ```
    promise.then(function(result) {
      console.log(result); // "Stuff worked!"
    }, function(err) {
      console.log(err); // Error: "It broke"
    });
    ```

* [There is a polyfill! (Although major support has already arrived)](https://github.com/stefanpenner/es6-promise#readme)
* Chaining
  * Call `then()` at the end of another `then()` function to chain promises together
  * The subsequent promise will receive the return value from the previous promise
* Error handling
  * The second function argument is used when handling errors
  * `catch()` can be used to catch errors
  * This method can be used instead of calling a promise with 2 arguments
* More Advanced Syntax
  * `Promise.resolve()` will return a promise that always resolves with the given value
  * `Promise.reject()` will return a promise that always rejects with the given value
  * `Promise.all()` takes an array of promises that fulfills when all of them succuessfully complete

### <a name="CORS">[HTTP access control (CORS)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)</a>

* Cross-Origin Resource Sharing allows a web application running at one origin to have permission to access selected resource from a server at a different origin
* Browsers restrict cross-origin HTTP requests intiated from within scripts
* Functional overview
  * Adds new HTTP headers that allow servers to describe a set of origins that are permitted to read that information using the browser
* Examples of access control scenarios
  * Simple requests do not trigger the CORS preflight request, such as GET requests
  * Preflighted requests
    * An OPTIONS request is sent to confirm the actual request is safe to send
      * PUT, DELETE, CONNECT, OPTIONS, TRACE, PATCH can trigger preflight requests
   * Requests with credentials
     * By default, cross-site requests will not send credentials. A specific flag must be set
* The HTTP response headers
  * Access-Control-Allow-Origin
    * Returns either a single, specified origin or "*" for any origin
      * "\*" wildcard cannot be returned with credentials
  * Access-Control-Expose-Headers
    * The server whitelists headers that are exposed to the browser
  * Access-Control-Max-Age
    * Indicates how long the results of a preflight request can be cached
  * Access-Control-Allow-Credentials
    * Indicates if the request can be made using credentials
  * Access-Control-Allow-Methods
    * Indicates the methods allowed when accessing the resource
  * Access-Control-Allow-Headers
    * Indicates the headers allowed when making the request
* The HTTP request headers
  * Origin
    * Indicates the origin of the cross-site access request or preflight reqeuest
  * Access-Control-Request-Method
    * Used in the preflight request to let the server know what method the actual request will use
  * Access-Control-Request-Headers
    * Used in the preflight request to let the server know what headers the actual request will use

## <a name="A11y">Accessibility</a>

Web pages and applications should be accessible to all users, including those with visual,
motor, hearing, and cognitive impairments. Using HTML, CSS, JavaScript, you'll be asked to
show you can integrate accessibility best practices into your web pages and applications by:
* Using a logical tab order for tabbed navigation
* Using skip navigation links to bypass navbars and asides
* Avoiding hidden content on the page that impedes tab navigation
* Using heading tags that provide a logical page structure
* Using text alternatives to visual content, such as alt, <label>, aria-label, and
aria-labelledby
* Applying color contrast to all elements and following accessibility best practices
* Sending timely alerts for urgent messages using aria-live
* Using semantic markup to keep content and presentation separate when appropriate

### <a name="A11yFundamentals">[Web Fundamentals - Accessibility](https://developers.google.com/web/fundamentals/accessibility/)</a>

* What is accessibility?
  * Broad definition: A site's content and functionality can be operated by *anyone*
  * Accessiblity includes non-physical and temporary impairments
* Web Content Accessibility Guidelines
  * [Web Content Accessibility Guidelines](https://www.w3.org/TR/WCAG20/)
  * POUR and the [WebAIM (Web Accessibility in Mind) Checklist](https://webaim.org/standards/wcag/checklist)
  * Perceivable - Can users perceive the content?
  * Operable - Can users use UI components and navigate the content?
  * Understandable - Can users understand the content?
  * Robust - Is the content cross-browser compatible? Does it work with assistive technologies?
* Understanding users' diversity
  * Four main impairments - visual, motor, hearing, cognitive
  * Visual
    * Screen reader, braille reader, or a combination of both could be used to navigate the site
    * Visual includes blindness, low-vision, color blindness/poor color vision, and even stuff like glare on the screen
  * Motor
    * User could be paralyzed and not have access to a mouse or could have a broken wrist or could simply prefer to use the keyboard
  * Hearing
    * Deaf, hard-of-hearing, or loud background environment
  * Cognitive
    * ADD, Dyslexia, Autism, etc.

### <a name="UdacityA11y">[Web Accessibility](https://www.udacity.com/course/web-accessibility--ud891)</a>
Note: These notes are my notes taken while taking the Mobile Web Specialist Nanodegree course by Udacity, which includes these courses as part of the program.

* Introduction to Focus
    * Using the keyboard to drive page functionality
* What is Focus?
  * Tab - move focus forwards
  * Shift + Tab - move focus backwards
  * Arrow keys - move focus between option elements
  * Tab Order -  order in which elements are focused
  * Implicitly focusable - elements which are implicitly tab ordered, usually input elements
* DOM Order Matters
  * Implicit Tab Order is determined by HTML order
  * WebAIM 1.3.2 - Meaningful Sequence
    * The reading and navigation of tab order should be logical
* Quiz: Fixing DOM Order
  * Move elements around in the HTML so they make sense
* Using Tabindex
  * Attribute to manually set tab order
  * -1 - Not in natural tab order but can be focused with focus()
  * 0 - In tab order, can be programmatically focused
  * >0 - in the tab order, jumped to the front of the tab order. ANTI-PATTERN
* Deciding what’s in focus
  * Only add focus behavior to interactive controls
* Quiz: Which Element Should Have Focus?
  * Elements that are interactable should have focus
* Managing Focus
  * Don’t add tab index to site content unless the page is manipulated in response to user action
* Skip Links
  * A link that jumps straight to main content
    * Skips ahead of navbars and other things to get straight to the important stuff
  * Can hide skip link offscreen until it’s focused
* Focus in Complex Components
  * ARIA Design Patterns lists keyboard interactions with components
* Keyboard Design Patterns
  * Roving focus - changing focus between items in an input group
* Offscreen Content
  * Accessibility Dev Tools extension - adds audits for accessibility
  * Display: none or visibility: hidden to hide offscreen
    * Display: block and visibility: visible to bring back
* Modals and Keyboard Traps
  * Keyboard trap - focus is stuck on input
  * Modals want to keep focus though - want temp keyboard trap
  * Lots of good code here talking about keyboard traps for modals, reference this later
* Assistive Technology
  * Devices, software, and tools that help any person with a disability complete a task
* Affordances
  * Cues based on previously encountered objects - such as handle on a kettle and handles on mugs and various other things with handles
* Semantics and Assistive Technologies
  * For all user interface components, the name and role should be able to be programmatically determined
* Quiz: Experience Using a Screen Reader
  * I am glad I have fully functional eyes
* Role, Name, Value
  * Role, Name, State, Value - what the screenreader should be able to dictate to the user
* The Accessibility Tree
  * The browser takes the DOM tree and modifies it for screen readers
* Semantics in Native HTML
  * Implicit Semantic Meaning - The DOM uses standard HTML elements that work in predictive ways
* Writing Semantic HTML: The Name Game
  * Provide text-alternatives for non-text content
  * Labels - visible and text-alternative
  * Make sure input elements have labels
* Text Alternatives
  * Alt text only used if image isn’t available
  * Alt text should convey same meaning of image
  * Empty alt text skips content
* Navigating with a screen reader
  * Headings are very valuable for screen readers
* Using Headings
  * DOM order matters for heading order
  * Headings can be placed outside screen for use with screen readers, but should be used carefully
* Quiz: Using Headings
  * Don’t rely on headings to style size. Use CSS for that. Use headings for importance
* Other navigational options example
  * Can navigate by links only
  * Can navigate by form controls
* Link Text
  * Link anti-patterns
    * Don’t use span links or `<a>` with href
      * Always use hrefs
    * Don’t use links when buttons should be used
    * If using images for links, make sure the image has alt text
  * Links should be described by the link text alone
* Landmarks
  * Elements that are used to designate content based on context
    * Main
    * Header
    * Footer
    * Nav
    * Article
    * Section
    * Aside
* Outro Lesson 4
  * Meaningful headings and good page structure
  * Don’t try to control the experience of a screen reader
* Why ARIA
  * Web Accessibility Initiative - Accessible Rich Internet Applications
  * Specify attributes on elements that change how elements are translated into the accessibility tree
  * role and aria-checked attributes, for example, to make a checkbox
  * ARIA attributes always need explicit values
* What can ARIA do for you?
  * Create custom widgets for accessibility
  * Express relationships between elements
* Roleplaying
  * Role and tabindex on same element for tabbing through elements
  * Roles - various elements that can be used in the DOM
  * ARIA spec for more info
* More Ways to Label
  * label, labelledby, describedby
  * aria-label
    * Label for the role of an element, like “Close” or “Menu”
  * aria-labelledby 
    * Refer to another element in the DOM by id to be used as the label
    * Overrides all other namespaces
* Default Semantics and Landmarks
  * Don’t redefine default semantics
    * input with type checkbox already has a role
    * Exception: if default semantics aren’t defined
* ARIA Relationships
  * aria-owns 
    * Assigns parent with more children for other elements that aren’t children in the DOM
  * aria-activedescedant
    * When parent has focus, put focus on this element instead
  * aria-describedby 
    * Description used in the same fashion as aria-labelledby
  * aria-posinset and aria-setsize
    * Defines relationships between sibling elements in a set
    * setsize describes actual size of set
    * posinset describes position in set
* Hidden In Plain Sight
  * Anything hidden will not be displayed in accessibility tree
  * Not visually rendered but not hidden still in accessibility tree
    * Also used with aria-label and other aria attributes
  * aria-hidden removes element and descendant from accessibility tree
* Introducing ARIA Live
  * aria-live: give live update in similar way as a visual experience would have
    * off, polite, and assertive
  * Live-region should be in initial page load
* Atomic Relevant Busy
  * aria-atomic
    * Consider entire live region for live updates
  * aria-relevant	
    * Describe what content should be read on updates
  * aria-busy
    * Temporarily ignore changes to this element for live updates
* Working with focus styles
  * What page element has focus should be visibly apparent
  * focus pseudo class only applies when the element has focus
  * NEVER remove focus ring completely
  * hover pseudo class also useful
* Input Modality
  * Certain elements have special behavior for focus styles
    * Buttons do not have focus styling for when clicking but do when tabbing
* Styling with Aria
  * Use CSS attribute selector for when attribute is set
    * Visually confirms Aria attributes
* Responsive design for multi-device Pt. 2
  * Zoom can trigger mobile sites, which is better for reading when super-zoomed
  * Don’t forget the viewport tag
  * Use ems and rems for text for better text scaling
  * Ensure margins around icons as well
* Meeting Contrast Requirements
  * Minimum contrast ratio of 4.5:1 for text
    * Large text can be 3:1
  * Enhanced text and images should have 7.5:1
  * Chrome has built-in accessibility auditing
* Don’t convey info with color alone
  * Always provide multiple avenues to convey important information
  * Color shouldn’t be used to distinguish links alone
  * NoCoffee - accessibility testing tool for color and visual impairments
* High Contrast Mode
  * Invert background and foreground colors
  * Verify that UI is still usable in high contrast
* Course Outro
  * Impact - most impact with least effort
    * How frequently is this piece of UI used?
    * How badly does this issue affect your users?
    * How expensive is it going to be to fix?
  * Good accessibility is good UX

### <a name="MobileA11y">[Mobile Accessibility](https://developer.mozilla.org/en-US/docs/Learn/Accessibility/Mobile)</a>

* Accessibility on mobile devices
  * Mobile devices now have screenreaders and other accessibility tool support
  * Following a11y best practices will get you the majority of the way to a fully accessible mobile site
  * Exceptions:
    * Control mechanisms - Ensure interface controls (such as buttons) are accessible on mobile
    * User input - Ensure user input requirements as painless as possible (e.g. in forms. Typing in forms on mobile is a pain)
    * Responsive design - Ensure layout works on mobile and users can still access ALL content
* Summary of screenreader testing on Android and iOS
  * Most common mobile platforms have fully functional screenreaders
* Control mechanisms
  * `mousedown` and `mouseup` cannot be activated on mobile while `click` can. Use `click` events for cross-compatibility
  * If you must use mouse events, include an equivalent such as `ontouchstart` and `ontouchend`
* Responsive design
  * Responsive design is the practice of making your layouts and other feature of your apps dynamically change depending on factors such as screen size and resolution
  * Most common problems
    * Suitable layouts. For example, multi-column layouts don't work on mobile and should be addressed by using technologies such as flexbox
    * Conserving image sizes downloaded. Small screens usually need smaller images. Mobile devices also are usually on slower connections and smaller images will load faster
    * Thinking about high resolutions. Mobile devices have high resolutions for their small screen sizes. Use SVG vector graphics where possible to maximize resolution and file size requirements.
  * Specific mobile considerations
    * Don't disable zoom
    * Keep menus accessible - Don't remove the menu; hide it and reveal it when the user prompts for it by using techniques such as the hamburger menu
* User input
  * Try to use as minimal typing into inputs as possible
  * Instead of universal text fields, consider a `select` element with an "Other" option which enables a text field
  * Mobile devices often have custom widgets for various input types, such as `time` and `date`

### <a name="TabIndex">[Using tabindex](https://developers.google.com/web/fundamentals/accessibility/focus/using-tabindex)</a>

* The `tabindex` HTML attribute can be used to change the order in which elements are tabbed through
* `tabindex="0"` inserts an element in the natural tab order
* `tabindex="-1"` removes an element from the natural tab order but can still be focused with `focus()`
* Any tab index greater than 0 jumps the element to the front of the natural tab order.
  * If there are multiple elements with a tab index above 0, the tab order starts from the lowest value greater than zero and then works up
  * THIS IS AN ANTI-PATTERN
* If the element is not interactable, don't worry about tab index. Screenreaders can still understand it.
* Managing focus at the page level
  * Managing focus is particularly helpful when working on a single page that has some content hidden and becomes visible
* Managing focus in components
  * When creating custom components, managing focus is key
  * [Accessible Rich Internet Applicaions (ARIA) Authoring Practices)[https://www.w3.org/TR/wai-aria-practices/] contains guidelines for creating custom components
* Modal and keyboard traps
  * Keyboard focus should never be locked or trapped at one particular page element
  * Exception to the above: modal windows
  * Create a keyboard trap for a modal by creating a loop of the focusable elements in the modal.
    * When the user requests to tab to an element at the last focusable element in the modal, add focus to the first element in the modal. 
    * Add an event listener for "Esc" to close the modal. This creates a better user experience

### <a name="Focus">[Focus](https://developers.google.com/web/fundamentals/accessibility/focus/)</a>

* Focus refers to which control on the screen currently receives input from the user
* Elements that are focused will be visually represented as such
* What is focusable?
  * Interactive elements (such as inputs) are *implicitly focusable*, that is, they are automatically inserted into the tab order.

### <a name="SkipNavLinks">[Skip Navigation Links](https://webaim.org/techniques/skipnav/)</a>

* Overview
  * A Skip Navigation Link is a link that is the first tabbable item that, when clicked, will skip over all navigation content and get straight to the main content.
  * Skip nav links are useful for getting around all of the header links and navigation content at the beginning of a site
  * Especiially useful for keyboard-only navigation
* Creating "Skip Navigation" Links
  * Visible links at the top of the page
    * Add a visible link to the list of nav items
    * Important that the link is the first or one of the very first links on a page
    * Method works well but can be intrusive to visual design or overall confusing
  * Invisible links
    * Place the link in the DOM but hide it offscreen until it is focused
    * Could be easily skipped so is important to make the skip link easily visible once selected
* Browser Quirks
  * Some browsers may not fully support skip links but can be created using `focus()`
* Multiple "Skip" Links
  * One or two skip links are useful. Any more could be overbearing
  * HTML5 section elements and ARIA landmarks can also help avoid the need for multiple skip links
* Alternatives to "Skip Navigation" Links
  * Navigating by headings
    * A page filled with useful headings can be a better alternative for screenreader users
  * Alternate reading orders
    * Put nav links at the bottom of the DOM and use CSS to place it at the top
    * Becomes an issue when screenreader users want to use the nav links

### <a name="ARIA">[ARIA](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA)</a>

* ARIA - Accessible Rich Internet Applications - a set of attributes that define ways to make the internet accessible to everyone
* If there is a choice between the ARIA implementation and the HTML5 implementation, use the HTLM5 implementation
  * The HTML5 standard includes many of the necessary a11y features that ARIA provides
  * If you do use ARIA, it is your responsibility for maintaining the correct a11y behavior
* ARIA attributes describe behavior of components so a11y technologies such as screenreaders can help users use the site
* An overview of accessible web applications and widgets
  * The problem
    * Dynamic content on a web page modify the DOM in ways that assistive technology may not be aware of
    * ARIA helps solve this
  * ARIA
    * Roles - describe widgets that aren't otherwise available in HTML4 such as sliders, menu bars, tabs, and dialogs
    * Properties - describe characteristics of the aforementioned widgets such as if they are draggable or have an associated popup
    * State - describe the current interaction state of an element such as disabled, selected, or hidden
  * Presentational changes - Changing the appearance of content
    * State changes
      * Declaring the current state of a UI widget
      * [Full list of ARIA states](https://www.w3.org/TR/wai-aria-1.1/#introstates)
    * Visibility changes
      * Set `aria-hidden` when an element is hidden or shown
  * Role changes
    * Declare a semantic role for an element that otherwise does not have one
    * The role of an element should not change
  * Keyboard navigation
    * All features of a web application or widget should be controllable with the keyboard

## <a name="PWA">Progressive Web Apps</a>

Users expect native applications to be available offline and provide a feature-rich experience
that is launchable from their home page. You'll be asked to show that you can use service
workers, and HTML and JavaScript to build out progressive web application features similar to
native applications by:
* Creating a web app that is available offline, and that caches elements by routing
requests through a service worker
* Storing the default display orientation, theme color, display icon (add to home screen),
and splash screen in the web application manifest (or using meta tags)
* Separating critical application functionality and UI into an application shell that can be
loaded independently from the content

### <a name="PWAOverview">[Progressive Web Apps](https://developers.google.com/web/progressive-web-apps/)</a>

* Progressive Web Apps are user experiences that have the reach of the web and are:
  * Reliable - Load instantly and never show an offline error even when offline or with slow internet
  * Fast - Respond quickly to user interactions with no jank
  * Engaging - Feel like a natural app on the device with an immersive user experience
* Reliable - When launched from the user's home screen, the PWA loads instantly regardless of network state
* Fast - The site loads quickly and once loaded, navigating the site is responsive and quick-to-respond
* Engaging - Installable on the user's home screen without an app store and can even use push notifications
* Why build a PWA?
  * Increased engagement
  * Work reliably no matter the network conditions
  * Improve conversions

### <a name="PWATraining">[Progressive Web App Training](https://developers.google.com/web/ilt/pwa/)</a>

Note: This section is *very* in-depth. It is recommended instead to follow along with the tutorial to cover all of the material.

### <a name="AppShellModel">[Web Fundamentals - The App Shell Model](https://developers.google.com/web/fundamentals/architecture/app-shell)</a>

* Application shell - A method of building a PWA that reliably and instantly loads on the screen
  * The minimal HTML, CSS, and JavaScript required to power the user interface and can load instantly when offline
* When to use the app shell model
  * When the navigation is relatively unchanging but has changing content
* Benefits
  * Reliable performance that is consistently fast
  * Native-like interactions
  * Economical use of data
* Requirements
  * Load fast
  * Use as little data as possible
  * Use static assets from a local cache
  * Separate content from navigation
  * Retrieve and display page-specific content
  * Optionally cache dynamic content
* Building your app shell
  * Structure your app with a clear distinction between page shell and dynamic content
  * Determine the right balance between speed and data freshness for each data source

### <a name="FirstPWA">[Your First Progressive Web App](https://developers.google.com/web/fundamentals/codelabs/your-first-pwapp/)</a>

Note: This section contains a codelab which walks through the steps of building a simple PWA.
If you have never built one before, I recommend following it through.
This section of notes will contain important parts of the step-by-step process.

* Architect your App Shell
  * Design the app shell
    * What needs to be on screen immediately?
    * What other UI components are key to our app?
    * What supporting resources are needed for the app shell?
* Implement your App Shell
  * Create the HTML for the App Shell
  * Include the key JavaScript code that is necessary for the app to run
* Use service workers to pre-cache the App Shell
  * Register the service worker if it's available
  * Cache the site assets
  * Serve the app shell from the cache
* Use service workers to cache dynamic data
  * Intercept the network request and cache the response
* Support native integration
  * Declare an app manifest with a `manifest.json` file
    * Best Practices
      * Place the manifest link on all pages
      * Chrome prefers the `short_name`
      * Define icon sets for different density screens
      * Include an icon with a size that is sensible for a splash screen
      * Don't forget to set the `background_color`
* Deploy to a secure host and celebrate

### <a name="SW">[Using Service Workers](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API/Using_Service_Workers)</a>

* The premise of service workers
  * Service workers are used to cache and serve content when offline
* Basic architecture

1. The service worker URL is fetched and registered via `serviceWorkerContainer.register()`
2. The service worker is executed in a `ServiceWorkerGlobalScope`
3. The service worker is now ready to process events
4. Installation of the worker is attempted when service worker controlled pages are accessed
5. When the `oninstall` handler completes, the service worker is considered installed
6. Once the service worker is installed, it receives an activate event
7. The service worker will now control pages but only those opened after `register()` is successful

* Registering your worker

  ```
  if ('serviceWorker' in navigator) {
    navigator.serviceWorker.register('/sw-test/sw.js', {scope: '/sw-test/'})
    .then(function(reg) {
      // registration worked
      console.log('Registration succeeded. Scope is ' + reg.scope);
    }).catch(function(error) {
      // registration failed
      console.log('Registration failed with ' + error);
    });
  }
  ```
  * Why is my service worker not registering?
    * It must be running on HTTPS
    * The path to the service worker file must be written relative to the origin, not the app's root directory
    * The service worker must be on the same origin as the app
* Install and activate: populating your cache
  * After a SW is registered, it will attempt to install. If the install succeeds, an `install` event is fired.
  
  ```
  self.addEventListener('install', function(event) {
    event.waitUntil(
      caches.open('v1').then(function(cache) {
        return cache.addAll([
          '/sw-test/',
          '/sw-test/index.html',
          '/sw-test/style.css',
          '/sw-test/app.js',
          '/sw-test/image-list.js',
          '/sw-test/star-wars-logo.jpg',
          '/sw-test/gallery/',
          '/sw-test/gallery/bountyHunters.jpg',
          '/sw-test/gallery/myLittleVader.jpg',
          '/sw-test/gallery/snowTroopers.jpg'
        ]);
      })
    );
  });
  ```
  
* Custom responses to requests
  
  ```
  self.addEventListener('fetch', function(event) {
    event.respondWith(
      caches.match(event.request)
    );
  });
  ```

* Recovering failed requests
  * If the request isn't in the cache, fetch it and store it for later
  ```
  self.addEventListener('fetch', function(event) {
    event.respondWith(
      caches.match(event.request).then(function(resp) {
        return resp || fetch(event.request).then(function(response) {
          let responseClone = response.clone();
          caches.open('v1').then(function(cache) {
            cache.put(event.request, responseClone);
          });

          return response;
        });
      }).catch(function() {
        return caches.match('/sw-test/gallery/myLittleVader.jpg');
      })
    );
  });
  ```

* Updating your service worker
  * SWs have versions which need to be incremented to install the latest version
  
  ```
  self.addEventListener('install', function(event) {
    event.waitUntil(
      caches.open('v2').then(function(cache) {
        return cache.addAll([
          '/sw-test/',
          '/sw-test/index.html',
          '/sw-test/style.css',
          '/sw-test/app.js',
          '/sw-test/image-list.js',

          …

          // include other new resources for the new version...
        ]);
      })
    );
  });
  ```

* Deleting old caches

```
self.addEventListener('activate', function(event) {
  var cacheWhitelist = ['v2'];

  event.waitUntil(
    caches.keys().then(function(keyList) {
      return Promise.all(keyList.map(function(key) {
        if (cacheWhitelist.indexOf(key) === -1) {
          return caches.delete(key);
        }
      }));
    })
  );
});
```

## <a name="Perf">Performance Optimization and Caching</a>

Mobile users demand websites that load nearly instantly, despite poor or absent connectivity. Because many users also face expensive data caps, you must minimize their application's data footprint to reduce page load time as much as possible. You'll be asked to show you can carry out performance audits on applications to reduce page load times and maintain responsive user experiences by:
* Preventing main thread blocking with a dedicated web worker
* Providing an optimized critical rendering path using:
  * Compressed or minified JavaScript, HTML and CSS files to reduce render blocking
  * Inline CSS for essential styles on a specific page, with asynchronous loading for additional styles as necessary
  * Inline JavaScript files for initial rendering only where necessary (or otherwise eliminated, deferred, or marked as async)
  * Ordered loading of remaining critical resources and early download of all critical assets to shorten the critical path length
  * Reduced DOM depth to minimize browser layout/reflow
  * Your browser's developer tools to diagnose performance issues on mobile devices
* Prefetching files that load when resources are available, reducing the time to meaningful interaction
* Providing client storage that is appropriate to a web application’s data persistence needs, including:
  * Session state management
  * Asset caching based on their impact on load time and offline functionality
  * Using IndexedDB to store dynamic content in offline mode

### <a name="WebWorkers">[Using Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers)</a>

* Web Workers API
  * A worker is an object that runs a named JavaScript file
  * A dedicated worker is only accessible from the script that first spawned it
  * Shared workers can be accessede from multiple scripts
  * A worker can do almost anything any other script can do *except* modify the DOM or use some properties of `window`
    * [For an exhaustive list of supported functions, see this link](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Functions_and_classes_available_to_workers)
  * `postMessage()` is used to send messages between the main thread and workers
  * The `onmessage` event can be used to handle the aforementioned messages
* Dedicated workers
  * Worker feature detection
    * To ensure browser support, it is recommended that all worker code be wrapped in the following: 
    * `if (window.Worker) { ... }`
  * Spawning a dedicated worker
    * `var myWorker = new Worker('workerScript.js');`
  * Sending messages to and from a dedicated worker
    * `myWorker.postMessage([value1, value2]);` 
    ```
    onmessage = function(e) {
      console.log('Message received from main script');
      var workerResult = 'Result: ' + (e.data[0] * e.data[1]);
      console.log('Posting message back to main script');
      postMessage(workerResult);
    }
    ```
    ```
    myWorker.onmessage = function(e) {
      result.textContent = e.data;
      console.log('Message received from worker');
    }
    ```
  * Terminating a worker
    * The following will close a worker immediately without closing up after itself
    * `myWorker.terminate();`
    * The following can be used within a worker to close itself
    * `close();`
  * Handling errors
    * `onerror` is called when a runtime error occurs
    * The error event has the following fields
      * `message` - the human readable error message
      * `filename` - the name of the script in which the error occurred
      * `lineno` - the line number of the script file on which the error occurred
  * Spawning subworkers
    * A worker may spawn subworkers as long as the subworkers are hosted within the same origin as the parent page
  * Importing scripts and libraries
    * Worker threads can access `importScripts()` which can be used to import scripts
    * The script is loaded and then executed
* Shared workers
  * A shared worker is accessible by multiple scripts
  * Spawning a shared worker
    * `var myWorker = new SharedWorker('worker.js');`
    * Shared workers communicate via a `port` object, which must be specified by the `onmessage` event handler or with the `start()` method
      * `start()` must be called in both the parent and child threads for 2-way communication
  * Sending message to and from a shared worker
    * `myWorker.port.postMessage([value1, value2]);`
    ```
    onconnect = function(e) {
      var port = e.ports[0];

      port.onmessage = function(e) {
        var workerResult = 'Result: ' + (e.data[0] * e.data[1]);
        port.postMessage(workerResult);
      }
    }
    ```
    * `myWorker.port.onmessage = function(e) { ... }`
* About thread safety
  * `Worker` threads spawn real OS-level threads but because communication between threads is more limited, it is often difficult to get concurrency problems
* Content security policy
  * Workers are not governed by the document's [content security policy](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/Content_Security_Policy)
  * To specify a content security policy for the worker, set a Content-Security-Policy response header for the request which delivers the worker script
* Transferring data to and from workers: further details
  * Data passed between the main page and workers is copied, not shared

### <a name="GoogleOfflineWebApps">[Offline Web Applications by Google](https://www.udacity.com/course/offline-web-applications--ud899)</a>

### <a name="PerformanceFundamentals">[Web Fundamentals - Performance](https://developers.google.com/web/fundamentals/performance/why-performance-matters/)</a>

* Performance is about retaining users
  * High performance is an asset, poor performance is a liability
* Performance is about improving conversions
  * Better performance, more user conversions
* Performance is about the user experience
  * Better performance is better user experience
* Performance is about people
  * The better your site performs, the more people are able to access it
* Where to go from here
  * Mind what resources you send
    * Consider what CSS resources you need as it is render blocking
    * Search for the leanest options to JavaScript libraries
    * Not all websites need to be single page applications. Consider changing to avoid extra JavaScript
  * Mind how you send resources
    * Migrate to HTTP/2
    * Expedite the delivery of resources using resource hints
      * `rel=preload` tells browser that the resource is critical and should be fetched early
    * Consider using code splitting to limit the amount of scripts downloaded to only what is necessary
  * Mind how much data you send
    * Minify text assets
    * Configure the server to compress resources
    * Optimize images
    * Consider alternate image formats such as webp
    * Deliver images responsively
    * Use video instead of animated gifs
    * Use client hints to determine what resources to deliver
    * Use the `NetworkInformation` API to adjust the experience for users on slower connections

### <a name="OfflineCookbook">[The Offline Cookbook](https://jakearchibald.com/2014/offline-cookbook/)</a>

* The cache machine - when to store resources
  * On install - as a dependency
    * Cache things that are needed to load other things
    * CSS, images, fonts, JS, templates, other static images needed for the site
    * Basically, anything that without it, would make the site non-functional
    ```
    self.addEventListener('install', function(event) {
      event.waitUntil(
        caches.open('mysite-static-v3').then(function(cache) {
          return cache.addAll([
            '/css/whatever-v3.css',
            '/css/imgs/sprites-v6.png',
            '/css/fonts/whatever-v8.woff',
            '/js/all-min-v4.js'
            // etc
          ]);
        })
      );
    });
    ```
    * `event.waitUntil` takes a promise to define the length & success of the install
    * If any of the resources fail to fetch, the entire call rejects
  * On install - not as a dependecy
    * Ideal for bigger resources that aren't crucial but will be used later on
    ```
    self.addEventListener('install', function(event) {
      event.waitUntil(
        caches.open('mygame-core-v1').then(function(cache) {
          cache.addAll(
            // levels 11-20
          );
          return cache.addAll(
            // core assets & levels 1-10
          );
        })
      );
    });
    ```
    * The promise for levels 11-20 isn't being passed back to `event.waitUntil` so even if it fails, everything else will still be available offline
  * On activate
    * Ideal for clean-up and migration
    * Runs once the old version of the service worker is done
    ```
    self.addEventListener('activate', function(event) {
      event.waitUntil(
        caches.keys().then(function(cacheNames) {
          return Promise.all(
            cacheNames.filter(function(cacheName) {
              // Return true if you want to remove this cache,
              // but remember that caches are shared across
              // the whole origin
            }).map(function(cacheName) {
              return caches.delete(cacheName);
            })
          );
        })
      );
    });
    ```
  * On user interaction
    * If the entire site cannot be taken offline (such as YouTube or Wikipedia), allow the user to select what content they want offline
    ```
    document.querySelector('.cache-article').addEventListener('click', function(event) {
      event.preventDefault();

      var id = this.dataset.articleId;
      caches.open('mysite-article-' + id).then(function(cache) {
        fetch('/get-article-urls?id=' + id).then(function(response) {
          // /get-article-urls returns a JSON-encoded array of
          // resource URLs that a given article depends on
          return response.json();
        }).then(function(urls) {
          cache.addAll(urls);
        });
      });
    });
    ```
  * On network response
    * Ideal for frequently updating resources such as messages in an inbox
    * If a request doesn't match anything in the cache, get it from the network, send it to the page, and add it to the cache
    ```
    self.addEventListener('fetch', function(event) {
      event.respondWith(
        caches.open('mysite-dynamic').then(function(cache) {
          return cache.match(event.request).then(function (response) {
            return response || fetch(event.request).then(function(response) {
              cache.put(event.request, response.clone());
              return response;
            });
          });
        })
      );
    });
    ```
  * Stale-while-revalidate
    * Ideal for frequently updating resources that don't always need the very latest version
    * If there's a cached version available, use it but fetch an update for next time
    ```
    self.addEventListener('fetch', function(event) {
       event.respondWith(
         caches.open('mysite-dynamic').then(function(cache) {
           return cache.match(event.request).then(function(response) {
             var fetchPromise = fetch(event.request).then(function(networkResponse) {
               cache.put(event.request, networkResponse.clone());
               return networkResponse;
             })
             return response || fetchPromise;
           })
         })
       );
     });
     ```
   * On push message
     * Ideal for content relating to a notification
     * Awakens the service worker from a response to the OS's messaging service
     ```
     self.addEventListener('push', function(event) {
       if (event.data.text() == 'new-email') {
         event.waitUntil(
           caches.open('mysite-dynamic').then(function(cache) {
             return fetch('/inbox.json').then(function(response) {
               cache.put('/inbox.json', response.clone());
               return response.json();
             });
           }).then(function(emails) {
             registration.showNotification("New email", {
               body: "From " + emails[0].from.name
               tag: "new-email"
             });
           })
         );
       }
     });

     self.addEventListener('notificationclick', function(event) {
       if (event.notification.tag == 'new-email') {
         // Assume that all of the resources needed to render
         // /inbox/ have previously been cached, e.g. as part
         // of the install handler.
         new WindowClient('/inbox/');
       }
     });
     ```
    * On background-sync
      * Ideal for non-urgent updates, especially regular ones that wouldn't necessitate a push notification
      ```
      self.addEventListener('sync', function(event) {
        if (event.id == 'update-leaderboard') {
          event.waitUntil(
            caches.open('mygame-dynamic').then(function(cache) {
              return cache.add('/leaderboard.json');
            })
          );
        }
      });
      ```
* Cache persistence
  * The origin is given a certain amount of free space
  * Find out how much is available:
  ```
  navigator.storageQuota.queryInfo("temporary").then(function(info) {
    console.log(info.quota);
    // Result: <quota in bytes>
    console.log(info.usage);
    // Result: <used data in bytes>
  });
  ```
  * The browser is free to throw away storage when necessary
  * Request persistent storage from the user:
  ```
  // From a page:
  navigator.storage.requestPersistent().then(function(granted) {
    if (granted) {
      // Hurrah, your data is here to stay!
    }
  });
  ```
* Serving suggestions - responding to requests
  * The Service Worker won't use the cache unless you tell it when and how
  * Cache only
    * Ideal for anything you'd consider static to that version of the site
    * These should have been cached at install
    ```
    self.addEventListener('fetch', function(event) {
      // If a match isn't found in the cache, the response
      // will look like a connection error
      event.respondWith(caches.match(event.request));
    });
    ```
  * Network only
    * Ideal for things that have no offline equivalent
    ```
    self.addEventListener('fetch', function(event) {
      event.respondWith(fetch(event.request));
      // or simply don't call event.respondWith, which
      // will result in default browser behaviour
    });
    ```
  * Cache, falling back to network
    * Ideal for offline first applications
    ```
    self.addEventListener('fetch', function(event) {
      event.respondWith(
        caches.match(event.request).then(function(response) {
          return response || fetch(event.request);
        })
      );
    });
    ```
  * Cache and network race
    * Ideal for small assets where you're chasing performance on devices with slow disk access
    ```
    // Promise.race is no good to us because it rejects if
    // a promise rejects before fulfilling. Let's make a proper
    // race function:
    function promiseAny(promises) {
      return new Promise((resolve, reject) => {
        // make sure promises are all promises
        promises = promises.map(p => Promise.resolve(p));
        // resolve this promise as soon as one resolves
        promises.forEach(p => p.then(resolve));
        // reject if all promises reject
        promises.reduce((a, b) => a.catch(() => b))
          .catch(() => reject(Error("All failed")));
      });
    };

    self.addEventListener('fetch', function(event) {
      event.respondWith(
        promiseAny([
          caches.match(event.request),
          fetch(event.request)
        ])
      );
    });
    ```
  * Network falling back to cache
    * A quick-fix for resources that update frequently outside of the version of the site
    * Online users get the most up-to-date content but offline users get an older cached version
    * If the network connection succeeds, update the cached version
    * Bad for slow connections as the user will still have to wait for the network to fail to get the content
    ```
    self.addEventListener('fetch', function(event) {
      event.respondWith(
        fetch(event.request).catch(function() {
          return caches.match(event.request);
        })
      );
    });
    ```
  * Cache then network
    * Ideal for content that updates frequently
    * The page makes two requests; one to the cache, one to the network
    * Show the cached data first, then update the page when/if the network data arrives
    * If updating data when the network responds, don't disrupt the user
    Code in the page:
    ```
    var networkDataReceived = false;

    startSpinner();

    // fetch fresh data
    var networkUpdate = fetch('/data.json').then(function(response) {
      return response.json();
    }).then(function(data) {
      networkDataReceived = true;
      updatePage();
    });

    // fetch cached data
    caches.match('/data.json').then(function(response) {
      if (!response) throw Error("No data");
      return response.json();
    }).then(function(data) {
      // don't overwrite newer network data
      if (!networkDataReceived) {
        updatePage(data);
      }
    }).catch(function() {
      // we didn't get cached data, the network is our last hope:
      return networkUpdate;
    }).catch(showErrorMessage).then(stopSpinner);
    ```
    Code in the Service Worker: 
    ```
    self.addEventListener('fetch', function(event) {
      event.respondWith(
        caches.open('mysite-dynamic').then(function(cache) {
          return fetch(event.request).then(function(response) {
            cache.put(event.request, response.clone());
            return response;
          });
        })
      );
    });
    ```
  * Generic fallback
    * Ideal for secondary imagery such as avatars, failed POST requests, "Unavailable while offline" page
    * Use if you fail to serve something from the cache and/or network
    * Should be an install dependency
    ```
    self.addEventListener('fetch', function(event) {
      event.respondWith(
        // Try the cache
        caches.match(event.request).then(function(response) {
          // Fall back to network
          return response || fetch(event.request);
        }).catch(function() {
          // If both fail, show a generic fallback:
          return caches.match('/offline.html');
          // However, in reality you'd have many different
          // fallbacks, depending on URL & headers.
          // Eg, a fallback silhouette image for avatars.
        })
      );
    });
    ```
  * ServiceWorker-side templating
    * Ideal for pages that cannot have their server response cached
    ```
    importScripts('templating-engine.js');

    self.addEventListener('fetch', function(event) {
      var requestURL = new URL(event.request);

      event.respondWith(
        Promise.all([
          caches.match('/article-template.html').then(function(response) {
            return response.text();
          }),
          caches.match(requestURL.path + '.json').then(function(response) {
            return response.json();
          })
        ]).then(function(responses) {
          var template = responses[0];
          var data = responses[1];

          return new Response(renderTemplate(template, data), {
            headers: {
              'Content-Type': 'text/html'
            }
          });
        })
      );
    });
    ```
* Putting it together
  * A site will most likely use a combination of the previously mentioned methods
  * Look at your request and decide how to handle it
  * Example:
  ```
    self.addEventListener('fetch', function(event) {
    // Parse the URL:
    var requestURL = new URL(event.request.url);

    // Handle requests to a particular host specifically
    if (requestURL.hostname == 'api.example.com') {
      event.respondWith(/* some combination of patterns */);
      return;
    }
    // Routing for local URLs
    if (requestURL.origin == location.origin) {
      // Handle article URLs
      if (/^\/article\//.test(requestURL.pathname)) {
        event.respondWith(/* some other combination of patterns */);
        return;
      }
      if (/\.webp$/.test(requestURL.pathname)) {
        event.respondWith(/* some other combination of patterns */);
        return;
      }
      if (request.method == 'POST') {
        event.respondWith(/* some other combination of patterns */);
        return;
      }
      if (/cheese/.test(requestURL.pathname)) {
        event.respondWith(
          new Response("Flagrant cheese error", {
            status: 512
          })
        );
        return;
      }
    }

    // A sensible default pattern
    event.respondWith(
      caches.match(event.request).then(function(response) {
        return response || fetch(event.request);
      })
    );
  });
  ```

### <a name="Cache">[Cache - MDN](https://developer.mozilla.org/en-US/docs/Web/API/Cache)</a>

* The Cache interface provides a storage mechanism for Request / Response object pairs that are cached as part of the ServiceWorker life cycle
  * Note: Cache is exposed to windows scopes as well as workers, so it is not necessary to only use it with service workers
* Cache items are not updated unless explicitly requested. They do not expire unless deleted.
* You are responsible for managing the amount of storage your site uses.
* Methods
  * `Cache.match(request, options)` - Returns a Promise that resolves to the response associated with the first matching request in the Cache object
  * `Cache.matchAll(request, options)` - Returns a Promise that resolves to an array of all matching requests in the Cache object
  * `Cache.add(request)` - Takes a URL, retrieves it, and adds the resulting response object to the given cache.
    * Equivalent to calling `fetch()`, then using `put()` to add the results to the cache.
  * `Cache.addAll(requests)` - Takes an array of URLs, retrieves them, and adds the resulting response objects to the given cache
  * `Cache.put(request, response)` - Takes both a request and its response and adds it to the given cache
  * `Cache.delete(request, options)` - Finds the cache entry whose key is the request, returning a Promise that resolves to `true` if a matching cache entry is found and deleted. If no entry is found, the promise resolves to `false`,
  * `Cache.keys(request, options)` - Returns a promise that resolves to an array of cache keys
* Example
  ```
    var CACHE_VERSION = 1;

    // Shorthand identifier mapped to specific versioned cache.
    var CURRENT_CACHES = {
      font: 'font-cache-v' + CACHE_VERSION
    };

    self.addEventListener('activate', function(event) {
      var expectedCacheNames = Object.values(CURRENT_CACHES);

      // Active worker won't be treated as activated until promise
      // resolves successfully.
      event.waitUntil(
        caches.keys().then(function(cacheNames) {
          return Promise.all(
            cacheNames.map(function(cacheName) {
              if (!expectedCacheNames.includes(cacheName)) {
                console.log('Deleting out of date cache:', cacheName);

                return caches.delete(cacheName);
              }
            })
          );
        })
      );
    });

    self.addEventListener('fetch', function(event) {
      console.log('Handling fetch event for', event.request.url);

      event.respondWith(

        // Opens Cache objects that start with 'font'.
        caches.open(CURRENT_CACHES['font']).then(function(cache) {
          return cache.match(event.request).then(function(response) {
            if (response) {
              console.log('Found response in cache:', response);

              return response;
            }

            console.log('Fetching request from the network');

            return fetch(event.request).then(function(networkResponse) {
              cache.put(event.request, networkResponse.clone());

              return networkResponse;
            });
          }).catch(function(error) {

            // Handles exceptions that arise from match() or fetch().
            console.error('Error in fetch handler:', error);

            throw error;
          });
        })
      );
    });
  ```

### <a name="Storage">[Storage](https://developer.mozilla.org/en-US/docs/Web/API/Storage)</a>

* The Storage interface of the Web Storage API provides access to a particular domain's session or local storage.
* Properties
  * `Storage.length` - Returns an integer representing the number of data items stored in the Storage object
* Methods
  * `Storage.key()` - When passed a number n, this method will returns the name of the nth key in the storage
  * `Storage.getItem()` - When passed a key name, will return that key's value
  * `Storage.setItem()` - When passed a name and value, will add that key to the storage or update that key's value if it already exists
  * `Storage.removeItem()` - When passed a key name, will remove that key from the storage
  * `Storage.clear()` - When invoked, will empty all keys out of the storage
* Example
  ```
  if(!localStorage.getItem('bgcolor')) {
    populateStorage();
  }
  setStyles();

  function populateStorage() {
    localStorage.setItem('bgcolor', document.getElementById('bgcolor').value);
    localStorage.setItem('font', document.getElementById('font').value);
    localStorage.setItem('image', document.getElementById('image').value);
  }

  function setStyles() {
    var currentColor = localStorage.getItem('bgcolor');
    var currentFont = localStorage.getItem('font');
    var currentImage = localStorage.getItem('image');

    document.getElementById('bgcolor').value = currentColor;
    document.getElementById('font').value = currentFont;
    document.getElementById('image').value = currentImage;

    htmlElem.style.backgroundColor = '#' + currentColor;
    pElem.style.fontFamily = currentFont;
    imgElem.setAttribute('src', currentImage);
  } 
  ```

### <a name="LocalStorage">[Local Storage And How To Use It On Websites](https://www.smashingmagazine.com/2010/10/local-storage-and-how-to-use-it/)</a>

* Adding State To The Web: The "Why" Of Local Storage
  * HTTP is stateless - it doesn't remember what you were doing after you close your browser
  * Local storage can be used to add state
* C Is For Cookie. Is That Good Enough For Me?
  * A cookie is a text file hosted on the user's computer and connected to the domain. It can store some basic information
  * Cookie limitations
    * They add to the load of every document accessed on the domain
    * They allow up to only 4 KB of storage
    * Some people do not trust cookies and disallow them
* Using Local Storage in HTML5-Capable Browsers
  * `localStorage.setItem('favoriteflavor', 'vanilla');`. That's it. It's that easy.
  * `localStorage.getItem('favoriteflavor');` returns vanilla
  * `localStorage.removeItem('favoriteflavor');` and *poof* it's gone
* Working Around The "Strings Only" Issue
  * Objects do not store as would be most helpful
  * `JSON.stringify()` and `JSON.parse()` can be used to work around this
  * `localStorage.setItem('myObject', JSON.stringify(myObjectExample));`
  * `JSON.parse(localStorage.getItem('myObject'));`
* Use Case #1: Local Storage Of Web Service Data
  * If you store large data sets, you don't have to take the time to request them a second time
* Use Case #2: Maintaining The State Of An Interface The Simple Way
  * Store the state of interfaces

### <a name="IndexedDB">[IndexedDB API](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API)</a>

* IndexedDB is a low-level API for client-side storage of significant amounts of structured data, including files and blobs
* Web Storage is useful for storing smaller amounts of data but is less useful for larger amounts of structured data. That's where IndexedDB comes to help.
* Key concepts and usage
  * IndexedDB is a transactional database system, like SQL
  * Unlike SQL, IndexedDB is a JavaScript-based object-oriented database
  * Store and retrieve objects with a key
  * Synchronous and asynchronous
    * Operations are done asynchoronously
    * Originally it included a synchornous API. It was removed because it is a bad idea to work synchornously for most web technologies
* Interfaces
  * To get access to a database, call `open()` on the `indexedDB` attribute of a `window` object
  * This returns an `IDBRequest` object
  * Connecting to a database
    * `IDBEnvironment` - Provides access to IndexedDB functionality. It is implemented by the `window` and `worker` objects. *Not part of the 2.0 specification*
    * `IDBFactory` - Provides access to a database. This is the interface implemented by the global object `indexedDB` and is therefore the entry point for the API.
    * `IDBOpenDBRequest` - Represents a request to open a database
    * `IDBDatabase` - Represents a connection to a database. It's the only way to get a transaction on the database
    * `IDBTransaction` - Represents a transaction. You create a transaction on a database, specify the scope, and determine the kind of access that you want.
    * `IDBRequest` - Genereic interface that handles database requests and provides access to results
    * `IDBObjectStore `- Represents an object store that allows access to a set of data in an IndexedDB database, looked up via primary key
    * `IDBIndex` - Uses an index to retrieve the record(s) rather than the primary key
    * `IDBCursor` - Iterates over object stores and indexes
    * `IDBCursorWithValue` - Iterates over object stores and indexes and returns the cursor's current value
    * `IDBKeyRange` - Defines a key range that can be used to retrieve data from a database in a certain range
  * Custom event interfaces
    * `IDBVersionChangeEvent` - Indicates that the version of the database has changed

### <a name="DevTools">[Get Started with Analyzing Network Performance in Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools/network-performance/)</a>

* Set up DevTools
  * Use the `Capture Screenshots` button in the dev tools to capture screenshots of the page load
* Emulate a mobile user's experience
  * Use `Disable Cache`. This will emulate the first visit to s ite
  * Select your internet speed and change it to a mobile speed to simulate a mobile user
    * If you can load fast on terrible connections, it will load fast for all users
* Analyze requests
  * Find render-blocking scripts
    * When the browser finds a `<script>` tag, it stops everything and executes the script immediately
    * Any scripts that aren't needed immediately should be tagged with `async`
    * Consider also moving scripts to the bottom of the `<body>`
  * Find large requests
    * If the site takes too long loading one individual file, that file is probably too big. Consider compressing it or changing it for a smaller file (such as png to svg) if possible
* Verify fixes on updated page
  * With the fixes in place, test the page to verify that it does indeed load faster

## <a name="Test">Testing and Debugging</a>

Developers typically work in highly iterative deployment environments, relying on extensive testing and debugging to maintain functionality and code integrity. You'll be asked to show that you can verify expected behaviors and diagnose common web application bugs by:
* Writing unit tests that first verify a function’s intended behavior, and then iteratively modifying its code until it passes those tests
* Setting breakpoints within a complicated function to determine exactly where it deviates from expected behavior
* Using console logs to output relevant debugging information
* Reproducing and fixing bugs based on user reported issues

### <a name="JSDevTools">[Get Started with Debugging JavaScript in Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools/javascript/)</a>

* Get familiar with the Sources panel UI
  * The `Sources` panel in the dev tools is where you debug JavaScript
  * The Sources panel has 3 parts
  ![Sources Panel](https://developers.google.com/web/tools/chrome-devtools/javascript/imgs/sources-annotated.png)
  1. File Navigator pane - Every file that the page requests
  2. Code Editor pane - The contents of an individual file
  3. JavaScript Debugging pane - Various debugging tools
* Reproduce the bug
  * The first step in debugging is finding the series of actions that consistently reproduces the bug
* Pause the code with a breakpoint
  * A common practice is to `console.log()` a bunch of stuff to see what's going on. It "works" but takes forever
  * Setting a breakpoint will allow you to see the value of all active variables at that point in execution
  * To see a full list of the various types of breakpoints and when to use them, [use this link](https://developers.google.com/web/tools/chrome-devtools/javascript/breakpoints)
* Step through the code
  * Stepping through the code enables you to walk through your code's execution one line at a time and see where it is misbehaving
  * `Step into next function call` will go to the next line, stepping into a function if one is called
  * `Step over next function call` will go to the next line, executing a function and returning to the next line if a function is called
* Set a line-of-code breakpoint
  * Line-of-code breakpoints are the most common. They pause execution at a specific line
  * You can set a line-of-code breakpoint by clicking the line number of a script
* Check variable values
  * Method 1: The Scope pane
    * The Scope pane in the debugging panel will show the values of *all* variables in scope
  * Method 2: Watch Expressions
    * Next to the Scope pane is the Watch pane. You can add expressions to watch and it will track those expressions
    * You can add things such as `myVariable` and `typeof myVariable` to get the value of a variable or the type of a variable respectively
  * Method 3: The Console
    * You can use the console to quickly evaluate expressions as well
* Apply a fix 
  * You can edit the code live in the Code Editor pane to apply your fix directly and test out if it works immediately!

### <a name="Console">[Diagnose and Log to Console](https://developers.google.com/web/tools/chrome-devtools/console/console-write)</a>

* TL;DR
  * `console.log()` for basic logging
  * `console.error()` and `console.warn()` for more important stuff
  * `console.group()` and `console.groupEnd()` to group related messages
  * `console.assert()` to show conditional error messages
* Writing to the console
  * `console.log()` takes one or more expressions and writes their current values to the console
* Autocompleting commands - the console will recommend relevant commands as you type them. This includes expressions you previously executed
* Organizing Console output
  * Group messages together
    * The `console.group()` command takes a single string parameter to set the name of the group. AFter calling it, the console will group all subsequent output messages together
    * Use `console.groupEnd()` to end the grouping
  * Nested groups - You can call `console.group()` a second time to nest another group inside the main group
  * Auto-collapsing groups - Automatically collapse groups by calling `console.groupCollapsed()` instead of `console.group()`
* Errors and warnings
  * `console.error()` will display a red icon with red text
  * `console.warn()` will display a yelling warning icon with the message text
* Assertions
  * `console.assert()` takes an expression and a string. The string will only display (as an error) if the expression evaluates to `false`
  * Example: `console.assert(list.length < 5, 'List is too short!');` will display the assertion
* String substitution and formatting
  * Use string substitution to easily display variables
  * `console.log('%s has %d points', 'Sam', 100)` => `Sam has 100 points`
  * Format specifiers
    * %s - String
    * %i or %d - Integer
    * %f - Float
    * %o - DOM element
    * %O - JavaScript object
    * %c - Applies CSS style rules to the output string

### <a name="DebugSW">[Debugging Service Workers](https://developers.google.com/web/fundamentals/codelabs/debugging-service-workers/)</a>

Note: This section is a codelab. To get the most benefit from it, it is recommended to follow along with the codelab. What I feel like are the most important notes from it are listed here.

* Introducing the Application Tab
  * Inspecting the Manifest
    * Manifest is included under the `Application` list under the `Application` tab
    * Includes an `Add to homescreen` button to simulate the experience of adding the app to the homescreen
  * Inspecting the Service Workers
    * Service Workers is included under the `Application` list under the `Application` tab
    * Provides information about Service Workers which are active in the current origin
    * Available testing options
      * Offline - Will simulate being disconnected from the network
      * Update on reload - Will force the current SW to be replaced by a new one
      * Bypass for network - Will force the browser to ignore any active SW and fetch resources from the network
      * Show all - Will show a list of all active SWs regardless of the origin
* Exploring the cache
  * Add caching to your Service Worker
    * It is recommended to use `Update on reload` for any SWs when working on caching related content
  * Inspecting Cache Storage
    * When content is in the cache, the `Cache Storage` section will be expandable
    * It will contain all files cached by the SW
    * You can remove a file from the cache by right-clicking it and selecting `Delete`
  * Cleaning the slate
    * Select `Clear storage` from the `Application` list and at the button select `Clear selected`. This will delete all selected cached files
  * Under the network tab, any resource served from a SW will have a gear icon next to it
* Simulating different network conditions
  * Serving requests while offline
    * Select `Offline` under the `Service Worker` settings to ensure that files are being served while offline
  * Testing slow or flaky networks
    * Select `Bypass for network` under the `Service Worker` settings
    * Select a network throttling speed under the `Network` tab
    * Notice the time it takes to download files. Uncheck `Bypass for network` and compare the speeds
* Remember, it's just JavaScript
  * You can use existing JavaScript debugging tools to debug Service Workers
  * Working with the debugger
    * Use the sources panel. Breakpoints and `debugger` keywords are your friends!
* Testing Push Notifications
  * Adding Push support
    * Add an event listener for the `push` event in your SW file
    * Example: 
    ```
    self.addEventListener('push', function(event) {
      var title = 'Yay a message.';
      var body = 'We have received a push message.';
      var icon = '/images/smiley.svg';
      var tag = 'simple-push-example-tag';
      event.waitUntil(
        self.registration.showNotification(title, {
          body: body,
          icon: icon,
          tag: tag
        })
      );
    });
    ```
    * Push requests will require user permission before they are enabled

## <a name="ES2015">ES2015 Concepts and Syntax</a>

Web developers must stay current with the latest JavaScript features that promote simpler and more readable code. With polyfills enabling code written in ES2015 JavaScript to be used in unsupported browsers, there is a strong incentive for developers to begin using the new features and syntax. You'll be asked to show that you understand and can write ES2015 JavaScript code using:
* JavaScript promises with ES2015 syntax that create asynchronous functions and incorporate graceful error handling
* Variables that can be used with block scope, function scope, and made immutable depending on context using let, var, and const
* String literals that include string interpolation and multi-line strings
* Arrow functions that create anonymous functions and use an unbounded this
* Default function parameters that initialize default values for a function when no argument or undefined is provided
* for...of loops that can iterate over any iterable object while running a custom function on each
* Maps that allow for arbitrary key and value pairs that are iterable and include non-string keys
* Sets that contain only unique, iterable elements where an array would degrade performance

### <a name="ES6Promises">[JavaScript Promises: an Introduction](https://developers.google.com/web/fundamentals/primers/promises)</a>

[Note: This section has already been covered here](#Promises)

### <a name="Promise">[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)</a>

* The `Promise` object represents the eventual completion (or failure) of an asynchronous operation and its resulting value.
* Syntax
  * `new Promise( /* executor */ function (resolve, reject) { ... } );`
  * executor
    * A function that is passed with the arguments `resolve` and `reject`
    * The executor function is executed immediately by the Promise implementation, passing `resolve` and `reject` functions.
    * The `resolve` and `reject` functions, when called, resolve or reject the promise
    * The executor will do its function and then calls `resolve` to resolve the promise or rejects if an error occurs
    * If any error occurs in the executor function, the promise rejects
* Description
  * A `Promise` is a proxy for a value not necessarily known when the promise is created
  * This is particularly helpful for asynchronous operations
  * A `Promise` has the following possible states
    * pending - initial state, neither fulfilled nor rejected
    * fulfilled - the operation completed successfully
    * rejected - the operation failed
  * When a promise is fulfilled or rejected, the associated `then` method is called
  * As `Promise.prototype.then()` and `Promise.prototype.catch()` return promises, they can be chained
* Properties
  * `Promise.length` - Length property whose value is always 1 (number of constructor arguments)
  * `Promise.prototype` - Represents the prototype for the `Promise` constructor
* Methods
  * `Promise.all(iterable)`
    * Returns a promise that either fulfills when all of the promises in the iterable argument have fulfilled or rejects as soon as one of the promises rejects.
    * If the promise is fulfilled, it is fulfilled with an array of the values from the fulfilled promises in the same order as defined in the iterable.
    * If the promise is rejected, it is rejected with the reason from the first promise that is rejected.
  * `Promise.race(iterable)`
    * Returns a promise that fulfills or rejects as soon as one of the promises in the iterable fulfills or rejects
  * `Promise.reject(reason)`
    * returns a `Promise` object that is rejected with the given reason
  * `Promise.resolve(value)`
    * Returns a `Promise` object that is resolved with the given value
* Promise prototype
  Properties
  * `Promise.prototype.constructor
    * Returns the function that created an instance's prototype. This is the `Promise` function by default
  Methods
  * `Promise.prototype.catch(onRejected)`
    * Appends a rejection handler callback to the promise and returns a new promise resolving to the return value of the callback if it is called or to its original fulfillment value if the promise is instead fulfilled
  * `Promise.prototype.then(onFullfilled, onRejected)`
    * Appens fulfillment and rejection handler to the promise and returns a new promise resolving to the return value of the handler
  * `Promise.prototype.finally(onFinally)`
    * Appends a handler to the promise and returns a new promise which is resolved when the original promise is resolved.
    * The handler is called when the promise is settled, either fulfilled or rejected
* Creating a Promise
  ```
  const myFirstPromise = new Promise((resolve, reject) => {
    // do something asynchronous which eventually calls either:
    //
    //   resolve(someValue); // fulfilled
    // or
    //   reject("failure reason"); // rejected
  });
  ```
  To provide a function with promise functionality, simply have it return a promise
  ```
  function myAsyncFunction(url) {
    return new Promise((resolve, reject) => {
      const xhr = new XMLHttpRequest();
      xhr.open("GET", url);
      xhr.onload = () => resolve(xhr.responseText);
      xhr.onerror = () => reject(xhr.statusText);
      xhr.send();
    });
  }
  ```
* Examples
  * Basic Example
    ```
    let myFirstPromise = new Promise((resolve, reject) => {
      // We call resolve(...) when what we were doing asynchronously was successful, and reject(...) when it failed.
      // In this example, we use setTimeout(...) to simulate async code. 
      // In reality, you will probably be using something like XHR or an HTML5 API.
      setTimeout(function(){
        resolve("Success!"); // Yay! Everything went well!
      }, 250);
    });

    myFirstPromise.then((successMessage) => {
      // successMessage is whatever we passed in the resolve(...) function above.
      // It doesn't have to be a string, but if it is only a succeed message, it probably will be.
      console.log("Yay! " + successMessage);
    });
    ```
  * Advanced Example
    ```
    'use strict';
    var promiseCount = 0;

    function testPromise() {
        let thisPromiseCount = ++promiseCount;

        let log = document.getElementById('log');
        log.insertAdjacentHTML('beforeend', thisPromiseCount +
            ') Started (<small>Sync code started</small>)<br/>');

        // We make a new promise: we promise a numeric count of this promise, starting from 1 (after waiting 3s)
        let p1 = new Promise(
            // The resolver function is called with the ability to resolve or
            // reject the promise
           (resolve, reject) => {
                log.insertAdjacentHTML('beforeend', thisPromiseCount +
                    ') Promise started (<small>Async code started</small>)<br/>');
                // This is only an example to create asynchronism
                window.setTimeout(
                    function() {
                        // We fulfill the promise !
                        resolve(thisPromiseCount);
                    }, Math.random() * 2000 + 1000);
            }
        );

        // We define what to do when the promise is resolved with the then() call,
        // and what to do when the promise is rejected with the catch() call
        p1.then(
            // Log the fulfillment value
            function(val) {
                log.insertAdjacentHTML('beforeend', val +
                    ') Promise fulfilled (<small>Async code terminated</small>)<br/>');
            }).catch(
            // Log the rejection reason
           (reason) => {
                console.log('Handle rejected promise ('+reason+') here.');
            });

        log.insertAdjacentHTML('beforeend', thisPromiseCount +
            ') Promise made (<small>Sync code terminated</small>)<br/>');
    }
    ```

### <a name="TemplateLiterals">[Template literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)</a>

* Template literals are string literals that allow embedded expressions
* Syntax
  * `` `string text` ``
  * `` `string text ${expression} string text` ``
* Description
  * Template literals are enclosed by the back-tick character instead of double or single quotes
  * Template literals can contain placeholders. They are indicated by the dollar sign and curly braces `${expression}`
  * Mutli-line strings
    * Any newline characters inserted in the source are part of the template literal
    ```
    console.log(`string text line 1
    string text line 2`);
    // "string text line 1
    // string text line 2"
    ```
  * Tagged templates
    * Tags allow you to parse template literals with a function
    * The first argument of a tag function contains an array of string values
    * The remaining arguments are related to the expressions
    ```
    var person = 'Mike';
    var age = 28;

    function myTag(strings, personExp, ageExp) {
      var str0 = strings[0]; // "That "
      var str1 = strings[1]; // " is a "

      // There is technically a string after
      // the final expression (in our example),
      // but it is empty (""), so disregard.
      // var str2 = strings[2];

      var ageStr;
      if (ageExp > 99){
        ageStr = 'centenarian';
      } else {
        ageStr = 'youngster';
      }

      // We can even return a string built using a template literal
      return `${str0}${personExp}${str1}${ageStr}`;
    }

    var output = myTag`That ${ person } is a ${ age }`;

    console.log(output);
    // That Mike is a youngster
    ```
    * Tag functions don't need to return a string, as shown in this example
    ```
    function template(strings, ...keys) {
      return (function(...values) {
        var dict = values[values.length - 1] || {};
        var result = [strings[0]];
        keys.forEach(function(key, i) {
          var value = Number.isInteger(key) ? values[key] : dict[key];
          result.push(value, strings[i + 1]);
        });
        return result.join('');
      });
    }

    var t1Closure = template`${0}${1}${0}!`;
    t1Closure('Y', 'A');  // "YAY!"
    var t2Closure = template`${0} ${'foo'}!`;
    t2Closure('Hello', {foo: 'World'});  // "Hello World!"
    ```
  * Raw strings
    * The special `raw` property, available on the first function argument of tagged templates, allows you to access the raw strings as they were entered without processing escape sequences
    ```
    function tag(strings) {
      console.log(strings.raw[0]);
    }

    tag`string text line 1 \n string text line 2`;
    // logs "string text line 1 \n string text line 2" ,
    // including the two characters '\' and 'n'
    ```
  * Tagged templates and escape sequences
    * Tagged templates conform to the rules of the following escape sequences
      * Unicode escapes started by `\u`. For example: `\u00A9`
      * Unicode code point escapes indicated by `\u{}`. For example: `\u{2F804}`
      * Hexadecimal escapes started by `\x`. For example, `\xA9`
      * Octal literal escapes started by `\` and (a) digit(s). For example, `\251`

### <a name="ArrowFunctions">[Arrow Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)</a>

* An arrow function has a shorter syntax than a function expression and does not have its own `this`, `arguments`, `super`, or `new.target`.
* Arrow functions are best suited for non-method functions and cannot be used as constructors
* Syntax
  * Basic Syntax
    * `(param1, param2, ..., paramN) => { statements }`
    * `(param1, param2, ..., paramN) => expression` equivalent to `=> { return expression; }`
    * Parentheses are optional when there is only one parameter: `singleParam => { statements }`
  * Advanced Syntax
    * Parenthesize the body of a function to return an object literal expression: `params => ({foo: bar})`
    * Rest parameters and default parameters are supported
      * `(param1, param2, ...rest) => { statements }`
      * `(param1 = defaultValue1, param2, ..., paramN = defaultValueN) => { statements }`
    * Destructuring within the parameter list is also supported
      * `var f = ([a, b] = [1, 2], {x: c} = {x: a + b}) => a + b + c;`
      * `f(); //6`
* Description
  * The two biggest influences on the introduction of arrow functions were shorter functions and no `this` keyword
  ```
  elements.map(function(element ) { 
    return element.length; 
  }); // [8, 6, 7, 9]
  ```
  vs
  ```
  elements.map(element => element.length); // [8, 6, 7, 9]
  ```
  * No separate `this`
    * Every function having its own `this` became frustrating with any object-oriented style of programming
    * Arrow functions do not have their own `this`. The `this` value of the enclosing lexical context is used (Basically, it follows normal variable scoping)
    * Relation with strict mode
      * Strict mode rules with regard to `this` are ignored
      * All other strict mode rules apply normally
    * Invoked through call or apply
      * Since arrow functions do not have their own `this`, the methods `call()` or `apply()` can only pass in parameters. `thisArg` is ignored
  * No binding of `arguments`
    * Arrow functions do not have their own `arguments` object
    * If `arguments` is used, it refers to the arguments of the enclosing scope
    ```
    var arguments = [1, 2, 3];
    var arr = () => arguments[0];

    arr(); // 1

    function foo(n) {
      var f = () => arguments[0] + n; // foo's implicit arguments binding. arguments[0] is n
      return f();
    }

    foo(3); // 6
    ```
    * In most case, using rest parameters is a good alternative to using an `arguments` object
  * Arrow functions used as methods
    * Since arrow functions do not have their own `this` method, it is recommended to not use them as object methods
  * Use of the `new` operator
    * Arrow functions cannot be used as constructors and will throw an error when used with `new`
  * Use of `prototype` property
    * Arrow functions do not have a `prototype` property
  * Use of the `yield` keyword
    * The `yield` keyword may not be used in an arrow function's body. As a consequence, arrow functions cannot be used as generators
* Function body
  * Arrow functions can have either a "concise body" or the usual "block body"
  ```
  var func = x => x * x;                  
  // concise body syntax, implied "return"

  var func = (x, y) => { return x + y; }; 
  // with block body, explicit "return" needed
  ```
* Returning object literals
  * Using the concise body syntax to return object literals will not work as expected
  * It will be parsed as a sequence of statements, not an object literal
  * Correct syntax: `var func = () => ({foo: 1});`
* Line breaks
  * An  arrow function cannot contain a line break between its parameters and its arrow
* Parsing order
  ```
  let callback;

  callback = callback || function() {}; // ok

  callback = callback || () => {};      
  // SyntaxError: invalid arrow-function arguments

  callback = callback || (() => {});    // ok
  ```

### <a name="Defaults">[Default parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)</a>

* Default function parameters allow named parameters to be initialized with default values if no value or `undefined` is passed
* Syntax
  ```
  function [name]([param1[ = defaultValue1 ][, ..., paramN[ = defaultValueN ]]]) {
     statements
  }
  ```
* Description
  * If no value is provided for a given parameter, it is instead assigned to the default parameter
* Examples
  * Passing `undefined` vs other falsy values
    * Passing nothing or passing `undefined` will use the default value. Other falsy values (such as `null`) will not use the default
  * Evaluated at call time
    * The default argument is evaluated at call time
    * A new object is created each time the function is called
  * Default parameters are available to later default parameters
    * Default parameters defined beforehand are available to later default paremeters
    * `function greet(name, greeting, message = greeting + ' ' + name) { ... }`
  * Functions defined inside function body
    * Functions declared in the function body cannot be referred to inside the outer function's default parameters
  * Destructured parameter with default value assignment
    * You can use default value assignment with the destructuring assignment notation
    * `function f([x, y] = [1, 2], {z: z} = {z: 3}) { ... }`

### <a name="ForOf">[For...of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)</a>

* The `for...of` statement creates a loop iterating over iterable objects, including `String`, `Array`, Array-like objects, `TypedArray`, `Map`, `Set`, and user defined iterables
* Syntax
  ```
  for (variable of iterable) {
    statement
  }
  ```
  * `variable` - On each iteration a value of a different property is assigned to variable
  * `iterable` - Object whose iterable properties are iterated
* Examples
  * Iterating over an `Array`
    ```
    let iterable = [10, 20, 30];

    for (let value of iterable) {
      value += 1;
      console.log(value);
    }
    // 11
    // 21
    // 31
    ```
    * You can use `const` if you don't reassign the variable inside the loop
  * Iterating over a `String`
    ```
    let iterable = 'boo';

    for (let value of iterable) {
      console.log(value);
    }
    // "b"
    // "o"
    // "o"
    ```
  * Iterating over a `TypedArray`
    ```
    let iterable = new Uint8Array([0x00, 0xff]);

    for (let value of iterable) {
      console.log(value);
    }
    // 0
    // 255
    ```
  * Iterating over a `Map`
    ```
    let iterable = new Map([['a', 1], ['b', 2], ['c', 3]]);

    for (let entry of iterable) {
      console.log(entry);
    }
    // ['a', 1]
    // ['b', 2]
    // ['c', 3]

    for (let [key, value] of iterable) {
      console.log(value);
    }
    // 1
    // 2
    // 3
    ```
  * Iterating over a `Set`
    ```
    let iterable = new Set([1, 1, 2, 2, 3, 3]);

    for (let value of iterable) {
      console.log(value);
    }
    // 1
    // 2
    // 3
    ```
  * Iterating over the arguments object
    ```
    (function() {
      for (let argument of arguments) {
        console.log(argument);
      }
    })(1, 2, 3);

    // 1
    // 2
    // 
    ```
  * Iterating over a DOM collection
    ```
    // Note: This will only work in platforms that have
    // implemented NodeList.prototype[Symbol.iterator]
    let articleParagraphs = document.querySelectorAll('article > p');

    for (let paragraph of articleParagraphs) {
      paragraph.classList.add('read');
    }
    ```
  * Closing iterators
    * `break`, `continue`, `throw`, or `return` will interrupt the loop and close the iterator
  * Iterating over generators - You can iterate over generators
    * Do not reuse generators, even if the `for...of` loop is terminated early
  * Iterating over other iterable objects
    ```
    var iterable = {
      [Symbol.iterator]() {
        return {
          i: 0,
          next() {
            if (this.i < 3) {
              return { value: this.i++, done: false };
            }
            return { value: undefined, done: true };
          }
        };
      }
    };

    for (var value of iterable) {
      console.log(value);
    }
    // 0
    // 1
    // 2
    ```
  * Difference between `for...of` and `for...in`
    * `for...in` iterates over the enumerable properties of an object in an arbitrary order
    * `for...of` iterates over data that an iterable object defines to be iterated over

### <a name="Map">[Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)</a>

* The `Map` object holds key-value pairs. Any value may be used as either a key or a value
* Syntax
  * `new Map([iterable])`
  * Parameters
    * `iterable` - An `Array` or other iterable object whose elements are key-value pairs
* Description
  * A `Map` object iterates its elements in insertion order
  * A `for...of` loop returns an array of `[key, value]` for each iteration
  * Key equality
    * `NaN` is considered the same as `NaN` (despite `NaN !== NaN`)
    * All other values are considered equal according to the semantics of `===`
  * Objects and maps compared
    * The keys of an `Object` are `Strings` and `Symbols` whereas they can by any value for a `Map`
    * The keys in a `Map` are ordered while keys added to an `Object` are not
    * `Map` has the `size` property while the size of an `Object` must be determined manually
    * `Map` is itself iterable while iterating over an `Object` requires obtaining its keys and accessing the values from the object using them
    * An `Object` has a prototype so there are default keys in the map that could cause collission
    * A `Map` may perform better when adding/removing many key pairs
* Properties
  * `Map.length` - The value of the `length` property is 0
  * `get Map[@@species]` - The constructor function that is used to create derived objects
  * `Map.prototype` - Represents the prototype for the `Map` constructor. Allows the addition of properties to all `Map` objects
* `Map` instances
  * All `Map` instances inherit from `Map.prototype`
  * Properties
    * `Map.prototype.constructor` - Returns the function that created an instance's prototype. This is the `Map` function by default
    * `Map.prototype.size` - Returns the number of key/value pairs in the `Map`
  * Methods
    * `Map.prototype.clear()` - Removes all key/value pairs
    * `Map.prototype.delete(key)` - Returns `true` if an element existed and has been removed or `false` if the element does not exist
    * `Map.prototype.entries()` - Returns an `Iterator` that contains an array of `[key, value]` for each element in the `Map` in insertion order
    * `Map.prototype.forEach(callbackFn[, thisArg])` - Calls `callbackFn` once for each key/value pair present in insertion order
    * `Map.prototype.get(key)` - Returns the value associated to the `key` or `undefined` if there is none
    * `Map.prototype.has(key)` - Returns `true` if key is in `Map`, otherwise `false`
    * `Map.prototype.keys()` - Returns a new `Iterator` object that contains the keys for each element in insertion order
    * `Map.prototype.set(key, value)` - Sets the value for the `key` in the `Map`. Returns the `Map` object
    * `Map.prototype.values()` - Returns an `Iterator` that contains the values for each element in insertion order
    * `Map.prototype[@@iterator]()` - Returns an `Iterator` that contains an array of `[key, value]` for each element in insertion order
* Examples
  * Using the `Map` object
    ```
    var myMap = new Map();

    var keyString = 'a string',
        keyObj = {},
        keyFunc = function() {};

    // setting the values
    myMap.set(keyString, "value associated with 'a string'");
    myMap.set(keyObj, 'value associated with keyObj');
    myMap.set(keyFunc, 'value associated with keyFunc');

    myMap.size; // 3

    // getting the values
    myMap.get(keyString);    // "value associated with 'a string'"
    myMap.get(keyObj);       // "value associated with keyObj"
    myMap.get(keyFunc);      // "value associated with keyFunc"

    myMap.get('a string');   // "value associated with 'a string'"
                             // because keyString === 'a string'
    myMap.get({});           // undefined, because keyObj !== {}
    myMap.get(function() {}) // undefined, because keyFunc !== function () {}
    ```
  * Using `NaN` as `Map` keys
    * `NaN` can be used as a key
    ```
    var myMap = new Map();
    myMap.set(NaN, 'not a number');

    myMap.get(NaN); // "not a number"

    var otherNaN = Number('foo');
    myMap.get(otherNaN); // "not a number"
    ```
  * Iterating `Maps` with `for...of`
    ```
    var myMap = new Map();
    myMap.set(0, 'zero');
    myMap.set(1, 'one');
    for (var [key, value] of myMap) {
      console.log(key + ' = ' + value);
    }
    // 0 = zero
    // 1 = one

    for (var key of myMap.keys()) {
      console.log(key);
    }
    // 0
    // 1

    for (var value of myMap.values()) {
      console.log(value);
    }
    // zero
    // one

    for (var [key, value] of myMap.entries()) {
      console.log(key + ' = ' + value);
    }
    // 0 = zero
    // 1 = one
    ```
  * Iterating `Maps` with `forEach()`
    ```
    myMap.forEach(function(value, key) {
      console.log(key + ' = ' + value);
    });
    // Will show 2 logs; first with "0 = zero" and second with "1 = one"
    ```
  * Relation with `Array` objects
    ```
    var kvArray = [['key1', 'value1'], ['key2', 'value2']];

    // Use the regular Map constructor to transform a 2D key-value Array into a map
    var myMap = new Map(kvArray);

    myMap.get('key1'); // returns "value1"

    // Use the Array.from function to transform a map into a 2D key-value Array
    console.log(Array.from(myMap)); // Will show you exactly the same Array as kvArray

    // Or use the keys or values iterators and convert them to an array
    console.log(Array.from(myMap.keys())); // Will show ["key1", "key2"]
    ```
  * Cloning and merging `Maps`
    ```
    var original = new Map([
      [1, 'one']
    ]);

    var clone = new Map(original);

    console.log(clone.get(1)); // one
    console.log(original === clone); // false. Useful for shallow comparison 
    ```
    * The data itself is not cloned
    * Maps can be merged
    ```
    var first = new Map([
      [1, 'one'],
      [2, 'two'],
      [3, 'three'],
    ]);

    var second = new Map([
      [1, 'uno'],
      [2, 'dos']
    ]);

    // Merge two maps. The last repeated key wins.
    // Spread operator essentially converts a Map to an Array
    var merged = new Map([...first, ...second]);

    console.log(merged.get(1)); // uno
    console.log(merged.get(2)); // dos
    console.log(merged.get(3)); // three
    ```
    * Maps can be merged with Arrays
    ```
    var first = new Map([
      [1, 'one'],
      [2, 'two'],
      [3, 'three'],
    ]);

    var second = new Map([
      [1, 'uno'],
      [2, 'dos']
    ]);

    // Merge maps with an array. The last repeated key wins.
    var merged = new Map([...first, ...second, [1, 'eins']]);

    console.log(merged.get(1)); // eins
    console.log(merged.get(2)); // dos
    console.log(merged.get(3)); // three
    ```

### <a name="Set">[Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)</a>

* The `Set` stores unique values of any type
* Syntax
  * `new Set([iterable]);`
  * Parameters
    * `iterable` - All elements in the `Iterable` object are added to the new `Set`. If the iterable is empty or `null`, the `Set` will be empty
* Description
  * `Set` objects are a collection of unique values.
  * Value equality
    * In ECMA2015, `+0` and `-0` are equal. 
    * `NaN` is considered equal to `NaN`
* Properties
  * `Set.length` - The value of the `length` property is 0
  * `get Set[@@species]` - The constructor function that is used to create derived objects
  * `Set.prototype` - Represents the prototype for the `Set` constructor
* `Set` instances
  * All `Set` instances inherit from `Set.prototype`
  * Properties
    * `Set.prototype.constructor` - Returns the function that created an instance's prototype
    * `Set.prototype.size` - Returns the number of values in the set
  * Methods
    * `Set.prototype.add(value)` - Appends a new element to the set. Returns the `Set` object
    * `Set.prototype.clear()` - Removes all elements
    * `Set.prototype.delete(value)` - Removes the `value` from the `Set`. If the value existed, returns `true`, otherwise, returns `false
    * `Set.prototype.entries()` - Returns an `Iterator` that contains an array of `[value, value]` for each element in the `Set` in insertion order. This is kept similar to `Map` so that each entry has the same value for its key and value here
    * `Set.prototype.forEach(callbackFn[, thisarg])` - Calls `callbackFn` once for each value in the `Set` in insertion order. If a `thisArg` parameter is provided, it will be used as the `this` value for each callback
    * `Set.prototype.has(value)` - Returns `true` if the value is in the `Set`, otherwise `false
    * `Set.prototype.keys()` - Is the same function as `Set.prototype.values()`
    * `Set.prototype.values()` - Returns an `Iterator` that contains values for each element in the `Set` in insertion order
    * `Set.prototype[@@iterator]()` - Returns an `Iterator` that contains values for each element in insertion order
* Examples
  * Using the `Set` object
    ```
    var mySet = new Set();

    mySet.add(1); // Set [ 1 ]
    mySet.add(5); // Set [ 1, 5 ]
    mySet.add(5); // Set [ 1, 5 ]
    mySet.add('some text'); // Set [ 1, 5, 'some text' ]
    var o = {a: 1, b: 2};
    mySet.add(o);

    mySet.add({a: 1, b: 2}); // o is referencing a different object so this is okay

    mySet.has(1); // true
    mySet.has(3); // false, 3 has not been added to the set
    mySet.has(5);              // true
    mySet.has(Math.sqrt(25));  // true
    mySet.has('Some Text'.toLowerCase()); // true
    mySet.has(o); // true

    mySet.size; // 5

    mySet.delete(5); // removes 5 from the set
    mySet.has(5);    // false, 5 has been removed

    mySet.size; // 4, we just removed one value
    console.log(mySet);// Set [ 1, "some text", Object {a: 1, b: 2}, Object {a: 1, b: 2} ]
    ```
  * Iterating Sets
    ```
    // iterate over items in set
    // logs the items in the order: 1, "some text", {"a": 1, "b": 2}, {"a": 1, "b": 2} 
    for (let item of mySet) console.log(item);

    // logs the items in the order: 1, "some text", {"a": 1, "b": 2}, {"a": 1, "b": 2} 
    for (let item of mySet.keys()) console.log(item);

    // logs the items in the order: 1, "some text", {"a": 1, "b": 2}, {"a": 1, "b": 2} 
    for (let item of mySet.values()) console.log(item);

    // logs the items in the order: 1, "some text", {"a": 1, "b": 2}, {"a": 1, "b": 2} 
    //(key and value are the same here)
    for (let [key, value] of mySet.entries()) console.log(key);

    // convert Set object to an Array object, with Array.from
    var myArr = Array.from(mySet); // [1, "some text", {"a": 1, "b": 2}, {"a": 1, "b": 2}]

    // the following will also work if run in an HTML document
    mySet.add(document.body);
    mySet.has(document.querySelector('body')); // true

    // converting between Set and Array
    mySet2 = new Set([1, 2, 3, 4]);
    mySet2.size; // 4
    [...mySet2]; // [1, 2, 3, 4]

    // intersect can be simulated via 
    var intersection = new Set([...set1].filter(x => set2.has(x)));

    // difference can be simulated via
    var difference = new Set([...set1].filter(x => !set2.has(x)));

    // Iterate set entries with forEach
    mySet.forEach(function(value) {
      console.log(value);
    });

    // 1
    // 2
    // 3
    // 4
    ```
  * Implementing basic set operations
    ```
    function isSuperset(set, subset) {
        for (var elem of subset) {
            if (!set.has(elem)) {
                return false;
            }
        }
        return true;
    }

    function union(setA, setB) {
        var _union = new Set(setA);
        for (var elem of setB) {
            _union.add(elem);
        }
        return _union;
    }

    function intersection(setA, setB) {
        var _intersection = new Set();
        for (var elem of setB) {
            if (setA.has(elem)) {
                _intersection.add(elem);
            }
        }
        return _intersection;
    }

    function difference(setA, setB) {
        var _difference = new Set(setA);
        for (var elem of setB) {
            _difference.delete(elem);
        }
        return _difference;
    }

    //Examples
    var setA = new Set([1, 2, 3, 4]),
        setB = new Set([2, 3]),
        setC = new Set([3, 4, 5, 6]);

    isSuperset(setA, setB); // => true
    union(setA, setC); // => Set [1, 2, 3, 4, 5, 6]
    intersection(setA, setC); // => Set [3, 4]
    difference(setA, setC); // => Set [1, 2]
    ```
  * Relation with `Array` objects
    ```
    var myArray = ['value1', 'value2', 'value3'];

    // Use the regular Set constructor to transform an Array into a Set
    var mySet = new Set(myArray);

    mySet.has('value1'); // returns true

    // Use the spread operator to transform a set into an Array.
    console.log([...mySet]); // Will show you exactly the same Array as myArray
    ```
  * Relation with `Strings`
    ```
    var text = 'India';

    var mySet = new Set(text);  // Set ['I', 'n', 'd', 'i', 'a']
    mySet.size;  // 5
    ```

## <a name="Forms">Mobile Web Forms</a>

Filling out online forms, especially on mobile devices, can be difficult. To improve the user experience you'll be asked to show that you can use basic HTML5, JavaScript, and the HTML5 Constraint Validation API, to design efficient and secure HTML web forms with:
* Appropriate label tags associated with inputs
* Inputs with appropriate type, name and autocomplete attributes
* Inputs with large touch targets for mobile forms
* Suggestions for user input using the datalist element
* Front-end validation of inputs (e.g., pattern, maxlength, required) and DOM elements, including:
    * Checking validation errors in real-time with pseudo-classes on inputs
    * Form validation prior to submission (Constraint Validation API)

### <a name="AmazingForms">[Create Amazing Forms](https://developers.google.com/web/fundamentals/design-and-ux/input/forms/)</a>

* Design efficient forms
  * Avoid repeated actions
  * Ask only for the necessary information
  * Show form progress to users
  * TL;DR
    * Use existing data to pre-populate fields and be sure to enable autofill
    * Use clearly labeled progress bars to help users get through multi-part forms
    * Provide a visual calendar so users don't have to leave your site and jump to the calendar app on their smartphones
  * Minimize repeated actions and fields
    * Only use as many fields as necessary and take advantage of autofill
    * Look for opportunities to pre-fill information you already know
  * Show users how far along they are
    * Progress bars and menus should accurately convey overall progress through multi-step forms and processes
    * Users dislike overly complex forms and will leave because of them
  * Provide visual calendars when selecting dates
    * Provide a clear calendar so users can have more context when selecting dates
* Choose the best input type
  * Use the best input type for the current context. For example, number pads for number inputs
  * TL;DR
    * Choose the most appropriate input type for your data to simplify input
    * Offer suggestions as the user types with the `datalist` element
  * HTML5 input types
    * HTML5 introduced a number of new input types
    * url - For entering a URL
    * tel - For entering a telephone number
    * email - For entering email addresses
    * search - A text input field styled in a way that is consistent with the platform's search field
    * number - For numeric input
    * range - For number input but the value is less important. It is displayed as a slider
    * datetime-local - For entering a date and time value where the time zone is provided in the local time zone
    * date - For entering a date with no time zone
    * time - For entering a time with no time zone
    * week - For entering a week with no time zone
    * month - For entering a month with no time zone
    * color - For picking a color
  * Offer suggestions during input with datalist
    * `datalist` is a list of suggested input values associated with a form field
    * The browser uses it to suggest autocomplete options as the user types
    ```
    <label for="frmFavChocolate">Favorite Type of Chocolate</label>
    <input type="text" name="fav-choc" id="frmFavChocolate" list="chocType">
    <datalist id="chocType">
      <option value="white">
      <option value="milk">
      <option value="dark">
    </datalist>
    ```
* Label and name inputs properly
  * Good forms provide semantic input types
  * TL;DR
    * Always use `label`s on form inputs and ensure they're visible when the field is in focus
    * Use `placeholder`s to provide guidance about what you expect
    * To help the browser auto-complete the form, use established `name`'s for elements and include the `autocomplete` attribute
  * The importance of labels
    * The `label` element provides direction to the user telling them what information is needed in a form element
  * Label sizing and placement
    * Labels and inputs should be large and easy to press
    * Field labels should be above inputs in portrait and beside them in landscape
  * Use placeholders
    * The placeholder attribute provides a hint to the user about what is expected in the input
    * Placeholders disappear as soon as the user starts typing. **They are not replacements for labels**
  * Use metadata to enable auto-complete
    * You can give hints to the browser by using the `name` and `autocomplete` attributes to for it to guess what should be autocompleted
    * Chrome requires `input` elements to be wrapped in a `<form>` to enable auto-complete
    ```
    <label for="frmNameA">Name</label>
    <input type="text" name="name" id="frmNameA"
      placeholder="Full name" required autocomplete="name">

    <label for="frmEmailA">Email</label>
    <input type="email" name="email" id="frmEmailA"
      placeholder="name@example.com" required autocomplete="email">

    <label for="frmEmailC">Confirm Email</label>
    <input type="email" name="emailC" id="frmEmailC"
      placeholder="name@example.com" required autocomplete="email">

    <label for="frmPhoneNumA">Phone</label>
    <input type="tel" name="phone" id="frmPhoneNumA"
      placeholder="+1-555-555-1212" required autocomplete="tel">
      ```
   * Recommended input `name` and `autocomplete` attribute values
   
     Content type | name attribute | autocomplete attribute
     --- | --- | ---
     Name | name fname mname lname | name(full name) given-name(first name) additional-name(middle name) family-name(last-name)
     Email | email | email
     Address | address city region province state zip zip2 postal country | street-address(one address input) address-line1 address-line2 (two addressess inputs) address-level1(state or province) address-level2(city) postal-code(zip code) country
     Phone | phone mobile country-code area-code exchange suffic ext | tel
     Credit Card | ccname cardnumber cvc ccmonth ccyear exp-date card-type | cc-name cc-number cc-csc cc-exp-month cc-exp-year cc-exp cc-type
     Usernames | username | username
     Passwords | password | current-password(for sign-in forms) new-password (for sign-up and password-change forms)
   * The `autofocus` attribute
     * Desktop browsers immediately move the focus to the input field
     * Mobile browser ignore `autofocus` to prevent the keyboard from randomly appearing
* Avoid common patterns that break Chrome Autofill
  * Field validation pitfalls
    * Autofill does not recognize client-side validation
    * If using client-side validation, be sure to use the correct autofill keywords so data isn't lost or changed unexpectedly
  * Use standard input fields 
    * Use standard form controls instead of creating your own. This is better for accessibility and will work with Chrome Autofill more reliably
  * Don't use fake placeholders in input fields
    * Use `placeholder` instead of setting the value
  * Don't copy the shipping address into the billing address section
  * Ensure that autocomplete attributes are correct
    * Verify spelling of autocomplete attributes is correct or else autofill might not work as expected
* Provide real-time validation
  * Validation tools should tell the user what they need to do before submitting the form
  * TL;DR
    * Leverage the browser's built-in validation patterns like `pattern`, `required`, `min`, `max`, etc.
    * Use JavaScript and the Constraints Validation API for more complex validation requirements
    * Show validation errors in real time and if the user tries to submit an invalid form, show all fields they need to fix
  * Use these attributes to validate input
    * The `pattern` attribute
      * A regular expression used to validate an input field
    * The `required` attribute
      * The field must contain a value before the form can be submitted
    * The `min`, `max`, and `step` attributes
      * Defines the minimum and maximum values for number inputs as well as how they should be incredmented/decremented
    * The `maxlength` attribute
      * Specifies a maximum length for an input or textbox
    * The `minlength` attribute
      * Specifies a minimum length for an input or textbox
    * The `novalidate` attribute
      * Add this attribute to the `form` element to allow the user to submit the form even when the form contains invalid values
  * Use JavaScript for more complex real-time validation
    * The Constraint Validation API can be used for more complex validation
    * `setCustomValidity()` - Sets a custom validation message and the `customError` property of the `ValidityState` object to `true`
    * `validationMessage` - Returns a string with the reason the input failed the validation test
    * `checkValidity()` - Returns `true` if the element satisfies all of its constraints, otherwise `false`. Deciding how to respond to `false` is up to the developer
    * reportValidiity()` - Returns `true` if the element satisfies all of its constraints, otherwise `false`. Deciding how to respond to `false` is up to the user
    * `validity` - Returns a `ValidityState` object representing the validity states of the element
  * Set custom validation messages
    * If a field fails, use `setCustomValidity()` to mark the field invalid and explain why
  * Prevent form submission on invalid forms
    * Use `checkValidity()` on the form to determine if it is valid
  * Show feedback in real-time
    * HTML5 has pseudo-classes that can be used for feedback
    
    Pseudo-class | Description
    --- | ---
    :valid | Sets the style for an input  when the value meets all of the validation requirements
    :invalid | Sets the style for an input when the value does not meet all of the validation requirements
    :required | Sets the style for an inputthat has the required attribute
    :optional | Sets the style for an input that does not have the required attribute
    :in-range | Sets the style for a number input where the value is in range
    :out-of-range | Sets the style for a number input where the value is out of range
    
    * Validation happens immediately upon page load, which can mark some fields immediately as invalid
      * This can be fixed by setting the class with JavaScript after it is visited
      

### <a name="ConstraintValidation">[Constraint Validation](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/HTML5/Constraint_validation)</a>

* Intrinsic and basic constraints
  * HTML5 basic constraints
    * Use semantically appropriate values for the input's `type` attribute
    * Set values on validation-related attributes
  * Semantic input types
  
    Input type | Constraint description | Associated violation
    --- | --- | ---
    `<input type="URL">` | The value must be an absolute URL | Type mismatch contrainst violation
    `<input type="email">` | Must be a valid email pattern | Type mismatch constraint violation
  * Validation-related attributes
  
    Attribute | Input types supporting the attribute | Possible values | Constraint description | Associated violation
    --- | --- | --- | --- | ---
    `pattern` | `text`, `search`, `url`, `tel`, `email`, `password` | A Regex compiled with `global`, `ignoreCase`, and `multiline` flags disabled | The value must match the pattern | Pattern mismatch
    `min` | `range`, `number`, `date`, `month`, `week`, `datetime`, `datetime-local`, `time`, | A valid number/date | The value must be >= the value | Underflow
    `max` | `range`, `number`, `date`, `month`, `week`, `datetime`, `datetime-local`, `time` | A valid number/date | The value must be <= the value | Overflow
    `required` | `text`, `search`, `url`, `tel`, `email`, `password`, `date`, `datetime`, `datetime-local`, `month`, `week`, `time`, `number`, `checkbox`, `radio`, `file`, `<select>*`. `<textarea>*` | None, is a boolean attribute | There must be a value if set | Missing
    `step` | `date`, `month`, `week`, `datetime`, `datetime-local` `time`, `range`, `number` | An integer number of days/months/weeks/seconds | Unless the step is set to any literal, the value must be `min` + an integral multiple of the step | Step mismatch
    `minlength` | `text`, `search`, `url`, `tel`, `email`, `password`, `<textarea>*` | An integer length | The number of characters must not be less than the value | Too short
    `maxlength` | `text`, `search`, `url`, `tel`, `email`, `password`, `<textarea>*` | An integer length | The number of characters must not be greater than the value | Too long
* Constraint validation process
  * Constraint validation is done through the Constraint Validation API through the following
    * A call to `checkValiditiy()` method of a form element which validates only that element
    * `checkValidity()` on the form which checks all constraints
    * Submitting the form
* Complex constraints using HTML5 Constraint API
  * The API can be used to have complex constraints or combine several fields
  * Constraint combining several fields: Postal code validation (Example)
    * Form
    ```
    <form>
        <label for="ZIP">ZIP : </label>
        <input type="text" id="ZIP"> 
        <label for="Country">Country : </label>
        <select id="Country">
          <option value="ch">Switzerland</option>
          <option value="fr">France</option>
          <option value="de">Germany</option>
          <option value="nl">The Netherlands</option>
        </select>
        <input type="submit" value="Validate">
    </form>
    ```
    * Code
    ```
    function checkZIP() {
      // For each country, defines the pattern that the ZIP has to follow
      var constraints = {
        ch : [ '^(CH-)?\\d{4}$', "Switzerland ZIPs must have exactly 4 digits: e.g. CH-1950 or 1950" ],
        fr : [ '^(F-)?\\d{5}$' , "France ZIPs must have exactly 5 digits: e.g. F-75012 or 75012" ],
        de : [ '^(D-)?\\d{5}$' , "Germany ZIPs must have exactly 5 digits: e.g. D-12345 or 12345" ],
        nl : [ '^(NL-)?\\d{4}\\s*([A-RT-Z][A-Z]|S[BCE-RT-Z])$',
                        "Nederland ZIPs must have exactly 4 digits, followed by 2 letters except SA, SD and SS" ]
      };

      // Read the country id
      var country = document.getElementById("Country").value;

      // Get the NPA field
      var ZIPField = document.getElementById("ZIP");

      // Build the constraint checker
      var constraint = new RegExp(constraints[country][0], "");
        console.log(constraint);


      // Check it!
      if (constraint.test(ZIPField.value)) {
        // The ZIP follows the constraint, we use the ConstraintAPI to tell it
        ZIPField.setCustomValidity("");
      }
      else {
        // The ZIP doesn't follow the constraint, we use the ConstraintAPI to
        // give a message about the format required for this country
        ZIPField.setCustomValidity(constraints[country][1]);
      }
    }

    window.onload = function () {
        document.getElementById("Country").onchange = checkZIP;
        document.getElementById("ZIP").oninput = checkZIP;
    }
    ```
* Visual styling of constraint validation
  * Controlling the look of elements
    * `:required` and `:optional` CSS pseudo-classes - Elements that have `required` or don't, respectively
    * `:valid` and `:invalid` CSS pseudo-classes - Elements that validate or don't, respectively

### <a name="ClientSideValidation">[Client-Side Form Validation with HTML5](https://www.sitepoint.com/client-side-form-validation-html5/)</a>

* The `type` Attribute
  * `type` designates the type of input that is expected
  * (Note: This has been covered much more in depth in previous sections)
* The `pattern` Attribute
  * Specifies a Regex for checking against the field value
  * Example: Telephone number: `^\d{3}-\d{3}-\d{4}$` will match a `xxx-xxx-xxxx` phone number
  * Example: Alpha-Numeric Values: `[a-zA-Z0-9]+`
  * Note: I recommend [RegExr](regexr.com) for configuring regexes for use with this
* Giving Hints
  * `title` will provide a hint for when an error is reporting that the field is invalid or when the user hovers over the input
* The `required` Attribute
  * `required` is a boolean attribute that will mark the element as required
  * The form will not submit if an element with `required` is empty

### <a name="DataFormValidation">[Data form validation](https://developer.mozilla.org/en-US/docs/Learn/HTML/Forms/Form_validation)</a>

* What is form validation? 
  * Ensure that the user does not enter data that you are not expecting
  * Different types of form validation
    * Client-side validation
      * JavaScript validation
      * Built-in form validation
    * Server-side validation
      * Validation that occurs on the server after the data has been submitted
      * Slower and less user-friendly than client-side validation but also ensures that the data isn't malicious or incorrect
* Using built-in form validation
  * Validation constraints on input elements - starting simple
  * The required attribute
    * `required` when used with form elements marks it as required and will show an error if not filled
  * Validating against a regular expression
    * Use `pattern` to validate against a regular expression
  * Constraining the length of your entries
    * `minlength` and `maxlength` can be used to constrain the length of text inputs
  * Full example
    * HTML
    ```
    <form>
      <p>
        <fieldset>
          <legend>Title<abbr title="This field is mandatory">*</abbr></legend>
          <input type="radio" required name="title" id="r1" value="Mr"><label for="r1">Mr.</label>
          <input type="radio" required name="title" id="r2" value="Ms"><label for="r2">Ms.</label>
        </fieldset>
      </p>
      <p>
        <label for="n1">How old are you?</label>
        <!-- The pattern attribute can act as a fallback for browsers which
             don't implement the number input type but support the pattern attribute.
             Please note that browsers that support the pattern attribute will make it
             fail silently when used with a number field.
             Its usage here acts only as a fallback -->
        <input type="number" min="12" max="120" step="1" id="n1" name="age"
               pattern="\d+">
      </p>
      <p>
        <label for="t1">What's your favorite fruit?<abbr title="This field is mandatory">*</abbr></label>
        <input type="text" id="t1" name="fruit" list="l1" required
               pattern="[Bb]anana|[Cc]herry|[Aa]pple|[Ss]trawberry|[Ll]emon|[Oo]range">
        <datalist id="l1">
          <option>Banana</option>
          <option>Cherry</option>
          <option>Apple</option>
          <option>Strawberry</option>
          <option>Lemon</option>
          <option>Orange</option>
        </datalist>
      </p>
      <p>
        <label for="t2">What's your e-mail?</label>
        <input type="email" id="t2" name="email">
      </p>
      <p>
        <label for="t3">Leave a short message</label>
        <textarea id="t3" name="msg" maxlength="140" rows="5"></textarea>
      </p>
      <p>
        <button>Submit</button>
      </p>
    </form>
    ```
    * CSS
    ```
    body {
      font: 1em sans-serif;
      padding: 0;
      margin : 0;
    }

    form {
      max-width: 200px;
      margin: 0;
      padding: 0 5px;
    }

    p > label {
      display: block;
    }

    input[type=text],
    input[type=email],
    input[type=number],
    textarea,
    fieldset {
    /* required to properly style form 
       elements on WebKit based browsers */
      -webkit-appearance: none;

      width : 100%;
      border: 1px solid #333;
      margin: 0;

      font-family: inherit;
      font-size: 90%;

      -moz-box-sizing: border-box;
      box-sizing: border-box;
    }

    input:invalid {
      box-shadow: 0 0 5px 1px red;
    }

    input:focus:invalid {
      outline: none;
    }
    ```
  * Customized error messages
    * The validation error messages that are shown can only be altered with JavaScript
    * Use `setCustomValidity()` to customize them
    * HTML
    ```
    <form>
      <label for="mail">I would like you to provide me an e-mail</label>
      <input type="email" id="mail" name="mail">
      <button>Submit</button>
    </form>
    ```
    * JavaScript
    ```
    var email = document.getElementById("mail");

    email.addEventListener("input", function (event) {
      if (email.validity.typeMismatch) {
        email.setCustomValidity("I expect an e-mail, darling!");
      } else {
        email.setCustomValidity("");
      }
    });
    ```
* Validating forms using JavaScript
  * The HTML constraint validation API
  * Constraint validation API properties
  
  Property | Description
  --- | ---
  `validationMessage` | A localized message describing the validation constraints that the control does not satisfy
  `validity` | A `ValidityState` object describing the validity of the element
  `validity.customError` | Returns `true` if the element has a custom error, otherwise `false`
  `validity.patternMismatch` | Returns `true` if the value does not match the provided pattern, otherwise `false`
  `validity.rangeOverflow` | Returns `true` if the value is above the maximum, otherwise `false`
  `validity.rangeUnderflow` | Returns `true` if the value is below the minimum, otherwise `false`
  `validity.stepMismatch` | Returns `true` if the value does not fit the rules provided by the step attribute, otherwise `false`
  `validity.tooLong` | Returns `true` if the element is longer than `maxlength`, otherwise `false`
  `validity.typeMismatch` Returns `true` if the element's value is not the correct syntax, otherwise `false`
  `validity.valid` | Returns `true` if the element has no validity problems, otherwise `false`
  `validity.valueMissing` | Returns `true` if the element has no value but is a required field, otherwise `false`
  `willValidate` | Returns `true` if the element will be validated when the form is submitted, otherwise `false`
  
  * Constraint validation API methods
  
  Method | Description
  --- | ---
  `checkValidity()` | Returns `true` if the element's value has no validity problems, otherwise `false`. If the element is invalid, causes an `invalid` event
  `HTMLFormElement.reportValidity()` | Returns `true` if the element's child controls satisfy their validation constraints
  `setCustomValidity(message)` | Adds a custom error message to the element. If the argument is the empty string, the custom error is cleared
  * Validating forms without a built-in API
    * If the Constraint Validation API isn't available or you don't want to use it, you can still validate using JS the old-fashioned way
    * What kind of validation should I perform? 
      * Determine how to validate your data. It's up to you. Remember that the form data is always text and is always provided as strings
    * What should I do if the form does not validate? 
      * How will you display errors? Will you allow the form to submit anyway?
    * How can I help the user to correct invalid data?
      * Provide as much helpful information as possible
  * Remote validation
    * Sometimes the form validity relies on information on the server (such as checking for a valid username)
    * You can use an AJAX request to check the validity rather than have the user submit the form and receive back an error
    * Remember, be careful when doing this to avoid exposing sensitive data
    * Do not block the form from submitting if the AJAX request does not complete in time

### <a name="HTMLForms">[HTML Forms](https://developer.mozilla.org/en-US/docs/Learn/HTML/Forms)</a>
