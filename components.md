---
title: "Components"
---

<a id="website-custom-components-and-plugins"></a>
## Website Custom Components and Plugins 


**Table of Contents**

<!-- MarkdownTOC levels="3" autolink="true" autoanchor="true" style="ordered" -->

1. [Global dependancies](#global-dependancies)
1. [Carousel Slider](#carousel-slider)
1. [Calendar of Events](#calendar-of-events)
1. [Frequently Asked Questions \(FAQ\)](#frequently-asked-questions-faq)

<!-- /MarkdownTOC -->

<a id="global-dependancies"></a>
### Global dependancies 

Note that all of the custom functions described here depend on styles and scripts define in the [Site header](/Docs/header_code) and or [Site footer](/Docs/footer_code), which is accessible via Home -> Settings -> Advanced -> Code Injection as:

- jQuery styles and script links
- [Custom function](/Docs/javascript.html) from UIL Github account
- [Custom styles](/Docs/styles.html) from UIL Github account
- Slick plugin styles and script links
- Lazy Summaries styles and script links in footer. 

<a id="carousel-slider"></a>
### Carousel Slider 

A SquareSpace summary block can be enabled as a carousel (via the design tab).   However, native nativation is a little limited.  We preferred a more intuitive naviation that automatically wraps around when the end is hit.

To accomplish that goal, a plugin called **Slick Carousel** ([https://kenwheeler.github.io/slick/](https://kenwheeler.github.io/slick/))was implemented in addition to some custom JavaScript code wrapper.  To implement this, you must first define a standard SquareSpace carousel.  Then, immediately before the caroussel, add a code block with the following: 

**Code block before carousel**
```
$(document).ready(function(){
    createCarousel ('#announcementCarousel');    
});
</script>
<div id="announcementCarousel"></div>
```

Note that the function call "**createCarousel**" is being passed the selector id (#announcementCarousel) for the div tag that follows.  If you have multiple carousels on the same page, then the selector id's must be unique.  Ie. the second carousel might use #announcementCarousel2. 

<a id="dependancies"></a>
**Carousel Slider Depenancies**

- Slick plugin Script/Style links in [header](/Docs/header_code.html)
- Code block (see above)
- Defined SquareSpace summary block as carousel

<a id="calendar-of-events"></a>
### Calendar of Events

The calendar custom function grabs data from a Google spreadsheet (calendar) and embeds Google calendars within an iframe on the page.  It uses the spreadsheet information to get the associated Google ID, iframe embed code, museum and title.

The calendar of events block is emplemented by adding a code block to the page with the following:

**Code block for calendar of events**
```
<script>
$(document).ready(function() {
  build_calendars('#calendarDiv',1, false);  
})
</script>
<body>
<div id="calendarDiv"></div>
```
Note that the function call "**build_calendars**" is being passed the number "2", which tells the function to select calendar number 2 (Leslie Science) as the default when opened. 

**Syntax:**

*build_calendars(selector, activeTab, expanded)*

**Where *activeTab* is:**
d
- 0, All museums (or null)
- 1, Ann Arbor Hands On
- 2, Leslie Science
- 3, Yankee Air Museum
- 4, Challenger Learning Center

**Calendar Dependancies**
- Code block (see above)
- [Spreadsheet data](/Docs/spreadsheets.html)

<a id="frequently-asked-questions-faq"></a>
### Frequently Asked Questions (FAQ)

