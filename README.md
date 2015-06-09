jquery-isoselective
===================

An update to Gatsby's isoSelective isotope plugin for jQuery 1.9+ compatibility.


Why an update?
--------------

[David DeSandro](http://desandro.com)'s lovely [isotope v1](http://isotope.metafizzy.co/v1/) does the job for most filtering and sorting applications, but sometimes you need to **combine filter selections** or **toggle filters**.

Alexander 'Gatsby' Jones (gatsbyart.com - site no longer online) smartly came up with isoSelective, which accomplishes exactly that.

However, isoSelective's last release still relied on jQuery's `.live()` method, which was deprecated as of jQuery 1.7 and removed altogether in jQuery 1.9. If you're running jQuery 1.9 or newer, isoSelective won't work for you.

Fortunately, replacing `.live()` with `.on()` in one spot does the trick.


New feature: preventEmpty
-------------------------

Using isoSelective filtering, it's possible to end up with all filters toggled off, in which case no isotope items are visible anymore. I've added the `preventEmpty` option to allow a choice between showing an empty isotope container or making all items visible again.

The default value for `preventEmpty` is `false`, which will behave as isoSelective has in the past (allowing an empty isotope container when all filters are toggled off).

```javascript
$container.isoSelective({
    linkSelector: 'a.filter',
    attrSelector: 'data-filter',
    activeClass: 'toggledOn',
    preventEmpty: true // when all filters are toggled off, change filter to "*" and show all items
});
```

bugfix: IE8
-----------

Using the `commonAncestor()` function, isoSelective automatically finds the parent element of your `linkSelector` elements. However, Internet Explorer 8 throws an error on the `.slice()` method here:

```javascript
parents[i] = parents[i].slice(parents[i].length - minlen);
```

If you're supporting IE8 and want to avoid hitting that error, pass the parent container selector as part of your isoSelective options:

```javascript
$container.isoSelective({
    linkSelector: 'a.filter',
    linkParentSelector: 'div#filtration',
    attrSelector: 'data-filter',
    activeClass: 'toggledOn',
    preventEmpty: true
});
```


Download the updated isoSelective plugin here:
----------------------------------------------
* [jquery.isoSelective.js](https://raw.github.com/simmerdesign/jquery-isoselective/master/jquery.isoSelective.js), 4.641 kb
* [jquery.isoSelective.min.js](https://raw.github.com/simmerdesign/jquery-isoselective/master/jquery.isoSelective.min.js), 1.721 kb


Usage
-----

Complete documentation for using isoSelective (which doubles as an isoSelective demo) *is* ~~still available here: http://www.gatsbyart.com/plugins/isoSelective/~~ *no longer available online*. I didn't grab it before it was taken down either.

The basic isotope setup is something like this:
```javascript
$container = $('#container');
$container.isotope({
    // options
    itemSelector : '.item'
});
```
    
**You'll do that first whether using isotope or isoSelective filtering.**
    
To enable isotope filtering you'd do something like this:
```javascript
// set up isotope filters
$('a.filter').click(function(){
    var selector = $(this).attr('data-filter');
    $container.isotope({filter:selector});
    return false;
});
```
    
If you're using isoSelective, however, you'll do something like this instead:
```javascript
// set up isoSelective filters
$container.isoSelective({
    linkSelector: 'a.filter',
    attrSelector: 'data-filter',
    activeClass: 'toggledOn',
    preventEmpty: true
});
```


What about Isotope v2? Is this compatible?
------------------------------------------

Sorry, isoSelective is only compatible with [Isotope v1](http://isotope.metafizzy.co/v1/) for now. If you'd like to take on porting isoSelective to [Isotope v2](http://isotope.metafizzy.co/), you'll probably beat me to it.
