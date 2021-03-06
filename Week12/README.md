
# Week 12: Storytelling Tools: Scrolling, Steppers

## Homework Review


## Storytelling Intro

For next week, read this smart paper:

* [Telling Stories with Data](http://vis.stanford.edu/files/2010-Narrative-InfoVis.pdf)


## Steppers ("Slideshow")

Reference:

* http://www.nytimes.com/interactive/2013/05/07/education/college-admissions-gap.html
* Budget Forecast Compared to Reality: http://www.nytimes.com/interactive/2010/02/02/us/politics/20100201-budget-porcupine-graphic.html

Tutorial:

* http://vallandingham.me/stepper_steps.html (includes a jquery version and a pure D3 version)

TODO: Make a simple button stepper example.


## Scroll-Triggered: "Scrollytelling"

The canonical example:
* Snow Fall: http://www.nytimes.com/projects/2012/snow-fall/#/?part=tunnel-creek


Jim Vallandingham's tutorial material:

* His Openvis talk: http://vallandingham.me/think_you_can_scroll.html
* His demo app: http://vallandingham.me/scroll_demo/
* His tutorial: http://vallandingham.me/scroller.html

Based on Jim's tutorial and talk, a Mike Freeman tutorial, but with a slightly modified code library:

* http://mfviz.com/scrollytelling/#/
* His code: https://github.com/mkfreeman/scrolling (I saved a copy as mfreeman_scroller.js in our js dir)

Truth: I spent a lot of time trying to adapt 2 graphs to these techniques in both the Bloomberg framework in graph-tools.io and Jim's.

The example for the homework is much simpler, a combo using Mike Freeman's modified version of Jim's scroller:

* A first simple pass: [scroller_template.html](scroller_template.html)
  * requires js/line_chart.js
  * js/scroller_settings.js
  * js/mfreeman_scroller.js
  * line.css
* But it's not good enough.  Here's some improved work: [scroller_template_lines2.html](scroller_template_lines2.html) -- with more page context around it.

TODO: Try to fix up lib used to handle backing up from different ending points; clarify step 0 and when to trigger it at start.  Generally document the start/end position issues.


### Examples of Scrollytelling

**Jim's list**:

* http://vallandingham.me/scroll_talk/examples/
* The Receession in 255 Charts: http://www.nytimes.com/interactive/2014/06/05/upshot/how-the-recession-reshaped-the-economy-in-255-charts.html
* Bloomberg What's Really Warming the World? http://www.bloomberg.com/graphics/2015-whats-warming-the-world/  (using the graph-scroll lib)

**Position-based scrolling** (as Mike Bostock calls it):

* Shark and Minnow: http://www.nytimes.com/newsgraphics/2013/10/27/south-china-sea/
* Ted Ligety: http://www.nytimes.com/newsgraphics/2014/sochi-olympics/giant-slalom.html

**Scrolling with steppers**:

* English vs. Chinese Colors: http://muyueh.com/greenhoney/
* http://www.nytimes.com/interactive/2014/03/31/science/motorcycle-helmet-laws.html
* The Making-of: https://source.opennews.org/en-US/articles/behind-scenes-fewer-helmets-more-deaths/

**Yet more scrolly goodness**:

* Let's Free Congress: http://letsfreecongress.org/,
  * And a post about the transitions: http://blog.tonyhschu.ca/post/49488608263/technical-write-up-scroll-linked-animations
* Battle of the Berrics, linked text too: http://www.georgelmurphy.com/berrics/
* http://www.bloomberg.com/graphics/2015-auto-sales/ - "Martini glass style" of storytelling
* CA is getting Fracked by Anna Flagg: http://www.facesoffracking.org/data-visualization/


### Zoomytelling, a subgenre?

* Jeter: http://www.nytimes.com/interactive/2014/09/14/sports/baseball/jeter-swings.html?_r=0
* Greenland: http://www.nytimes.com/interactive/2015/10/27/world/greenland-is-melting-away.html

* What is this... Active Satellites: http://qz.com/296941/interactive-graphic-every-active-satellite-orbiting-earth/

### Design Tip: Avoid Scolljacking

Read: http://bost.ocks.org/mike/scroll/

"Scrolljacking" is bad.

Contrast this MacPro page: http://www.apple.com/mac-pro/?afid=p238%7Csf9lg0Y3B-dc_mtid_1870765e38482_pcrid_91262087647_&cid=aos-us-kwg-mac-slid-
with the pencil examination in http://www.fiftythree.com/pencil.

In the latter, and in most of the good scrollytelling examples, the user can speed up and reverse to control their movement.  Motion is dependent on the mouse, they aren't hijacked and forced into someone else's pace.


### Other Related Scrolly Tools

graph-scroll.js from Bloomberg/Adam R Pearce:

* http://1wheel.github.io/graph-scroll/

Mobile Touch Slider

* http://www.idangero.us/swiper/#.Vjz8ia6rSRs

Storytelling With Maps Tool:

* http://cartodb.github.io/odyssey.js/
* http://www.pleens.com/
* http://v.isits.in/

Storytelling with Pageflow.io:

* http://pageflow.io/en

Example: http://pageflow.ericmakswitat.de/research


##Javascript Tips

### Switch Statement (and a Functional Alternative)

You'll see this in the Mike Freeman example and the homework based on his slides. See: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/switch.

````
switch (expression) {
  case value1:
    //Statements executed when the result of expression matches value1
    [break;]
  case value2:
    //Statements executed when the result of expression matches value2
    [break;]
  ...
  case valueN:
    //Statements executed when the result of expression matches valueN
    [break;]
  default:
    //Statements executed when none of the values match the value of the expression
    [break;]
}
````

However, notice that a lot of Javascript developers argue against switch statements in favor of using objects.

* https://javascriptweblog.wordpress.com/2010/03/08/caseagainstswitch/
* http://encosia.com/first-class-functions-as-an-alternative-to-javascripts-switch-statement/


### String Character Replacements

A useful string replace function -- replace spaces in a country name with underscore:

````
var country = country.replace(/\s/g, '_');
````

This comes in useful for creating id's on SVG elements for later reference in code.


##Homework

Readings:

* [Telling Stories with Data](http://vis.stanford.edu/files/2010-Narrative-InfoVis.pdf)
* Mike's piece: http://bost.ocks.org/mike/scroll/
* Read/skim in this order: http://vallandingham.me/think_you_can_scroll.html, http://mfviz.com/scrollytelling/#/


**Homework 1 (25pt), Scrollytelling**: Use the template in [scroller_template_lines2.html](scroller_template_lines2.html) and associated files to tell a short story about that line graph.  You can write your own functions to highlight, label, color, etc, anything you want.  If you prefer to try to put your own data and chart into it, if it will help with your project, go for it.  There should be at least 4 steps to it. Send as "Scrolling."

Note: If you prefer to use a stepper, you can construct a new page with buttons (like we did in the first few weeks) with highlights triggered by the buttons.  Again, do that only if you want to use it in your final project.

**Homeworkd 2 (35pt), 3 Charts**:

Make 3 D3 charts of different kinds that you would like to include in your final project, all on the same page.  You can use multiple data files (using queue).  They do not have to be interactive yet (you can avoid tooltips etc until later).  It will definitely save you time if you can reuse this code in your project, so make sure you are building towards your final design.  We will discuss the next level of interaction next week. Send as "3 Charts."

TODO: Code structuring for this earlier in semester.



