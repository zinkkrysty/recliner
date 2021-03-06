# Recliner.js
   
Recliner is a super lightweight (1KB), jQuery plugin for lazy loading images, iframes and other dynamic (AJAX) content.

For more information and a live demo see the project page: [http://sourcey.com/recliner](http://sourcey.com/recliner)

The script was born out of necessity when one of our clients was experiencing massive scroll lag on the mobile version of one of their media heavy news sites. It turned out that `lazy-load-xt` was the culprit, so we tested the other lazy load scripts out there but **none** of them meet our simple criteria:

* Lightweight
* Sets stateful CSS classes on elements
* Ability to override event callbacks for custom behaviour
* Can load *any* dynamic content (images, iframes, AJAX) 
* Mobile friendly

Recliner is currently used on some very high traffic sites, so it's well tested and production ready. Being lazy never felt so good, just hook it up, and start sippin' your margaritas!

## Usage

Add jQuery (2.x or 1.x) and Recliner to your HTML source:

``` html
<script src="//code.jquery.com/jquery-1.11.2.min.js"></script>
<script src="recliner.min.js"></script>
```

Instantiate Recliner on elements with the `.lazy` class on document load:

``` javascript
$(function() {
    $(".lazy").recliner({
        attrib: "data-src", // selector for attribute containing the media src
        throttle: 300,      // millisecond interval at which to process events
        threshold: 100,     // scroll distance from element before its loaded
        live: true          // auto bind lazy loading to ajax loaded elements
    });
});
```

You can also progrmatically trigger an update to check for new elements to be loaded (this may be necessary in some egde cases):

``` javascript
$(window).trigger("lazyupdate");
```

You can use Recliner to load a range of different dynamic content. Note that it's good practice to manually specify image dimensions so your page height doesn't go berserk as lazy content is loading.

##### Images

``` html
<img src="some-placeholder-image.png" data-src="image-to-lazy-load.png" class="lazy" width="333" height="333" /> 
```

##### IFrames

``` html
<iframe data-src="http://sourcey.com" width="333" height="333" class="lazy" frameborder="0" vspace="0" hspace="0"></iframe>
```

##### AJAX

``` html
<div data-src="http://sourcey.com" class="lazy" style="width:333px;height:333px">
    Loading, be patient damnit!
</div>
```

## Callbacks

Recliner uses a simple event based API for implementing custom behaviour:

##### lazyload

The `lazyload` event will be triggered on elements that are about to be loaded.

``` javascript
$(document).on('lazyload', '.lazy', function() {
    var $e = $(this);
    // do something with the element to be loaded...
    console.log('lazyload', $e);
});
```
    
##### lazyshow

The `lazyshow` event will be triggered on elements after they have been loaded.
    
``` javascript
$(document).on('lazyshow', '.lazy', function() {
    var $e = $(this);
    // do something with the loaded element...
    console.log('lazyshow', $e);
});
```

## Styling

Recliner will set the following stateful CSS classes of your elements:

* `lazy-loading`: The element is currently being loaded
* `lazy-loaded`: The element has loaded

Using the stateful classes you can add some fancy transitions to your images:

``` css
img {
  opacity: 0;
  transition: opacity .333s ease-in;
}

img.lazy-loaded {
  opacity: 1;
} 
```

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## Issues

If you find any bugs please use the [Github issue tracker](https://github.com/sourcey/recliner/issues).

