---
title: "Why Responsive"
date: 2018-04-28T15:34:30-04:00
toc: true
toc_label: Why Responsive
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

#### Emulators for Testing

Browsers: [BrowserStack](https://www.browserstack.com/)

Devices: Chrome Developer Tools (click on Phone icon)

#### Chrome Mobile Debugging

1. Open website to be debugged on phone.
2. Open [chrome://inspect/#devices](chrome://inspect/#devices) on desktop Chrome.
3. Connect phone via USB to PC. Allow USB debugging.

### 12: Starting Small

#### Pixels

**Hardware pixels**:  This is the width and height which we are used to seeing with regards to screens, IE: listed as 1920 x 1080 or 800 x 600. This is the pixel density.

**Device Independent Pixels (DIP)**: Browsers report width in number of DIPS. This is a unit of measurement that relates pixels to a real distance. A DIP takes up the <u>same amount of space</u> on a display regardless of pixel density of the display.

**Q**: What happens then when you open a website on a device with 2560 x 1440 resolution? 

**A**: In the example of a Chromebook Pixel, its browser has a viewport of 1280 DIPs. This is scaled up to 2560 hardware pixels. The is a pixel ratio of 2 - one DIP for every two hardware pixels.

In the example of a Nexus smartphone, which has 1080 hardware pixels width, the browser has a viewport of only 360 DIPs. The device pixel ratio is 3 - one DIP for every three hardware pixels.

##### Viewport

A viewport should be set on all websites. If it isn't set, this causes the browser to set the viewport and scale content however it sees fit (which could wreak havoc on a mobile device with small screen). Viewport is focused on browser.

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

**device-width:** Tells page to match screen's width in DIPs.

**initial-scale=1**: Tells browser to have a one to one relationship between DIPs and CSS pixels.

**Calculating CSS Pixels (Viewport):**

Maximum viewport width = {Device's hardware pixels width} / {Pixel ratio}

960 px = 1920px / 2

It is better to use relative rather than explicit widths in your CSS. Ie:

```css
img, embed, object, video {
    max-width: 100%;
}
```

##### Tap Targets

When navigating websites on small devices, buttons should be at minimum 48px x 48px. This exceeds the average finger width in pixels (which is 40). Also be sure there is enough room between buttons.

```css
nav a, button {
    min-width: 48px;
    min-height: 48px;
}
```

#### Quiz Project Part 1

1. Add a <meta> viewport to the page with initial scale. 

   Simply enter the meta tag seen above.

2. Adjust CSS markup so that everything displays in a single column. 

   Look at anything in CSS where it has a fixed width set to anything less than 100% (ie - 800px, 50%, etc). Change them to a full fixed width - width: 100%;

3. Make sure your touch targets are easy to hit. 

   His solution was adding padding to all <a> tags. Padding: 1.5em;

