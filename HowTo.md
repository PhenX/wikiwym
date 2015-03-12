

# Adding wikiwym to a Web Page #

It's really, really easy....

First, include the JavaScript code in your HTML page:

```
<script type="text/javascript" src="http://wikiwym.googlecode.com/svn/branches/stable/lib/GoogleCodeWikiParser.js"></script>
```

If you want the wikified source code blocks then you need the pretty-printing code:

```
<script type="text/javascript" src="http://wikiwym.googlecode.com/svn/branches/stable/lib/prettify/prettify.js"></script>

<link type='text/css' href="http://wikiwym.googlecode.com/svn/branches/stable/lib/prettify/prettify.css"/>
```

Note the word `stable` in the paths shown above. If you want the _latest_ code, replace `branches/stable` with `trunk`. But since any commit in the trunk branch might be broken and might not get fixed quickly, we _strongly recommend_ that clients pull from the `stable` branch.

In your JavaScript it can then be used like this:

```
var p = new GoogleCodeWikiParser();
var html = p.parse("_*Hi, world*_");
```

That would produce this HTML:

> _**Hi, world**_

The output would normally be added to a DOM element. For example, if using jQuery we can replace the contents of a given DOM element with wikified content by doing something like this:

```
jQuery('#myContent', p.parse(...) );
```


If you are using the pretty-print code then you need to run the following _after adding the parsed content to your DOM_:

```
prettyPrint();
```

Every time new parsed content is added to the DOM, `prettyPrint()` must be called in order to process the results. If you do not do this then the code blocks will not get syntax-highlighted.

# Using wikiwym without a Browser #

The wikiwym parser is not dependent on a browser environment and thus can be used from arbitrary JavaScript engines which support loading external files, e.g. Mozilla Rhino or one of the shells based on Google v8. Usage is unchanged in non-browser environments, but how the script is loaded depends on the engine/shell being used.

# Customizing Link Generation #

If you need to customize how the parser generates links (e.g. so that you can add logic to make your app respond sensibly to intra-wiki links), you can override its `createLink()` member like this:

```
// Approach #1: globally replace the createLink() member:
GoogleCodeWikiParser.prototype.createLink = function(where,label) {
  // see the original implementation for how this
  // function should behave.
};

// Approach #2: replace createLink() for a single instance:
p.createLink = function(where,label) { ... }
```