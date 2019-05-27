---
title: "Optimizations"
date: 2018-04-29T15:34:30-04:00
toc: true
toc_label: Optimizations
toc_sticky: true
categories:
  - Web Development
tags:
  - Udacity
  - Front End Web Developer Nanodegree
  - Notes
  - Class
---

## 01. Web Foundations

#### Images

**Source set** in image tag: Browser chooses which file it wants and only display that one.

**Picture element** uses media queries to choose which image to use.

#### Tables

##### Hidden Columns

Hides columns based on their importance once the viewport size gets smaller. Use this technique sparingly because it hides information from users completely.

````html
<tr>
    <td>
        <span class="shortName">TOR</span>
        <span class="longName">Toronto Blue Jays</span>
    </td>
    <td class="inning">0</td>
    <td class="inning">0</td>
    <td class="inning">0</td>
    <td class="inning">4</td>
    <td class="inning">0</td>
    <td class="inning">1</td>
    <td class="inning">0</td>
    <td class="inning">0</td>
    <td class="inning">0</td>
    <td class="final">5</td>
</tr>
````

```css
body {
    margin: 1em;
}
/*Most important info is shortName and final. Other table columns can be hidden by default*/
.longName {
    display: none;
}
.inning {
    display: none;
}
```

##### No More Tables

Within a smaller viewport, the table is collapsed and resembles a long list. All of the data is visible.

```html
<table>
    <thead>...</thead>
    <tbody>
        <tr>
            <td data-th="Team">...</td>
            <td data-th="1st">...</td>
            <td data-th="2nd">...</td>
            <td data-th="3rd">...</td>
            <td data-th="4th">...</td>
            <td data-th="5th">...</td>
            <td data-th="6th">...</td>
            <td data-th="7th">...</td>
            <td data-th="8th">...</td>
            <td data-th="9th">...</td>
            <td data-th="Final">...</td>
        </tr>
    </tbody>
</table>
```



```css
/*Under 500px width, don't want table to be a "table" anymore*/
@media screen and (max-width: 500px) {
    /*Force all table tags to render as display block*/
    table, thread, tbody, th, td, tr {
        display: block;
    }
    /*Get rid of table headers by positiong it way off screen. Could set display: none but that causes issues for accessibility*/
    thead tr {
        position: absolute;
        top: -9999px;
        left: -9999px
    }
    /*Set left padding and position of elements to relative*/
    td {
        position: relative;
        padding-left: 50%;
    }
    /*Add row labels with psuedo selector*/
    td:before {
        position: absolute;
        left: 6px;
        /*Set label for the row
        This line pulls the values from the data-th of each of the td elements and sets them as the label of the row. Ie: data-th="Team" becomes the text used on that row*/
        content: attr(data-th);
        font-weight: bold;
    }
}
```

##### Contained Tables

An easy way to contain a table to a viewport is to wrap it in a div, set the width to 100% and overflow-x to auto. Instead of breaking out of the viewport, the table will take up the same width but scrolls within the viewport.

```html
<div class="contained_table">
    <table>
        <thead></thead>
        <tr>
            <th>Team</th>
            <th>1st</th>
            <th>2nd</th>
            <th>3rd</th>
            <th>4th</th>
            ...
        </tr>
    </table>
</div>
```

```css
div.contained_table {
    width: 100%;
    overflow-x: auto;
}
```

##### Fonts

When considering text on a website, there are expectations that the font size never becomes too small or unreadable. A good starting place for the minimums is as follows:

- font-size:16px and line-height: 1.2em
- Measure (length of a line): ~65 characters per line
- Consider placing breakpoints based on measures.

##### Minor Breakpoints

Small changes to a website, such as adding margins and padding or to increase the font size. 

```html
<div class="weather-forecast" role="main">
    <div class="location">New York, NY</div>
    <div class="date">Tuesday, April 15th</div>
    <div class="desc">Overcast</div>
    <div class="current">...</div>
    <div class="seven-day">...</div>
</div>
```

```css
@media screen and (min-width: 450px) and (max-width: 550px) {
    /*Increases base font*/
    body {font-size: 1em; }
    /*Changes the low and high temperature to be inline block (on same line together)*/
    .seven-day-fc .temp-low,
    .seven-day-fc .temp-high
    {
        display: inline-block;
        width: 30%;
    }
    /*Increases icon size*/
    .seven-day-fc .icon {
        width: 60px;
        height: 60px;
    }
}

@media screen and (min-width: 700px) {
    .weather-forecast {
        width: 700px; /*Width will remain at 700px when viewport expands*/
        margin-left: auto; 
        margin-right: auto;
        display: block;
    }
}
```

