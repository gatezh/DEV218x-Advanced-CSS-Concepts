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

