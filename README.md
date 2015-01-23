## Status

Still Alpha.  But most parts now stable.  Should be beta in a week or two.

Until we go beta, we're not taking patches or feature requests.

# re-com

A library of ClojureScript UI components. 

Built on top of Dan Holmsand's terrific [Reagent](http://holmsand.github.io/reagent) 
which, in turn, is built on Facebook's brilliant [React](http://facebook.github.io/react). 

Re-com contains:
* familiar UI widgetry such as dropdowns, date pickers, popovers, tabs, etc.  (in Reagent terms these are `components`)
* layout `components` which organise widgets verticaly and horizontaly, within splitters, etc. `components` which put borders around their children. Plus these can all nest, etc.

In short, the sort of stuff you'd need to build a desktop-class app. Some components are still missing, so it is still a work in progress. 

The layouts and components work harmoniously together (umm, except for occasional bouts of English-soccer-hooligan-like hostility, but that's a bug right?).

## Are You Sure You Want To Be Here?

We're a bit new to HTML5, javascipt, ClojureScript, and FRP.   We're disgruntled refuges from Flash/Flex and before that places like QT, MFC, Smalltalk and Interviews. Without Guru status in modern browser technologies, should you be trusting us?

Having the substrate of React and Reagent bestows great benefits, for sure, but it has also posed us some serious challenges. For example, most javascript libs achieve 
popovers by adding absolutely positioned `<div>s` directly to the `<body>` element. But we couldn't do that - not if 
we wanted to abide by the ClojureScript, React/Reagent FRP-ish, immutable, dataflow rules.  We had to find other solutions. But there could be better ways. We're all ears.

We've done our best and 
it does seem to hang together fairly nicely, with only minor quirks. We're using it to build systems, and we've shaken out many bugs, but it is still early days, so you well  might find some hidden dragons.  

Despite all of the above, we intend to  talk with great authority and certainty, and hold strong opinions.

## No really, This Probably Isn't For You

We made this library to build desktop-class apps which will run in chrome environments like 
[node-webkit](https://github.com/rogerwang/node-webkit) 
and [atom-shell](https://github.com/atom/atom-shell). So we have not taken testing further than chrome. 

In theory, re-com should work on any modern browser, but there'd probably be teething issues like correct vendor-prefixing the CSS etc.

The layout side of this library and some components (visual widgets) rely on [Flexbox](http://css-tricks.com/snippets/css/a-guide-to-flexbox/) 
which [only works on modern browsers](http://caniuse.com/#feat=flexbox): Chrome, Firefox or IE11.

So for the next, say, year or so, this library would be a poor fit if you're targeting the retail web, which is rife with flexbox-less wastelands like IE10 and IE9. 
 
I can also confirm that none of the components have been designed with mobile in mind, and that there's been no attempt to handle media queries.  Its just not that kind of widget library.

Still here?

## So, Without Ado Being Any Furthered ...

Start your review with [the demo](). Wait! You are using Chrome right? 

The demo serves as: 
  - a way to visually showcase the components (widgets)
  - a demonstration of how to code using those components
  - a means to document the components (parameters etc)
  - a test harness of sorts

## Named Parameters

When you first start looking into re-com, you'll quickly notice that every component has `named parameters` (as apposed to `positional parameters`). Internally, not so much, but at the API boundary, definitely. 

So, when using re-com components, you will *not* we asked to use positional parameters like this:
```
[greet-component 2 "hello"]
```

Instead, re-com requires `named parameters` more like this:
```
[greet-component
   :times 2
   :say   "hello"]
```

Notice that the each parameter value has a short leading keyword name. 

While more verbose, we believe using `named parameters` in the API of a library has compelling benifits: 
	1. the code using the library is clearly easier to read
	2. as a result the code is more understandable - is there anything more important?
	2. optionality  -  not all parameters have to be supplied, defaults can be introduced
	3. flexibility - new parameters are easily added

## Running/Debugging the Demo and Tests

The demo app is provided to assist understanding of how to use the components. Look in the `re_demo` folder for the code.

To run the demo, clone this repository then from it's root, enter the commmand:

```
lein run
```

This will do a clean compile of the demo and load the required URL into your default browser (starting it if necessary).

You can also debug the demo with the following: 


```
lein debug
```

This will do a clean compile of the demo, load the required URL into your default browser and use [figwheel](https://github.com/bhauman/lein-figwheel) for debugging, which also starts a ClojureScript browser REPL. Sweet!

NOTE: Because the figwheel step is an infinite loop and it starts the server required to display the demo, the demo page will not show when initially launched. Simply refresh the page once the compile has finished.

You can run the tests with this commmand:

```
lein run-test
```

This will do a clean compile of the tests and load the required URL into your default browser.

You can also debug the tests with the following: 


```
lein debug-test
```

Unlike the demo, the tests are debugged using the more traditional cljsbuild.

## Using It In Your Apps

To use re-com in your application, you'll need to add this to your dependencies in project.clj:

```clj
:dependencies [
  [org.clojure/clojurescript "0.0-XXXX"]
  ...
  [reagent "0.5.0"]
  [re-com "0.X.2"]
]
```


You also need to include react.js itself. One way to do this is to add

    :preamble ["reagent/react.js"]

to the *:compiler* section of project.clj, as shown in the examples
directory (or "reagent/react.min.js" in production). You could also
add

```html
    <script src="http://fb.me/react-0.9.0.js"></script>
```

directly to your html.

XXX What else?  Bootstrap??

## Dependencies

These components make use of the following libraries:

 * [Bootstrap](http://getbootstrap.com) is a CSS/JavaScript library, but we're just using it for the CSS styling.
 *  is a ClojureScript wrapper for the [Facebook React](http://facebook.github.io/react) 
   library which is used to build web-based user interfaces.

## Leaky Abstractions

Layout is built on flexbox, but our abstractions are leaky.  At some point 
you're going to have to do the flexbox tutorials to understand what's going on. 

This is compounded by the viral nature of flexbox. It's reach tends to spread.  

## The Missing Widgets

* tree  (not hard but haven't needed one yet)
* a grid. HTML is good at small grids, so no problem there. But when the number of 
rows gets huge, you need a widget that does virtual rows. Otherwise there's just too many DOM nodes 
* drag and drop
* annimations / transitions.  We have ideas.  They seem clunky.
* Focus management - When the user presses tab, to which field does focus move. Just using the 
* A testing story. 



## The Intended Architecture 


## One Of These Days 

Eventually:

* Use GSS for layout. Instead of flexbox.  Performance problems apparently. 

## Component Suggestions

* Add a timed alert box which appears for a set period of time. This would probably be absolutely positioned over the UI and then fade away after the set time expires.


## RFP background



https://gist.github.com/staltz/868e7e9bc2a7b8c1f754/
http://elm-lang.org/learn/What-is-FRP.elm

Javelin:
Watch:     http://www.infoq.com/presentations/ClojureScript-Javelin
Read:        https://github.com/tailrecursion/javelin


https://www.youtube.com/watch?v=i__969noyAM
https://speakerdeck.com/fisherwebdev/flux-react

