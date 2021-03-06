# Week 10: Small Multiples, Map Start

## Homework Review

## Javascript and D3 Tips


### Javascript's getFullYear

````
var d = new Date();
var n = d.getFullYear();
````

Also have a look at [moment.js](http://momentjs.com/) if you want to do a lot with dates in Javascript.


### D3.map vs. JS Array.map: So Confusing

var countryNames = d3.map(data, function(d){
  return d.Country;
}).keys();

A d3.map function creates a lookup hash table with keys as the items you return in your function.  It's not the same thing as array.map.  Array.map just creates a new array of the items you asked for.

D3.map() is incredibly useful for storing data in objects, though. See https://github.com/mbostock/d3/wiki/Arrays#d3_map.


### Sorting Array Alphabetically, Reminder

````
array.sort(function(a, b) {return d3.ascending(a.Country,b.Country);}); // 
or
array.sort() // if there are just strings in the array!
````

But `function(a,b) {return a - b;}` doesn't work.


### Why: data(function (d) {return d;})

Inside a selection, with data attached, you will be selecting a subset of the data.

Remember in the Nested Selections document... http://bost.ocks.org/mike/nest/:

````
var td = d3.selectAll("tbody tr")
    .data(matrix)
  .selectAll("td")
    .data(function(d, i) { return d; }); // d is matrix[i]
````

### D3's "each" function

From the d3 docs: https://github.com/mbostock/d3/wiki/Selections#each

    # selection.each(function)

    Invokes the specified function for each element in the current selection, 
    passing in the current datum d and index i, with the this context of the 
    current DOM element. This operator is used internally by nearly every 
    other operator, and can be used to invoke arbitrary code for each selected 
    element. The each operator can be used to process selections recursively, 
    by using d3.select(this) within the callback function.

You'll see each with the small multiples today.  It gives you the d, i you need to work with!


### Mike's Process Data on Load function

You can see this in [small_multiples_simple.html](small_multiples_simple.html), a cool trick:

````
function typeFix(d) {
  d.Measles = +d.Measles;
  d.date = parseDate(d.Year);
  return d;
}
````

You invoke it like this:

````
d3.csv("data/deaths_04yearsold_excerpt.csv", typeFix, function(error, data) { ...}
````

Remember, this applies to every row in your data, and your "fix" function must return the row after doing things to it.


## Small Multiples in D3 - More Details

Three ways described by Mike:

* Version 1: http://bl.ocks.org/mbostock/1157787

See [small_multiples_simple.html](small_multiples_simple.html).

This method requires you to calculate the Y axis domain everytime you use it. That makes it harder to create axes labels with it.  Notice that the scale is very different across these graphs but that's not obvious here.  Labeling the last point helps a bit.

* Version 2: http://bl.ocks.org/mbostock/9490313 (uses 'each' and calls the drawing funct)

This variant calls a function on "each" of the data charts you're drawing, from the data. Also, allows easier actual axes drawing.

See my version in [small_multiples_each.html](small_multiples_each.html).

* Version 3 of Mike's saves a separate y scale per data set: http://bl.ocks.org/mbostock/9490516

(I didn't remake that one. I prefer version 2.)


Tutorials by Jim Vallandingham (that unfortunately use Coffee Script):

* Small Multiples with Details on Demand http://vallandingham.me/small_multiples_with_details.html
* Linked Small Multiples, also by Jim V: https://flowingdata.com/2014/10/15/linked-small-multiples/

Jim's Linked Small Multiples article should be read. He has lots of examples that inspired it.  He uses Version 2's style -- an each loop that draws each of the charts.

He also uses the Isotope jquery library: http://isotope.metafizzy.co/  Which you are welcome to use in your own work. (It is okay to use for non-commercial uses.)

See my version in JS: **[linked_small_mults.html](linked_small_mults.html)**

Using some UI from a tutorial by Nathan Yau (http://flowingdata.com/2012/01/05/build-interactive-time-series-charts-with-filters/), I also made a transition version:

**[small_multiples_each_trans.html](small_multiples_each_trans.html)**

and a variant with the scales different across each country, to show the comparison not blown out by Nigeria:

**[small_multiples_each_trans_diffaxis.html](small_multiples_each_trans_diffaxis.html)**

TODO: Create a linked version of Nathan's using Jim's code.

## Intro to Maps in D3

Read Mike's tutorial: http://bost.ocks.org/mike/map/

You don't have to do all of it yet.  We may or may not deal with the command line tools in class.

Let's look at [africa_map.html](africa_map.html).

Example of small multiple maps:

* Small Multiple Maps tutorial: http://blog.webkid.io/multiple-maps-d3/


## Recent Interesting Things

* Google Datasets search engine: https://cse.google.com/cse/publicurl?cx=002720237717066476899:v2wv26idk7m
* More scrollytelling: http://poly-graph.co/timeless/ -- features a bunch of great interactive features. Let's discuss!
* @VisualisingData's best of august 2015 in vis: http://www.visualisingdata.com/2015/10/best-of-the-visualisation-web-august-2015/
* Escape from Mercator: https://mapzen.com/blog/escape-from-mercator
* Greenland piece in NYT today: http://www.nytimes.com/interactive/2015/10/27/world/greenland-is-melting-away.html?hp&action=click&pgtype=Homepage&module=photo-spot-region&region=top-news&WT.nav=top-news


## Homework

Readings:

* https://flowingdata.com/2014/10/15/linked-small-multiples/
* Making of the Guardian piece I showed: https://source.opennews.org/en-US/articles/how-we-made-homan-square-portrait/
* Mike's tutorial: http://bost.ocks.org/mike/map/


**Homework 2 (25pt)**: Make a small multiples display for your own project data. Even if it's only a few multiples!  You can use any of the examples I provided.  I will give extra extra credit points for the more complex work, but the base requirement is to be like the code in small_multiples_simple.html.  Try to stay on your project topic, make something you would really use in it.  Send me the gist as "Week 10, Small Multiples."

Start making plans for your project more concrete.  Implement any charts with your project data that might be useful inside your final project.


