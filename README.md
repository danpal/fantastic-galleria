Fantastic Galleria
=========

Fantastic Galleria is the old aino galleria 1.0. 
I tried using the new one, but found it to complex and buggy. 

After I tried finding the old version and failing, I ended up taking the source from an 
old cached version of google code, and fixing it to work with the latest jquery
1.4, and maintaining it myself.

You can see this galleria in action in several sites like Airbnb.com and
http://fantastic-galleria.heroku.com/

Requirements
------------

Fantastic galleria requires JQuery 1.4 or above

Demo
------------

http://fantastic-galleria.heroku.com

Installation
------------

Copy fantastic.galleria.js to your javascript path
Copy galleria.css to your stylesheet path

Do not rename galleria.css file name


Quick Start
-----------
For a rails example take a look at https://github.com/danpal/Fantastic-galleria-website

Add this to your javascripts file:

<pre><code>
$(document).ready(function(){

 $('ul.galleria').galleria(
  {
     history : false,
     clickNext : true,
     insert : '#main_images',
     onImage : function(image,caption,thumb){
               // fade in the image & caption
                if(! (jQuery.browser.mozilla && navigator.appVersion.indexOf("Win")!=-1) ) { // FF/Win fades large images terribly slow
                    image.css('opacity', .9).fadeTo('fast', 1);
                }
                if(caption.html() == ''){
                    caption.fadeOut('fast');
                }
                else{
                    caption.css('display','none').fadeIn('fast');
                }

                //// fetch the thumbnail container
                var _li = thumb.parents('li');

                //this creates problems
                //// fade out inactive thumbnail this is not working
                //_li.siblings().children().removeClass('selected');
                //_li.siblings().children().fadeTo('fast',0.65);

                //// fade in active thumbnail
                thumb.fadeTo('fast',1).addClass('selected');
 
                // add a title for the clickable image
                image.attr('title','Next image >>');

                jQuery('#galleria_container').trigger('img_change');
         
       },

            onThumb : function(thumb){ // thumbnail effects goes here

                // fetch the thumbnail container
                var _li = thumb.parents('li');

                // if thumbnail is active, fade all the way.
                var _fadeTo = _li.is('.active') ? '1' : '0.65';

                // fade in the thumbnail when finnished loading
                thumb.css({display:'none',opacity:_fadeTo}).fadeIn('fast');

                // hover effects
                thumb.hover(
                    function() { thumb.fadeTo('fast',1); },
                    function() { _li.not('.active').children('img').fadeTo('fast',0.65); } // don't fade out if the parent is active
                )
            }

      });
});


</code></pre>

This will take any image on the ul.galleria class an added to the
galleria.
The images should be in a ul, each image is a different li

Eg in rails:

<pre><code>
  %ul.galleria
    %li= image_tag("photo.jpg")

</code></pre>

Contributing
------------

If you'd like to contribute you can open an issue here in github or
simple fork and ask for a pull request.


Credits
-------

Fantastic galleria is maintained by Daniel Palacio

Aino Galleria is originally by David Hellsing (monc.se)

License
-------

 * Licensed under the GPL licenses.

