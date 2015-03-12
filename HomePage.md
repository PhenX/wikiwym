# Introduction #

Wikiwym is wiki syntax parser, implemented in JavaScript, which tries to reasonably imitate the Google Code wiki format.

**Code status:** "It essentially works." See [SupportedWikiSyntax](SupportedWikiSyntax.md) for examples of what works and what doesn't.

**License:** MIT

**Primary Features:**

  * Fairly Small. The core parser lives in one file and has no external dependencies.
  * It is not based on regular expressions. For the most part it scans char-by-char, so it is more robust in handling things like nested markup (e.g. _**italicized bold**_) than regex-based implementations.
  * Can handle "most" Google Code wiki markup.  See [SupportedWikiSyntax](SupportedWikiSyntax.md) for what we believe works.
  * The main parser code has a one-class, one-function interface, so it's easy to use.
  * In some ways it's a better Google Code wiki parser than Google Code's wiki parser, as it can handle certain "strange, yet legal" linking constructs which GoCoWi doesn't natively handle.

**Primary Misfeatures:**

  * Certain wiki markup is not supported. See [SupportedWikiSyntax](SupportedWikiSyntax.md).
  * "Inline" markup (bold, italics, etc. i.e. all markup which is not for block-level items) is only processed within a single line. And i'm not 100% sure we have the same meaning of "end of line" as GoCo does.
  * There are not yet many configurable options. Use it as-is or hack it to suit.

# Getting and Installing #

  * Download the parser (a single file) from our source repo:
    * [stable branch](http://wikiwym.googlecode.com/svn/branches/stable/lib/GoogleCodeWikiParser.js)
    * [latest branch](http://wikiwym.googlecode.com/svn/trunk/lib/GoogleCodeWikiParser.js)
  * Include it in your HTML page.

You are of course free to "minimize" the source code using a minimizer of your choice, e.g. [Douglas Crockford's jsmin](http://www.crockford.com/javascript/jsmin.html). As of this writing (20100513), minimizing alone reduces the size by about 2/3rds. Compressing it using one of the common JS packers can reduce it by about 70-75%. Compressing it with gzip (or serving it from a server which supports such output compression), without minimizing/packing it first, provides only slightly smaller results than minimization, but can halve the size of a minified/packed copy. In my tests, the best reduction is obtained by combining minification and gzip (this is also more performant, as it requires no unpacking in the client JS engine).

The source tree [contains utility code for packing/minifying the parser](http://code.google.com/p/wikiwym/source/browse/#svn/trunk/pack).

# Ultra-mini HOWTO #

See also: [HowTo](HowTo.md)

The source tree has several files, in various stages of completion. The core parser code is in [GoogleWikiCodeParser.js](http://code.google.com/p/wikiwym/source/browse/trunk/lib/GoogleCodeWikiParser.js), and is used like this:

```
var g = new GoogleWikiCodeParser();
var html = g.parse( " ... wiki markup code ..." );
```

To see various live demos, visit out demo page:

  * http://fossil.wanderinghorse.net/demos/wikiwym/

From there you can preview any Google Code-hosted project's wiki pages using our online preview tool.

# Related Works #

  * http://remysharp.com/2008/04/01/wiki-to-html-using-javascript/, by Remy Sharp, supports a MediaWiki-like wiki syntax.