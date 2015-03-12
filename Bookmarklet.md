# The Google Code Wiki Editor Live-Preview Bookmarklet #
(Or GCWELPB, for short.)

Founder of this project, Fabien, created a bookmarklet which provides a real-time preview mode in the Google Code wiki editor.

It works on recent Firefox/Chrome versions. It is untested on others.

To install it:

First, copy the following text into your clipboard:


```
javascript:void(function(){var%20s=document.createElement("script");s.src="http://wikiwym.googlecode.com/svn/trunk/bookmarklet.js";document.getElementsByTagName("head")[0].appendChild(s);}())
```

(Sorry, but the GoCo wiki won't let me create a link to that construct.

<a href='javascript:void(function(){var%20s=document.createElement("script");s.src="http://wikiwym.googlecode.com/svn/trunk/bookmarklet.js";document.getElementsByTagName("head")[0].appendChild(s);}())' title='GoCoWiEditorPreview'>If you are using our parser to view this page, try copying this link to your clipboard</a> or dragging it to your bookmark bar. (If you are viewing this page in via Google Code then that link is elided, despite the docs which say it should work.)

Then:

  * Paste the URL as a bookmark on your bookmark toolbar. (Try drag/drop first - that may work for you.)
  * Visit a Google Code project where you have access to edit the wiki pages and open one of the pages in the editor.
  * Click the bookmarklet link.

That will modify the layout of the page to include a real-time preview of the wiki.

There will be slight differences from the official preview, since the preview is parsed with our parser, but the overall results should be close.