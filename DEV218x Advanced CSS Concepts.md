## Module 1 - Responsive Layout Using Media Queries


### Building a Responsive Layout

#### Device Breakpoints

Example of a set of major device breakpoints:

```css
/* Extra small devices (phones, up to 480px) */
@media screen and (max-width: 767px) {...}

/* Small devices (tablets, 768px and up) */
@media (min-width: 768px) and (max-width: 991px) {...}

/* tablets/desktops and up  */
@media (min-width: 992px) and (max-width: 1199px) {...}

/* large like desktops and up */
@media screen and (min-width: 1200px) {...}
```

> Remember to design your website’s layout for the smallest mobile device first, and progressively enlarge the layout design as more screen area becomes available.  


For devices with large screens, it’s best to limit the maximum width of the container panel so that it doesn’t consume the whole screen width, as in the following:

```css
//css for main container
.container {
   max-width: 62.5rem;
}
```

**Avoid using pixels to declare your breakpoints**, since this creates a horizontal scrollbar when the user zooms in on your content. Instead of using pixels, use relative units, which allows browsers to adjust the design, based on the user’s zoom level.


#### Working with Images

To make an image image responsive to the container it is in, you will set the width to 100%. The following is a basic CSS example to make you images responsive:

```css
img {
    max-width: 100%;
    height: auto;
}
```


### Building a Semantic HTML and CSS Foundation

#### To Set Up the CSS File by Adding Reset Files

```css
/***************************
Reset Styles
***************************/

@import 'normalize.css';

/* Change all elements to use border-box */
html {
    box-sizing: border-box;
}

*, *:before, *:after {
    box-sizing: inherit;
}
```

#### To Build Out the Wireframe Structure with Background Colors

```css
/***************************
Theme Styles
***************************/
.background-primary {
  background: #F7941E; /*Orange*/
}
.background-secondary {
  background: #00AEEF; /*Blue*/
}
.background-tertiary {
  background: #8DC63F; /*Green*/
}
```

Structure

```html
<header>Header Content</header>
<main>
    <section>Hero Primary Content</section>
    <section>Image and Text Content</section>
    <section>Featured Content</section>
    <section>Testimonial Content</section>
    <section>Media Objects</section>
    <section>More Content</section>
</main>
<footer>Footer Content</footer>
```

#### To Build a CSS Base

Add `Base Styles` according to Style Guides.

```css
/***************************
Base Styles
***************************/

body {
    color: #414042;
    font-family: Arial, Helvetica, sans-serif;
    font-weight: normal;
}

h1, h2, h3 {
    font-weight: bold;
}

a {
    color: #8dc63f;
    font-weight: bold;
}

a:hover {
    text-decoration: underline;
}
```

### Using Media Queries to Create a Responsive Grid System

#### To Create a Main Container

```css
/***************************
Layout Styles
***************************/

.container {
    padding-right: 15px;
    padding-left: 15px;
    margin-right: auto;
    margin-left: auto;
    max-width: 1170px;
}
```

Inside of `<main>`, add a `<div>` with a class of container around the content of each `<section>`.

> **Note:** When you are finished, your code should look something like the following:
> 
> ```html
> <header class="background-primary">
    <div class="container">
        Header Content
    </div>
    </header>
<main>
    <section class="background-secondary">
        <div class="container">
        Hero Primary Content
        </div>
    </section>
    <section>
        <div class="container">
        Image and Text Content
        </div>
    </section>
    <section class="background-primary">
        <div class="container">
        Testimonial Content
        </div>
    </section>
    <section class="background-secondary">
        <div class="container">
        Media Objects
        </div>
    </section>
    <section class="background-tertiary">
        <div class="container">
        More Content
        </div>
    </section>
</main>
<footer class="background-primary">
    <div class="container">
        Footer Content
    </div>
</footer>
```

#### To Create a Row

Next, we will create a simple grid system that we can customize for the columns we need.

```css
/***************************
Layout Styles
***************************/

.row {
    margin-right: -15px;
    margin-left: -15px;
}

.row:after {
    content: "";
    display: table;
    clear: both;
}
```

Since the `.container` has a padding of 15px, we add a margin of -15px to the `.row` to make it flush with the `.container`.

> **Note:** Since the columns will float left for any device larger than extra small, we need to clear our floats. Go to [https://www.sitepoint.com/clearing-floats-overview-different-clearfix-methods](https://www.sitepoint.com/clearing-floats-overview-different-clearfix-methods/) for more information on clearing floats.


#### To Create a Column

It is best to first build your CSS with mobile devices in mind. So, the first column we are making will stack just like it did in the mobile wireframe.

```css
[class*='col-'] {
    width: 100%;
    padding-left: 15px;
    padding-right: 15px;
}
```

Then: 

- create a media query that will target small devices and above
- define a float that will get your columns to stack horizontally when the screen is small and above

> Now we have columns that are willing to stack horizontally, but they can't because their width is 100%. So, let's build the two different column sizes we need.

```css
/* Media Query excludes extra small devices and includes small and above */
@media (min-width: 48em) {
    [class*='col-'] {
        float: left;
    }
    /* Column Third */
    .col-1-3 {
        width: 33.3333%;
    }
    /* Column Two Thirds */
    .col-2-3 {
        width: 66.6666%;
    }
}
```

#### To Build a Row and Column in Your HTML

Now we replace the following code

```html
<section>
    <div class="container">
        Image and Text Content
    </div>
</section>
```

With this

```html
<section>
    <div class="container">
        <div class="row">
            <div class="col-1-3">
                Circle Image
            </div>
            <div class="col-2-3">
                Content Area
            </div>
        </div>
    </div>
</section>
```

To get a layout that will work fine by default on mobile devices and will switch to another layout when a screen size is more than media query size set in a previous step.

### Self-Assessment Lab: Build a Fluid Layout from a Wireframe

#### Lab Instructions

You will need two rows in the footer, <u>also there is an empty column so use `min-height: 1px` to make sure it does not collapse horizontally.</u> You will also have to add classes .col-1-4 and .col-1-6.


## Module 2 - CSS Modules and High Fidelity Designs


### Resource Content: Building the Base and CSS Modules

#### Layout and Advanced Positioning for Modules

Knowing how to identify and break up modules can be difficult and will take practice. As a rule of thumb, it’s always helpful to separate layout and positioning from the module.

#### Abstracting Layout

For example we might have a design that shows a logo in the header and in the footer. The logo in the header is on the the left side of the screen and the footer logo on the right. In our first attempt to create a logo module in our css we might do something like this:

```css
.logo {

   display:inline-block;
   
   font-family: georgia;
   
   float: left;
   
}
```

However, by always floating the logo to the left we introduced a rule that the logo in the footer would have to override. So it makes sense to pull the layout rule from the module and create some layout modules instead:

```css
.pull-left {

   float:left;

}

.pull-right {

   float:right;

}
```

Now the HTML for the header becomes:

```html
<header>

   <div class=“pull-left”>

      <div class=“logo”>Logo</div>

   </div>

</header>
```


### Tutorial Lab: Build the Base Button Module

#### To Build the Base Button CSS Module

Underneath the `/*Modules*/` comment, add another comment for the button module, add the following code:

```css
/*Button Modules*/
.btn {
	display: inline-block;
	text-align: center;
	white-space: nowrap;
	vertical-align: middle;
	background-image: none;
	border: 1px solid transparent;
	cursor: pointer;
	text-decoration: none;
}
```

The above rules help the button take on some simple button characteristics at the most basic level.

Still working inside the button style, to specify some more base style attributes from your style guide, add the following code:

```css
padding: 12px 30px;
font-size: 1.313em;
font-weight: bold;
border-radius: 4px;
```

> Note: Go to [http://pxtoem.com](http://pxtoem.com) to convert your font sizes from the style guide into web friendly units.


#### To Include a Fade Transition for Button Hover State

To add a fade affect to the `.btn` module, add the following code:

```css
transition: all 0.3s ease 0s;
```

> Note: Go to [http://www.w3schools.com/css/css3_transitions.asp](http://www.w3schools.com/css/css3_transitions.asp) to learn more about CSS Transitions and browser support.



## Module 3 - Sass/Less and Preprocessing

###  Resource Content: CSS Preprocessing Tools

#### Sass/SCSS and Less

Sass uses CSS-compatible, indented syntax to provide customized, well-formatted output. It uses indentation rather than brackets to indicate nesting of selectors, and new lines rather than semicolons to separate properties.

```sass
//Sass Example
$text-color: #333333
body
     color: $text-color
```

SCSS followed the development of Sass; SCSS offers a more flexible syntax, including the ability to write basic CSS. SCSS is an extension of the CSS syntax; therefore, every valid CSS stylesheet is a valid SCSS file with the same meaning. Files using this syntax have the `.SCSS` extension.

```scss
//SCSS Example
$text-color: #333333;
body {
     color: $text-color;
}
```


##### Install Sass

```bash
gem install sass       # install Sass
```
The idea is that you have Sass installed on you computer globally, so now you can type Sass commands into your command-line.


##### Basic Sass Commands

```bash
sass -v                     # check Sass version
sass input.scss output.css  # compile a .scss file into a .css

# watch a .scss file for changes then create the .css file
sass --watch input.scss:output.css

sass-convert style.sass style.scss   # convert Sass to SCSS
sass-convert style.scss style.sass   # convert SCSS to Sass
```

##### Some Basic Syntax Differences from Sass

Remember that both Sass and Less can utilize variables to seclude values. Less uses the `@` symbol while Sass uses the `$` dollar sign to declare a variable, as seen in the following.

```less
//Less Variable
@link-color: blue;
```
```scss
//SCSS Variable
$link-color: blue;
```

`Mixins` also have a small syntax differences between Less and Sass.

```less
//Less mixin for rounding borders
.round-borders (@radius) {
   border-radius: @radius;
}

//Add the round-borders mixin with Less
.box { round-borders(0.5rem); }
```

The same round-border `mixin` in Sass looks as follows:

```sass
//Sass mixin for rounding corners
@mixin round-borders (@radius) {
   border-radius: $radius;
}

//Add the round-borders mixin with Sass
.box { @include round-borders(0.5rem); }
```

##### Using Less

The most efficient way to install Less is on the server, via the `node.js` package manager (`npm`), like so:

```bash
$ npm install -g Less
```


#### Getting Started with Sass/SCSS

```bash
sudo gem install sass            # install Sass
sass -v                          # check Sass version installed

# install nodejs first https://nodejs.org/en/download/
npm install node-sass            # install Node-Sass

node-sass input.scss output.css  # run node-sass
```

For more information about the usage of `Node-Sass`, go to [https://github.com/sass/node-sass](https://github.com/sass/node-sass).


##### File and Folder Structure

The directory where your Sass/SCSS files live is called the input folder. Your processed CSS files are saved to the output folder. These folders can be set up however you like, even nested inside one another. A typical pattern is for the input folder to reside with your site’s regular style sheets folder, like so:

```
  my_project/
    index.html
    css/
      main_style.css
    scss/
      main_style.scss 
      _mixins.scss
      _colors.scss
```


#### Sass Features In-Depth

##### Ampersand

One of the basic features of Sass is the ampersand (&). When you prepend an ampersand to a parameter in a nested Sass selector, that selector becomes attached to the parent selector, instead of being nested below it. This is immediately useful for pseudo class selectors such as :hover or :after that need to be associated with a selector.

The following SCSS

```scss
.parent {
    &:before {...}
}
```
is the same as the following CSS.

```css
.parent:before {...}
```


##### Combinatorial Explosion

You can apply combinatorial explosion to many combinations of selectors. Use it to add space between elements that are direct siblings (the + selector) and direct descendants (the > selector).

>Example: This code sample adds a top margin to any paragraph that is a direct sibling of another paragraph.

The following SCSS

```scss
p {
    + p {
        margin-top:16px;
    }
}
```
is the same as the following CSS.

```css
p + p {
    margin-top:16px;
}
```


##### Extend/Inheritance

Use the extend command, `@extend`, to share a set of CSS properties from one selector to another. This helps you avoid writing multiple class names on HTML elements, and allows for semantic names in your CSS instead. In the following example we will extend our primary container to make a new container:

```scss
//Container Rules
.container {
   max-width: 1024px;
   padding: 0 15px;
   margin: 0 auto;
}

//Container 2 Rules
.container-2 {
   @extend .container;
   padding: 0 45px;
}
```

##### Import

The CSS import option allows you to divide your CSS into smaller, more maintainable portions. Although each time you use `@import` in CSS, *it creates another HTTP request*. Sass builds on top of the current CSS `@import`. Instead of requiring an HTTP request, Sass takes the file that you want to import, and combines it with the file you're importing into. This combine function then serves a single CSS file to the web browser.


##### Mixin

You define a mixin as a CSS rule set. Mixins allow you to define common properties once, and then reuse them throughout the rest of your CSS. Specifically, mixins are a set of definitions that compiles according to parameters or static rules that you set. You can even pass in values to make your mixin more flexible. For example, you can use mixins to write cross-browser background gradients, CSS arrows, or vendor prefixes. To create a mixin, you use the `@mixin` directive and give it a name. To create a clearfix mixin that you can add to selectors that contain floated modules, use the following example:

```scss
//Clearfix Mixin
@mixin clearfix() { 
   &:before,
   &:after {
      content: "";
      display: table;
   }
   &:after {
      clear: both;
   }
}

//Add Clearfix to row
.row {
   @include clearfix();
}
```


### Tutorial Lab: Getting Started Transpiling SCSS into CSS

#### To Install a Node.js Version of Sass called Node-Sass

1. Download and install [Node.js](https://nodejs.org/en/download/)
2. To install Node-Sass globally

```bash
sudo npm install -g node-sass
```


#### To Set Up a Task Runner with Visual Studio Code to Transpile your SCSS into CSS

1. In Visual Studio Code, under the **View** menu, click **Command Palette**.
2. In the **Command Palette** pane, to set up a task runner, type **Configure Task Runner** and then **Other**. 
3. Replace code

	```json
	///////////////////
	// ORIGINAL CODE //
	///////////////////
	{
	    // See https://go.microsoft.com/fwlink/?LinkId=733558
	    // for the documentation about the tasks.json format
	    "version": "0.1.0",
	    "command": "echo",
	    "isShellCommand": true,
	    "args": ["Hello World"],
	    "showOutput": "always"
	}
	
	///////////////////////
	// REPLACE WITH THIS //
	///////////////////////
	{
	    "version": "0.1.0",
	    "command": "node-Sass",
	    "isShellCommand": true,
	    "args": ["scss/styles.scss", "css/styles.css"]
	}
	```

4. To run the task that you just created, press `SHIFT + CONTROL + B`


#### To Create Separate SCSS Files from stylesheet.css

Create file **styles.scss** in **scss** folder and import all the parts into it.

```scss
@import "base/normalize";
@import "base/base";
@import "base/media-queries";   
@import "layouts/layout";
@import "modules/bg-image";
@import "modules/buttons";
@import "modules/header";
@import "modules/hero";
@import "modules/logo";
@import "modules/media";
@import "modules/nav";
@import "themes/theme";
```
> **Warning!** Make sure that files with `mixins` defined are imported before files that use those mixins

To combine all the files into **css** file press `SHIFT + CONTROL + B`.


### Tutorial Lab: Build Desktop Header Section with Variables and Media Query Mixins

#### To Create a Breakpoint Variable and Media Query Mixins

In the base folder, open media-queries.scss, and then, to create a media-query variable, enter the following code:

```scss
$mq-1: 48em !default; /* 768px / 16px = 48em */
```

> Note: Using !default defines the variable with that value unless it has already been assigned. Go to [https://robots.thoughtbot.com/sass-default](https://robots.thoughtbot.com/sass-default) to learn more. 

In media-queries.scss, to create a mixin that will apply only to extra small devices, enter the following code:

```scss
@mixin extra-small-only {
    @media only screen and (max-width : $mq-1 - 0.0625) {
        @content;
    }
}
```

> Note: By subtracting 0.0625 from your mq-1 variable, you are basically removing a pixel. You remove the pixel so that the next media query mixin will not overlap.

Below the mixin that you just created, to add a new mixin for devices small and above, enter the following code:

```scss
@mixin small-and-above {
    @media only screen and (min-width : $mq-1) {
        @content;
    }
}
```

#### To Style the Logo Module for Devices Small and Above

Open **logo.scss** in **scss / modules** folder.  
Update `logo-primary` part so it looks like this

```scss
.logo-primary {
  width: 64px;
  height: 64px;
  @include small-and-above {  // using mixins defined in layouts
    width: auto;
    height: 50px;
    float: left;
  }
}
```


## Module 4 - Web App Testing and Support for Browsers and Devices

### Resource Content: Tools for Testing and Supporting Web Apps

#### Using Modernizr

Modernizr employs feature detection to ensure your website’s compatibility on various browsers. Feature detection is a series of tests, or detects, that programmatically check your website’s features and runs as your web page loads. Modernizr returns the results of the browser’s actual capabilities. You then use that information to tailor your website to a user’s experience. You can find Modernizr at [https://modernizr.com](https://modernizr.com).

Include ModernizerJS in your HTML by adding the following code inside your <head> element:

```html
<head>
   <script src="https://cdnjs.cloudflare.com/ajax/libs/modernizr/2.8.3/modernizr.min.js"></script>
</head>
```

Once this is in place use your web development tools to look at the source of the HTML, you will notice that Modernizer has added class names to your <html> element; as in the following:

```html
<html class=“js no-flexbox canvas canvastext no-webgl no-touch geolocation postmessage no-websqldatabase no-indexeddb hashchange no-history draganddrop”>
```

This allows you to detect information about a browser's support for a CSS property, allowing you to deliver content for specific device and bowser environments.