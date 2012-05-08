---
layout: default
---

# Welcome to jQuery++

jQuery++ is a collection of useful jQuery extensions and events.

They are organized in two broad categories:

 - DOM Helpers - helpers to work with DOM function or improve jQuery performance
 - Events - jQuery special events

## Get jQuery++

### Download Builder

Check the files you want to download and a zip file will be created.  The
zip file will contain each individual plugin, and a combined version of all plugins
minified and unminified.

### Using Steal

Add these to your jQuery folder:

### Using AMD

require('jquery/compare')

## $.compare `$(elA).compare(elB) -> Number`

[$.fn.compare](http://donejs.com/docs.html#!jQuery.compare) compares
the position of two nodes and returns a number bitmask detailing how they
are positioned relative to each other. The following list shows the `bitmask` __number__ and what it corresponds to:

* `000000` -> __0__: Elements are identical
* `000001` -> __1__: The nodes are in different documents (or one is outside of a document)
* `000010` -> __2__: #bar precedes #foo
* `000100` -> __4__: #foo precedes #bar
* `001000` -> __8__: #bar contains #foo
* `010000` -> __16__: #foo contains #bar

You can tell if `#foo` precedes `#bar` like:

{% highlight javascript %}
if( $('#foo').compare($('#bar')) & 4 ) {
    console.log("#foo preceds #bar")
}
{% endhighlight %}

This is useful when you want to rapidly compare element positions.  This is
common when widgets can reorder themselves (drag-drop) or with nested widgets (trees).

## $.cookie

[$.cookie](http://donejs.com/docs.html#!jQuery.cookie) wraps the [jQuery cookie](https://github.com/carhartl/jquery-cookie) plugin for easily manipulating cookies. You can use it like this:

{% highlight javascript %}
// Set a session cookie
$.cookie('the_cookie', 'the_value');
$.cookie('the_cookie'); // => 'the_value'
// Set a cookie that expires in 7 days
$.cookie('the_cookie', 'the_value', { expires: 7 });
// delete the cookie
$.cookie('the_cookie', null);
{% endhighlight %}

## $.styles `$(el).styles()`

[$.styles](http://donejs.com/docs.html#!jQuery.styles) is a fast way of getting a bunch of computed styles from an element instead of retrieving them individually. Computed styles reflect the actual style of an element, including browser defaults and CSS settings.

{% highlight javascript %}
$("#foo").curStyles('float','display') //->
// {
//  cssFloat: "left", display: "block"
// }
{% endhighlight %}

## $.dimensions

The [$.dimensions](http://donejs.com/docs.html#!jQuery.dimensions) plugin can set an elements inner and outer width and height including margins and paddings and enables `animate` to animate these values. You can set and read it with:

* `$(el).innerHeight([height])`
* `$(el).outerHeight([height])`
* `$(el).innerWidth([width])`
* `$(el).outerWidth([width])`

And use `$(el).animate({ innerHeight : 100 })` to animate these values. This is useful when you care about animating/settings the visual dimension of an element (which is what you typically want to animate):

{% highlight javascript %}
$('#foo').outerWidth(100).innerHeight(50);
$('#bar').animate({outerWidth: 500});
{% endhighlight %}

## $.selection

Gets or sets the selection

## $.within

## $.Range



## $.event.drag

## $.event.drop

## $.event.hover `hoverinit` `hoverenter` `hovermove` `hoverleave`

[$.event.hover](http://donejs.com/docs.html#!jQuery.hover) is a flexible way to deal with hover related events. You can listen to the `hoverinit`, `hoverenter`, `hovermove` and `hoverleave`:

{% highlight javascript %}
$('#menu').on(".option", "hoverenter", function(){
  $(this).addClass("hovering");
}).on(".option", "hoverleave", function(){
  $(this).removeClass("hovering");
})
{% endhighlight %}

An element is hovered when the mouse moves less than a certain distance in a specific time over the element. You can modify these values either globally by setting `$.Hover.delay` and `$.Hover.distance` or individually during `hoverinit`:

{% highlight javascript %}
$(".option").on("hoverinit", function(ev, hover){
  //set the distance to 10px
  hover.distance(10)
  //set the delay to 200ms
  hover.delay(10)
})
{% endhighlight %}

## $.event.destroyed `destroyed`

The [destroyed](http://donejs.com/docs.html#!jQuery.event.destroyed) event is triggered when the element is removed from the DOM through one of the jQuery [manipulation methods](http://api.jquery.com/category/manipulation/).

{% highlight javascript %}
$('form').on('destroyed', function() {
  // Clean up when a form element has been removed
});
{% endhighlight %}

## $.event.resize `resize`

Listen to [$.event.resize](http://donejs.com/docs.html#!jQuery.event.resize) event can update the

## $.event.swipe `swipeleft` `swiperight` `swipedown` `swipeup` `swipe`

[$.event.swipe](http://donejs.com/docs.html#!jQuery.event.swipe) adds support for swipe motions on touchscreen devices. You can listen to `swipeleft`, `swiperight`, `swipedown`, `swipeup` and a general `swipe` event:

{% highlight javascript %}
$('#swiper').on({
  'swipe' : function(ev) {
    console.log('Swiping');
  },
  'swipeleft' : function(ev) {
    console.log('Swiping left');
  },
  'swiperight' : function(ev) {
    console.log('Swiping right');
  },
  'swipeup' : function(ev) {
    console.log('Swiping up');
  },
  'swipedown' : function(ev) {
    console.log('Swiping down');
  }
});
{% endhighlight %}

Set `$.event.swipe.delay` to the maximum time the swipe motion can take (default is 500ms).

## $.event.key

[$.event.key](http://donejs.com/docs.html#!jQuery.event.key) allows you to define alternate keymaps or overwrite existing keycodes. For example lets map the arrow up, down, left and right keys to the more gamer friendly WASD mapping:

{% highlight javascript %}
$.event.key({
  "w" : 38,
  "a" : 37,
  "s" : 40,
  "d" : 39
});
{% endhighlight %}

You can also call `event.keyName()` to get a string representation of the key pressed, for example backspaces:

{% highlight javascript %}
$("input").keypress(function(ev){
  if(ev.keyName() == '\b') {
    ev.preventDefault();
  }
});
{% endhighlight %}

The following keynames will be returned by default:

- `\b` - backspace
- `\t` - tab
- `\r` - enter key
- `shift`, `ctrl`, `alt`
- `pause-break`, `caps`, `escape`, `num-lock`, `scroll-loc`, `print`
- `page-up`, `page-down`, `end`, `home`, `left`, `up`, `right`, `down`, `insert`, `delete`
- `' '` - space
- `0-9` - number key pressed
- `a-z` - alpha key pressed
- `num0-9` - number pad key pressed
- `/` `;` `:` = , \- . / \` \[ \\ \] ' "
- `f1-12` - function keys pressed

## $.event.default `eventname.default`

[$.event.default](http://donejs.com/docs.html#!jQuery.event.default) lets you perform default actions for events. A default event runs when all other event handlers have been triggered and none has called `event.preventDefault()` or returned false. To add a default event just prefix it with the *default* namespace:

{% highlight javascript %}
$("div").bind("default.click", function(ev) {
  // ...
});
{% endhighlight %}

## .triggerAsync `$(el).triggerAsync(event, [success], [prevented])`

[$.fn.triggerAsync](http://donejs.com/docs.html#!jQuery.fn.triggerAsync) triggers an event and calls a *success* handler when it has finished propagating through the DOM and `event.preventDefault()` is not called. The *prevented* callback will be used otherwise:

{% highlight javascript %}
$('panel').triggerAsync('show', function(){
    $('#panel').show();
  },function(){
    $('#other').addClass('error');
});
{% endhighlight %}


## $.event.pause `event.pause(), event.resume()`

[$.event.pause](http://donejs.com/docs.html#!jQuery.event.pause) lets you pause and resume events. Pausing an event works similar to [.stopImmediatePropagation()](http://api.jquery.com/event.stopImmediatePropagation/) by calling `event.pause()`. When `event.resume()` is being called propagation will continue. This is great for asynchronous processing in an event handler:

{% highlight javascript %}
$('#todos').bind('show', function(ev){
  ev.pause();

  $(this).load('todos.html', function(){
    ev.resume();
   });
})
{% endhighlight %}

## Get Help

## Why jQuery++

## Developing jQuery++