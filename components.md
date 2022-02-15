---
title: "Components"
---

<a id="website-custom-components-and-plugins"></a>
## Website Custom Components and Plugins 


**Table of Contents**

<!-- MarkdownTOC levels"2,3,4" autolink="true" autoanchor="true" style="ordered" -->

1. [Carousel Slider](#carousel-slider)
1. [Frequently Asked Questions \(FAQ\)](#frequently-asked-questions-faq)

<!-- /MarkdownTOC -->

<a id="carousel-slider"></a>
### Carousel Slider

A SquareSpace summary block can be enabled as a carousel (via the design tab).   However, native nativation is a little limited.  We preferred a more intuitive naviation that automatically wraps around when the end is hit.

To accomplish that goal, a plugin called **Slick Carousel** was implemented in addition to some custom JavaScript code wrapper.  To implement this, you must first define a standard SquareSpace carousel.  Then, immediately before the caroussel, add a code block with the following: 

```
(document).ready(function(){
    createCarousel ('#announcementCarousel');    
});
</script>
<div id="announcementCarousel"></div>
```

Note that the function call "createCarousel" is being passed the selector id for the div tag that follows.  If you have multiple carousels on the same page, then the selector id's must be unique.  


<a id="frequently-asked-questions-faq"></a>
### Frequently Asked Questions (FAQ)

