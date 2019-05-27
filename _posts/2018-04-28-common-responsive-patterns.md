---
title: "Common Responsive Patterns"
date: 2018-04-28T15:34:30-04:00
toc: true
toc_label: Common Responsive Patterns
toc_sticky: true
categories:
  - Web Development
tags:
  - Udacity
  - Front End Web Developer Nanodegree
  - Notes
  - Class
---


# 01. Web Foundations

#### Column Drop

![1524929697852](C:\Users\Loretta\Documents\e-Learning\Udacity\FrontEndWebDeveloper\Images\01_14ColumnDrop.jpg)

- At narrowest viewport, elements stack one on top of another.
- Elements expand with widening width until first break point is hit. Then two elements are now side by side. Third element is underneath.
- At next breakpoint, things reflow to a three column layout. As things grow even wider, margins are added to sides.

```html
<div class="container">
    <div class="box dark_blue"></div>
    <div class="box light_blue"></div>
    <div class="box green"></div>
</div>
```

```css
.container {
    display: flex;
    flex-wrap: wrap;
}
.box {
    width: 100px;
}

/*First breakpoint*/
@media screen and (min-width: 450px) {
    .dark_blue {
        width: 25%;
    }
    .light_blue {
        width: 75%;
    }
}

/*Second breakpoint*/
@media screen and (min-width: 550px) {
    .dark_blue, .green {
        width: 25%;
    }
    .light_blue {
        width: 50%;
    }
}
```

#### Mostly Fluid

![1524930076162](C:\Users\Loretta\Documents\e-Learning\Udacity\FrontEndWebDeveloper\Images\01_14MostlyFluid.jpg)

More grid-like than column drop pattern.

- At narrowest viewport, elements stack on top of each other. 
- As the layout gets wider, the grid pattern starts to appear.
- At its widest viewport, margins are added on left and right instead of continuing to expand.

```html
<div class="container">
    <div class="box dark_blue"></div>
    <div class="box light_blue"></div>
    <div class="box green"></div>
    <div class="box red"></div>
    <div class="box orange"></div>
</div>
```

```css
/*use Flexbox - set for narrowest viewport*/
.container {
    display: flex;
    flex-wrap: wrap;
}
.box {
    width: 100%
}

/*First breakpoint that sets blue and green elements next to each other*/
@media screen and (min-width: 450px) {
    .light_blue, .green {
        width: 50%;
    }
}
/*Next breakpoint which maintains the 50% on other elements and splits green, red, and orange into showing as three elements in a row*/
@media screen and (min-width: 550px) {
    .dark_blue, .light_blue {
        width: 50%;
    }
    .green, .red, .orange {
        width: 33.333333%;
    }
}
/*Next breakpoint adds margins once the width reaches a certain size*/
@media screen and (min-width: 700px) {
    .container {
        width: 700px;
        margin-left: auto;
        margin-right: auto;
    }
}
```

#### Layout Shifter

![01_14LayoutShifter.jpg](C:\Users\Loretta\Documents\e-Learning\Udacity\FrontEndWebDeveloper\Images\01_14LayoutShifter.jpg)

Requires more planning to maintain. May need to wrap other divs inside another container.

At narrowest viewport, elements stack on top of each other.

```html
<div class="container">
    <div class="box dark_blue"></div>
    <div class="container" id="container2">
        <div class="box light_blue"></div>
        <div class="box green"></div>
    </div>
    <div class="box red"></div>
</div>
```

```css
.container {
    width: 100%; /*Set width to 100 so that elements inside take up full width*/
    display: flex;
    flex-wrap: wrap;
}
.box {
    width: 100%;
}

/*Breakpoint changes dark blue and container to be 50% each*/
@media screen and (min-width: 500px) {
    .dark_blue {
        width: 50%;
    }
    #container2 {
        width: 50%;
    }
}

/*Breakpoint requires change of container2's width to go to 50%, and dark blue/red to 25% each.
To change order, need to specify order for each element. */
@media screen and (min-width: 600px) {
    .dark_blue {
        width: 25%;
        order: 1; /*Setting order to anything greater than 0 makes it appear last*/
    }
    #container2 {
        width: 50%;
    }
    .red {
        width: 25%;
        order: -1; /*Default order of element is 0. Setting to -1 makes it show first*/
    }
}
```

#### Off Canvas

![01_14OffCanvas.jpg](C:\Users\Loretta\Documents\e-Learning\Udacity\FrontEndWebDeveloper\Images\01_14OffCanvas.jpg)

Instead of stacking content vertically, off canvas places less frequently used content (navigation, etc) off screen. It only shows them if the screen is large enough.

- On smallest screen, hides navigation in a hamburger menu icon.
- On other size, content may come in from outside of the screen.

```html
<nav id="drawer" class="dark_blue">
</nav>

<main class="light_blue">
</main>
```

```css
/*Ensure that elements take up full viewport width at default smallest size*/
html, body, main {
    height: 100%;
    width: 100%;
}

/*Set styles for off canvas element*/
nav {
    width: 300px;
    height: 100%;
    position: absolute;
    transform: translate(-300px, 0); /*move off screen*/
    transition: transform 0.3s ease; /*animation*/
}

/*Class for making the element appear*/
nav.open {
    transform: translate(0,0);
}

/*Breakpoint to reposition everything back to its normal spot*/
@media screen and (min-width: 600px) {
    nav {
        position: relative; /*absolute slides in on top of existing content*/
        transform: translate(0,0); /*reset location to be onscreen*/
    }
    body {
        display: flex;
        flex-flow: row nowrap;
    }
    main {
        width: auto;
        flex-grow: 1; /*Allows the element to grow and take up full remaining width of viewport*/
    }
}
```

