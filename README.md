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

### <a name="OfflineCookbook">[The Offline Cookbook](https://jakearchibald.com/2014/offline-cookbook/)</a>

### <a name="Cache">[Cache - MDN](https://developer.mozilla.org/en-US/docs/Web/API/Cache)</a>

### <a name="Storage">[Storage](https://developer.mozilla.org/en-US/docs/Web/API/Storage)</a>

### <a name="LocalStorage">[Local Storage And How To Use It On Websites](https://www.smashingmagazine.com/2010/10/local-storage-and-how-to-use-it/)</a>

### <a name="IndexedDB">[IndexedDB API](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API)</a>

### <a name="DevTools">[Get Started with Analyzing Network Performance in Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools/network-performance/)</a>

## <a name="Test">Testing and Debugging</a>

### <a name="JSDevTools">[Get Started with Debugging JavaScript in Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools/javascript/)</a>

### <a name="Console">[Diagnose and Log to Console](https://developers.google.com/web/tools/chrome-devtools/console/console-write)</a>

### <a name="DebugSW">[Debugging Service Workers](https://developers.google.com/web/fundamentals/codelabs/debugging-service-workers/)</a>

## <a name="ES2015">ES2015 Concepts and Syntax</a>

### <a name="ES6Promises">[JavaScript Promises: an Introduction](https://developers.google.com/web/fundamentals/primers/promises)</a>

### <a name="Promise">[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)</a>

### <a name="TemplateLiterals">[Template literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)</a>

### <a name="ArrowFunctions">[Arrow Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)</a>

### <a name="Defaults">[Default parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)</a>

### <a name="ForOf">[For...of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)</a>

### <a name="Map">[Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)</a>

### <a name="Set">[Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)</a>

## <a name="Forms">Mobile Web Forms</a>

### <a name="AmazingForms">[Create Amazing Forms](https://developers.google.com/web/fundamentals/design-and-ux/input/forms/)</a>

### <a name="ConstraintValidation">[Constraint Validation](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/HTML5/Constraint_validation)</a>

### <a name="ClientSideValidation">[Client-Side Form Validation with HTML5](https://www.sitepoint.com/client-side-form-validation-html5/)</a>

### <a name="DataFormValidation">[Data form validation](https://developer.mozilla.org/en-US/docs/Learn/HTML/Forms/Form_validation)</a>

### <a name="HTMLForms">[HTML Forms](https://developer.mozilla.org/en-US/docs/Learn/HTML/Forms)</a>
