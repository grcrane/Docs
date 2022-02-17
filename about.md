---
title: "About UIL Documentation"
---

# About this project

<style>
   #myModal table {
  border-collapse: collapse;
  width: auto;
  margin-top: 20px;
}

#myModal td {
    background: #eee;
    font-weight: normal;
    padding: 10px;
    border-bottom: 1px solid black;
}

#myModal tr td:first-child {
    background: rgb(var(--global-bcolor-campweeks));
    color: rgb(var(--global-color-campweeks));
}

/*
.modal {
  display: none; 
  position: fixed; 
  z-index: 999;
  left: 0;
  top: 0;
  width: 100%; 
  height: 100%; 
  overflow: auto; 
  background-color: rgb(0,0,0); 
  background-color: rgba(0,0,0,0.4); 
}


.modal-content {
  background-color: #fefefe;
  xmargin: 190px auto; 
  margin:  0 auto;
  padding: 20px;
  border: 1px solid #888;
  width: 80%; 

  position:  relative;
  background-color: #fefefe;
margin: 0 auto;
padding: 20px;
width: 80%;
max-width: 800px;
border-radius: 20px;
border: 5px solid #6d6d6d;
font-family: "proxima-nova", "Helvetica Neue", Helvetica, Arial, sans-serif;
font-family: Poppins;
font-weight: 300;
font-style: normal;
letter-spacing: 0em;
text-transform: none;
font-size: 1rem;
line-height: 1.8;
position: relative;
margin-top:  150px;
  
}
*/

.modal-content {
  background-color: #fefefe;
  padding: 20px;
  width: 100%;
  border-radius: 20px;
  border: 5px solid #6d6d6d;
  font-family: "proxima-nova", "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-family: Poppins;
  font-weight: 300;
  font-style: normal;
  letter-spacing: 0em;
  text-transform: none;
  font-size: 1rem;
  line-height: 1.8;
  position: relative;
}

.modal {
  display: none;
  position: relative;
  width: 100%;
}

.modal-content .theModalContent {
  margin: 0 20px;
}

#myModal img.campImage {
  width:  100%;
  min-height:  200px;
  object-fit: cover;
}

#myModal div.imageDiv {
    max-width: 500px;
    margin: 0 auto;
}

#myModal .campTitle {
  font-weight:  bold;
  text-align:  center;
}

#myModal .signUpButton {
  display: block;
  clear: both;
  margin-top: 20px;
}

#myModal .signUpButton a {
  padding: .6rem 1.002rem;
  border: 1px solid black;
  margin-top: 20px;
  border-radius: 10px;
}


.close {
  color: #aaa;
  float: right;
  font-size: 28px;
  line-height:  28px;
  font-weight: bold;
  position:  absolute;
  top:  20px;
  right:  20px;
}

.close:hover,
.close:focus,
.bottomClose:hover,
.bottomClose:focus {
  color: black;
  text-decoration: none;
  cursor: pointer;
}

.bottomClose {
  color: #aaa;
   text-align: center;
   display: block;
   font-weight: bold;
   font-size: 1.5em;
   text-decoration: none;
   cursor: pointer;
   margin-bottom: 40px;
}

.idImage div.empty {
    background: #eee;
    width: 150px;
    height: 200px;
}

div.imageThumbs {
  display:  flex;
}

div.imageThumbs a img {
  padding:  10px;
  max-width: 400px;
  max-height: 300px;
  object-fit: cover;
}

/*@mobile:          ~"only screen and (max-width: 750px)";
@tablet:          ~"only screen and (min-width: 751px)";
@tablet-strict:   ~"only screen and (min-width: 751px) and (max-width: 949px)";
@tablet-desktop:  ~"only screen and (min-width: 751px)";
@desktop:         ~"only screen and (min-width: 950px)";
@desktop-strict:  ~"only screen and (min-width: 950px) and (max-width: 1199px)";
@desktop-xl:      ~"only screen and (min-width: 1200px)";
*/

@media only screen and (max-width: 750px) {
   .modal-content {
      width: 90%; 
      margin: 50px auto; 
   }

}

div.classmateContent p:first-child {
   margin-top:  0;
}

div.idImage {
   margin-top:  5px;
}

#classList .gallery-items .errorMessage {
  color:  red;
  font-size:  1.2em;
}
</style>


<script>

	function formatURL(file_id, sheet, query) {
  var d = new Date();
  var n = d.getTime(); 
  var temp = 'https://docs.google.com/spreadsheets/u/0/d/'
  + file_id + '/gviz/tq?headers=1&sheet=' + sheet 
  + '&t=' + n 
  + '&tqx=out:json&headers=1&tq=' + 
  escape(query);
  //alert(temp);
  return temp; 
}

/* https://stackoverflow.com/questions/19491336/how-to-get-url-parameter-using-jquery-or-plain-javascript */
function getSearchParams(k){
 var p={};
 location.search.replace(/[?&]+([^=&]+)=([^&]*)/gi,function(s,k,v){p[k]=v})
 return k?p[k]:p;
}

/* ----------------------------------------------------------- */
/* Initialize variables                                        */
/* ----------------------------------------------------------- */  

//Copy of Master List Public View (aahsclassof63@gmail.com)
var classmatefile_id ="1iF4ZFThYH6qRH9TyoEdxRDjVUplg8LIyolDlkbJbUzY";
var classmatesheet = "Sheet1";
var query = "";
var classmatesurl = formatURL(classmatefile_id, classmatesheet, query);

var imageArray = [];
var imageData = [];
var imageNumberXRef = []; 

var windowposition = 0; 



/* ----------------------------------------------------------- */
/* Fetch one or more URL's from Google                         */
/* ----------------------------------------------------------- */  

async function fetchGoogleDataAll(urls) {
  let promises = [];
  //urls[1] = 'xx'; // to test errors
  var status = ''; 
  urls.map(x => promises.push(
    fetch(x)
      .then((response) => {
        if (response.status >= 200 && response.status <= 299) {
          return response;
        } else {
          status = response.statusText;
        }
      })
      .catch((error) => {
        status = error;
      })
  ));
  const promisResponse = await Promise.all(promises);
  var data3 = []; 
  if (!status) {
    for (let i = 0; i < promisResponse.length; i++){
      var temp = await promisResponse[i].text();
      data3.push(JSON.parse(temp.substr(47).slice(0, -2)));
    }
  }
  return [data3,status];
}

/* ----------------------------------------------------------- */
/* Open modal window for calassmate details                    */
/* ----------------------------------------------------------- */  

function addMyModal () {
  var myModalID = jQuery('#myModal');
  var myModal = `<!-- The Modal -->
  <div id="myModal" class="modal">

    <!-- Modal content -->
    <div class="modal-content">
      <span class="close">Close</span>
      <div class="theModalContent"></div>
         <header class="entry-header">
            <h1 class="entry-title classmateTitle">Brayl, Jim<sup>**</sup></h1>
         </header>
         <div class="idImage" style="float:left;margin-right: 10px;">
            <img alt="" title="Brayl, Jim" class="idPhotoImage" src="">
         </div>
         <div class="classmateContent">
            classmate content
         </div>
         <div style="clear:both;"></div>
         <p class="status"></p>
         <span class="bottomClose">Close</span>
      </div>

   </div>`;
   if (myModalID.length == 0) {
    jQuery('section#primary').append(myModal);
   }
}



function do_classList() {
  var memberRows = []; 

  myTimer1 = setTimeout(function(){ jQuery('div#loading').show(); }, 2000);
  var imagesurl = formatURL(image_file_id, image_sheet, "");
  fetchGoogleDataAll([classmatesurl,imagesurl]).then(dataArrayx => {
    if (dataArrayx[1]) {  // if there was a status error of some kind
      clearTimeout(myTimer1);
      jQuery('div#loading').hide();
      jQuery('#classList .gallery-items')
        .html('<div class="errorMessage">Error fetching spreadsheet, status= ' + dataArrayx[1] + ' try refreshing page</div>');
      return; 
    }
    dataArray = dataArrayx[0][0].table.rows;
    imageData = dataArrayx[0][1].table.rows;

    clearTimeout(myTimer1);
    jQuery('div#loading').hide(); 

    var maxItem = parseInt(jQuery("#classmateItems").val());

    dataArray.forEach(function(item,key) {
      if (item.c[0] != null) {
        var ar = [];
        for (let i = 0; i < 16; i++) {
          var val =  (item.c[i] != null) ? item.c[i].v : '';
          ar.push(val);
        } 
        memberRows.push(ar);
      }
    });

    // Build an array of image names for quick lookup
    // for lookup

    var imageXRef = []; 
    imageData.forEach(function(item,key) {
      var xname =  (item.c[2] != null ) ? item.c[2].v : '';
      imageXRef.push(xname.toUpperCase());
    });

    // Build an array of image numbers for quick lookup
    // for lookup

    imageNumberXRef = []; 
    imageData.forEach(function(item,key) {
      var xnumber =  (item.c[0] != null ) ? item.c[0].v : '';
      imageNumberXRef.push(xnumber);
    });

    memberRows.sort( function(a, b) {
      return a[1].localeCompare(b[1])
        || a[2].localeCompare(b[2]);
    })

    memberRows.forEach(function(item, key) {
      var theclass = "";
      var needinfo = 'no';
      var id = item[0];
      var name = item[1] + ', ' + item[2];
      var themarried = item[4]; 
      var thestatus = (item[7]) ? item[7] : 'Unknown';
      var thetype = (item[8]) ? item[8] : 'classmate'; 
      var thesrc = item[9];
      var thepassed = item[15]; 
      var theobit = item[11]; 
      var google = ''; 
      //var theprofile = item[10];
      var hasprofile = (item[10]) ? 'Y' : 'N';
      var theimages = item[12]; 

      var x = imageXRef.indexOf(thesrc.toUpperCase()); 
   
      if (x > -1) {
        google = (imageData[x].c[3] != null) ? imageData[x].c[3].v : null;
      }   

      if (thesrc) {
        //thesrc = 'https://www.grcrane2.com/aahs63_images/' +thesrc;
        thesrc = 'https://drive.google.com/uc?export=view&id=' + google;
      }
      if (thestatus.toLowerCase() == 'passed') {
        if (thepassed.length < 5 || theobit == '') {
          needinfo = 'yes';
        }
      }
      var out = '<a class="itemLink" href="#" data-row="' + key + '" data-id="' + id + '"><div class="item" data-profile="' + hasprofile + '" data-name="' + name + " " + themarried +
        '" data-type="' + thetype + '" data-status="' + thestatus.toLowerCase() + 
        '" data-href="' + thesrc + '" data-need="' + needinfo +  
        '" data-images="' + theimages + '">\n';
      if (key > maxItem ) {thesrc = '';} 
      if (thesrc && google) {
        out = out + '<img class="' + theclass + '"  src="' + thesrc + '" xalt="No image" /></a>\n';
      }
      else {
        out = out + '<div class="empty"></div></a>'; 
      }
        //var name = item.c[1].v + ', ' + item.c[2].v;
        if (themarried) {name = name + " (" + themarried + ")";}
        out = out + '<div class="caption">\n' +
        name + 
        '</div>\n' +
        '</div>';
          jQuery(out).appendTo('.gallery-container .gallery-items');
    }) 

    jQuery('#search').on('keyup', function (event) {
      do_search();
    });

    do_reset();

    jQuery('#classmateType, #classmateStatus, #classmateItems').on('change',function() {
      do_search();
    })

    /* ----------------------------------------------------------- */
    /* User clicked on one of the classmates.                      */
    /* Switch to the detail block and fill in the information      */
    /* ----------------------------------------------------------- */  

    jQuery('.itemLink').on('click', function (event) {
      event.preventDefault(); 
      windowposition = jQuery(window).scrollTop(); 
      var id = jQuery(this).data("id");
      var row = jQuery(this).data("row");
     // var imgsrc = jQuery(this).find('img').attr('src');
      var imgsrc = jQuery(this).closest('div.item').data('href');
      
      
      var needinfo = jQuery(this).parent().data("need");
      jQuery('.classmateContent').text('');

      console.log(memberRows[row]);
      var profiletext = memberRows[row][10];
      var name = memberRows[row][1] + ', ' + memberRows[row][2];
      jQuery('#classmateInfo header h1').text(name);
      jQuery('.modal-content header h1').text(name);
      var status = (memberRows[row][7]) ? memberRows[row][7] : 'Unknown';
      var theimages = memberRows[row][12];
      jQuery('p.status').text('Status: ' + status);

      var obit = 'Missing'; 
      if (memberRows[row][11]) {
        obit = '<a href="' + memberRows[row][11] + '" target="_blank">' +
        memberRows[row][11] + '</a>\n';
      }
      var death = 'Unknown';
      if (memberRows[row][10]) {
        death = memberRows[row][10];
      }

      var img = '<div class="empty"></div>';
      if (imgsrc) {
        img = '<img class="idPhotoImage profileImg" src="' + imgsrc + '">';

      }
      jQuery('#idImage').html(img);
      jQuery('.idImage').html(img);

      jQuery('p.status').text('Status: ' + status);  
      var formurl = 'https://docs.google.com/forms/d/e/1FAIpQLSdG4w35Ip2u5-q9R7W8R5euIB4CJVqDHTrbIs8lxhx4Rq1jKA/viewform' +
        '?usp=pp_url&entry.1389452980=' + name;
      var temp = '';
      if (status == 'passed') {
        temp = '<br>Date of death: ' + death + 
        '<br>Obituary: <span>' + obit + '</span>';
        jQuery(temp).appendTo('p.status');
        temp = ''; 
      }
      temp = temp + '<div class="updateHelp">Help update, click <a href="' + formurl + '" target="_blank">here</a> if you have additional information.</div>'; 
      jQuery(temp).appendTo('p.status');

      jQuery('div.imageThumbBox, div.classmateVideos').remove(); 

      var temp = ''; 
     
      /* ----------------------------------------------------------- */
      /* Get the classmates profile, if it exists.                   */
      /* ----------------------------------------------------------- */
      
      if (profiletext) {
         jQuery('.classmateContent').html(profiletext);
      }
      else {
         jQuery('.classmateContent').html('<p>No profile found</p>');
      }

      /* ----------------------------------------------------------- */
      /* Get the classmates extra images                             */
      /* ----------------------------------------------------------- */
      
      if (theimages) {
        theimages = theimages.toString();
        var splitimages = theimages.split(":");
        var where = ' WHERE ';
        var sep = '';
        var temp = "<div class=\"imageThumbBox\">\n" +
          "<div class=\"imageThumbs\">\n";
        var thevideo = '';
        splitimages.forEach(function(item,key) { 
          var x = imageNumberXRef.indexOf(item);
          if (x) { 
            console.log(imageData[x]);
            var google = imageData[x].c[3].v;
            var caption =  (imageData[x].c[1] != null) ? imageData[x].c[1].v : '';
            var filename = (imageData[x].c[2] != null) ? imageData[x].c[2].v : '';
            filename = filename.toUpperCase();
            var x2 = filename.indexOf('.MP4');
            
            if (x2 > -1) {
              thevideo = '<div class="classmateVideos">';
              thevideo = thevideo + '<figure><iframe src="https://drive.google.com/file/d/' +
              google + '/preview" width="audo" height="audo" allowfullscreen allow="autoplay"></iframe>' + 
              '<figcaption><b>' + caption + '</b></figcaption></figure></div>';
            }
            else {
              var thesrc = 'https://drive.google.com/uc?export=view&id=' + google;
              temp = temp + '<a href="' + thesrc + '"><img src="' + thesrc + '"></a>';  
            }  
          }
            temp = temp;
        })
        temp = temp+ "</div></div>\n" +
          "<div style=\"clear:both;\"></div>\n" + thevideo;

          jQuery(temp).insertAfter('p.status');
        }   // if (theimages)
        
        //jQuery('#myModal .classmateTitle').focus();

        
        console.log('scrollTop=' + document.querySelector("#myModal .modal-content").scrollTop);
        
        //modal.style.display = "block";
        jQuery('#myModal').show();
        jQuery('main#main').hide();
        jQuery('html').scrollTop(0);
        delete(memberRows);  // all done with this variable
    })

    /* ----------------------------------------------------------- */
    /* Set up the buttons                                          */
    /* ----------------------------------------------------------- */

    jQuery('.backButton').on('click', function (event) {
      jQuery('#classmateInfo').hide();
      jQuery('.gallery-container').show();
      jQuery('#locateInfo').hide(); 
      
      
    })

    jQuery('.helpLocate').on('click', function (event) {
      jQuery('#classmateInfo').hide();
      jQuery('.gallery-container').hide();
      jQuery('#locateInfo').show(); 
      
    })

    jQuery('#resetValues').on('click',function(event) {
      event.preventDefault(); 
      do_reset(); 
      do_search(); 
      do_page(); 
    })

    addMyModal(); 

    // Get the modal
    var modal = document.getElementById("myModal");

    // Get the <span> element that closes the modal
    var span = document.getElementsByClassName("close")[0];
    var span2 = document.getElementsByClassName("bottomClose")[0];

    // When the user clicks on <span> (x), close the modal
    span.onclick = function(e) {
      e.preventDefault();
      modal.style.display = "none";
      jQuery('main#main').show();
      jQuery(window).scrollTop(windowposition); 
    }
    span2.onclick = function(e) {
      e.preventDefault();
      modal.style.display = "none";
      jQuery('main#main').show();
      jQuery(window).scrollTop(windowposition); 
    }

    // When the user clicks anywhere outside of the modal, close it
    window.onclick = function(event) {
      if (event.target == modal) {
        modal.style.display = "none";
        jQuery('main#main').show();
        jQuery(window).scrollTop(windowposition); 
      }
    } 

    var urlid = getSearchParams("id");
    if (urlid) {
      jQuery('div.item a').filter('[data-id="' + urlid + '"]').trigger('click');
    }

    jQuery('#passedList a').on('click', function(event) {
      event.preventDefault();
      var urlid = jQuery(this).data('id');
      jQuery('div.item a').filter('[data-id="' + urlid + '"]').trigger('click');

    });


    /* ----------------------------------------------------------- */
    /* All set now, clear search and show the class list           */
    /* ----------------------------------------------------------- */

    do_search(); 
    var c = jQuery('.item.showme');
  }).catch(error => {
    alert('Errors encountered: ' + error);
  });
}


jQuery(document).ready(function() {
  do_classList();   
});
</script>
<section id="primary" class="content-single content-area">
		<main id="main" class="site-main" role="main">
      
<div id="classList">
   <div class="gallery-container">
      <div class="title">
         <h2>AAHS Class of '63</h2>
         <div class="helpLocate"><a href="#">Help Us Locate Someone</a></div>
      </div>
      <div id="searchBoxes">
         <div class="searchBox">
            Items: 
            <select name="classmateItems" id="classmateItems">
               <option value="10">10</option>
               <option value="20">20</option>
               <option value="50">50</option>
            </select>
         </div>
         <div class="searchBox">
            Search: <input type="text" id="search">
         </div>
         <div class="searchBox">
            <label for="classmateType">Type:</label>
            <select name="classmateType" id="classmateType">
               <option value="">Any</option>
               <option value="classmate">Classmate</option>
               <option value="staff">Staff</option>
               <option value="other">Other</option>
            </select>
         </div>
         <div class="searchBox">
            Status: 
            <select name="classmateStatus" id="classmateStatus">
               <option value="">Any</option>
               <option value="passed">Passed</option>
               <option value="found">Found</option>
               <option value="missing">No Contact Info</option>
               <option value="profile">Has Profile</option>
               <option value="need">Passed ?</option>
            </select>
         </div>
         <div class="searchBox">
         </div>
      </div>
      <p id="found"><span class="count"></span><a href="#" id="resetValues">(Clear)</a><div id="markTime"></div></p>
      <div class="text-center">
         <div class="pagination-holder clearfix">
            <div class="light-pagination pagination light-theme simple-pagination">
            </div>
         </div>
      </div>
      <div id="loading">
         <div class="message">Gathering classmate information...</div>
         <div class="spinner"></div>
      </div>
      <div class="gallery-items"></div>
      <p>
      <div class="text-center">
         <div class="pagination-holder clearfix">
            <div class="light-pagination pagination light-theme simple-pagination">
            </div>
         </div>
      </div>
   </div>
   
   <div id="locateInfo">
      <button class="backButton" type="button">Return to classmate list</button>
      <div class="title">
         <h2>Help Us Locate Your Classmates</h2>
      </div>
      <p>
         The Class of '63 Reunion Committee is constantly trying to keep up with informaton 
         about classmates.  Sadly, with over 700 classmates we have lost track of quite a few.
         Some have changed emails, moved, change phone numbers or unfortunately passed away.  
      <p>We could really use your help.  If you see someone you personally know, or have some information about then please, please pass it along to us.
      <p>We will eventually have a handy on-line form for you, but in the mean time, please send us comments and information via email to <a style="text-decoration:underline;" href="mailto:aahs63@aahs.com">aahs63@aahs.com</a>. 
      <div style="width:80%;text-align:center;margin: 0 auto;">
         <br>
         <div style="font-weight:bold;">Your AAHS ’63 Reunion Committee:</div>
         <br>George Crane, Barbara (Stanley) Kramer, Butch Larkins, Carol (Schonberger) Spears, Rick Weid, Chuck Wilkins
         </p>
         <div style="clear:both;"></div>
      </div>
   </div>
</div>

In a word: **Awesome!**

See the [Home page](/Docs/index.html)



***Syntax:***

```
this is a test
sns
sksk
```

> Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
quis nostrud exercitation ullamco laboris nisi.


| Tables   |      Are      |  Cool |
|----------|:-------------:|------:|
| col 1 is |  left-aligned | $1600 |
| col 2 is |    centered   |   $12 |
| col 3 is | right-aligned |    $1 |