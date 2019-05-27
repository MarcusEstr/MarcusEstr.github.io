---
title: "Building Up"
date: 2018-04-28T15:34:30-04:00
toc: true
toc_label: Building Up
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

#### Media Queries

They allow you to utilize a specific CSS stylesheet when needed, ie when the viewport is wider than 500 px. There is also a media style for printing, to style the printed page.

```html
<link rel="stylesheet" media="screen and (min-width:500px)" href="over500.css">
```

Media queries can also be embedded in the CSS.

```css
/*Minimum width a which the @media CSS is applied. (500px)*/
@media screen and (min-width: 500px) {
    body {
        background-color: green;
    }
}
```

#### Breakpoints

Layout changes to a website based on the size of the browser window. 

Deciding where to put breakpoints should be based on the content itself. Starting from smallest, slowly expand the page to see where the "small", "medium", and "large" breakpoints should be according to viewport.

#### Flexbox

Typically, divs are situated within a containing div and appear on screen one under another. However, if you **set the container element's** CSS with ```display: flex;``` then they are now flexible elements in a single row, by default. 

Set ```flex-wrap: wrap;``` in addition to the display attribute specify that the elements will wrap within the container element.

```flex-item: order;``` allows elements to change position as opposed to always staying in the order they were written into the HTML at. 

This works with screen resizing well as a way to specify the order of elements at different views. To set order numbers, add it to CSS:

```css
@media screen and (min-width: 700px) {
    .dark_blue {width: 100%; order: 4;}
    .light_blue {order: 5;}
    .green {order: 2;}
    .orange {order: 3;}
    .red {order: 1;}
}
```



### Quizzes 

#### Which styles are applied?

```css
@media screen and (max-width: 400px) {
    body {
        background-color: red;
    }
}
@media screen and (min-width: 401px) and (max-width: 599px) {
    body {
        background-color: green;
    }
}
@media screen and (min-width: 600px) {
    body {
        background-color: blue;
    }
}
```

