**Table of Contents:**



The TOC is generated from all header entries by adding the `<wiki:toc/>` tag, which optionally takes a `max_depth=N` parameter, where `N` is the maximum header depth to include in the TOC.

# Introduction #

This page demonstrates the various wiki markup which is working (or believed to be working) in the [current parser code](http://code.google.com/p/wikiwym/source/browse/trunk/lib/GoogleCodeWikiParser.js). If you view this page using [our wiki previewer application](http://fossil.wanderinghorse.net/demos/wikiwym/GoCoWi-previewer.html), the content should look more or less just like it does when rendered via the Google Code wiki site.

The goal is not to achieve 100% compatibility with GoCo, but to have a tool which can be used to provide a reasonably accurate preview of a GoCo-formatted page before committing it to a GoCo-hosted project's source code repository. It "could" be used as the basis of a standalone wiki implementation, but that's not the goal.

A good way to get a feel for what this code can and cannot do is to browse your own wiki pages with it:

  * http://fossil.wanderinghorse.net/demos/wikiwym/

From there you can browse the wiki pages from any Google Code project which has wiki pages in its Subversion repository, and they will be rendered by this code. You can also use it as an editor, including a preview, and then copy/paste the changes back into Google Code when you're happy with them.

Or you can see a custom full-fledged wiki site which uses this parser as its main renderer:

  * http://whiki.wanderinghorse.net/

# Inlined Markup #

"Inlined" markup is stuff like **bold** and _emphasis_, which appear on elements spanning only across a single line.

## Basic Markup ##

All of the basic inline markup is supported, as demonstrated throughout this page.

## Wiki-style Links ##

Wiki-words are _not_ linked by default - only those in `[ThisSyntax]` or `[ThisSyntax label string]` are handled. e.g. [HomePage](HomePage.md) gets linked but HomePage does not. Remote URLs are also handled only if they are bracketed (e.g. http://code.google.com/p/v8-juice).

The exception to this rule is arbitrary wiki-words with a `!` prefix, e.g. `!``JavaScript`. In that case, the `!` is elided, as it is in GoCo.

## Image Links ##

Without a link:
`[http://s11n.net/img/logo/logo.lightblue.jpg]`

![http://s11n.net/img/logo/logo.lightblue.jpg](http://s11n.net/img/logo/logo.lightblue.jpg)

With a link:
`[http://s11n.net http://s11n.net/img/logo/logo.lightblue.jpg]`

[![](http://s11n.net/img/logo/logo.lightblue.jpg)](http://s11n.net)


## Table of Contents ##

Add a tag which looks like this to your page to have it generate a table of contents from all headers:

```
<wiki:toc max_depth="4"></wiki:toc>
```

The `max_depth` value specifies the header levels which should be included in the !ToC. e.g. set it to 1 to include only `H1` headers and 2 to also include `H2` headers.

# Block-level Markup #

## Source code blocks ##

```
if( (i < 10) && (i > 1) ) {
    print("hi, world!");
}
```

Source code highlighting requires third-party support. This parser does not colorize
code blocks by itself. It is normally fairly easy to add this to the generated HTML output. See [this article](http://angrycoding.blogspot.com/2011/04/recreating-google-code-wiki-with.html) for a tutorial describing how to do so.

## Block Quotes ##

Someone once said:

> This sentence will be quoted in the future as the canonical example
> of a quote that is so important that it should be visually separate
> from the rest of the text in which it appears.

## Lists ##

As of [r140](https://code.google.com/p/wikiwym/source/detail?r=140), nested lists are supported.

  * Item is _emphasized_.
    * Item is **bold**.
    * Item is **_emphasized bold_**.
  * Item is `backticked`.

  1. Item is ~~stricken~~.
    1. Item is <sub>subscripted</sub>.
    1. Item is <sup>superscripted</sup>.
      * Item is ~~**stricken boldly**~~.
      1. Item is **~~boldly stricken~~** (and is different list type than its neighbors).
      * Item is _**~~boldly stricken with emphasis~~**_.
  1. Do `<backticks block parsing of <`? (works as of [r35](https://code.google.com/p/wikiwym/source/detail?r=35))
  1. Can we **`bold backticked data`**? Of course. But not if we do `*asterisk inside the backticks*`.


## Tables ##

| cell 0,0 | <sub>cell 1,0</sub> | <sup>cell 2,0</sup> |
|:---------|:--------------------|:--------------------|
| ~~**cell 0,1**~~ | ~~cell 1,1~~ | _cell 2,1_ |
| <sup>*cell 0,2*</sup> (LOL! GoCo doesn't handle superscripted bold, but our parser does) | cell 1,2 | **cell 2,2** |

## Horizontal Lines ##

The HR element is represented by `----` on a line by its own:

---



# Blatantly Missing Features #

  * Gadgets and other features which require Google or browser-level infrastructure (since the parser is not tied to browser environments).