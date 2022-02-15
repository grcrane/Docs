---
title: "Footer Injection"
---

# Footer Injection

The SquareSpace footer code injection section is normally used to inject additional scripts as needed, although it can also be used to inject styles if necessarey.  Access the neader block via the SquareSpace application and going to Home -> Settings -> Advanced -> Code injection. 

**FOOTER**
```
</script>
<script>
!function(){window.self===window.top||window.top.document.getElementById("lazy-summaries-admin")||function(e,t,s,i,a){if(s.querySelector("#"+t))i&&i(this);else{var n=document.createElement("script");n.src=e+"?cache="+((new Date).getTime()+"").substr(0,8),n.id=t,n.onload=function(){a&&this.remove(),i&&i(this)},s.appendChild(n)}}("https://assets.squarewebsites.org/lazy-summaries/lazy-summaries-admin.js","lazy-summaries-admin",window.top.document.getElementsByTagName("head")[0])}();
</script>
<script>
$(document).ready(function() {
$('<div class="returnPrev"><A HREF="javascript:javascript:history.go(-1)">Back to previous page</A></div>').insertBefore('div.blog-item-wrapper');
$('<div class="returnPrev"><A HREF="javascript:javascript:history.go(-1)">Back to previous page</A></div>').insertAfter('div.blog-item-wrapper');
})
</script>
<style>
div.returnPrev {
	text-align: center;
}
div.returnPrev a {
	text-decoration: underline;
}
</style>
```
***Note**: the above footer injection code is just a sample, and may not represent the current state of the footer section.* 