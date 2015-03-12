# TODOs #

The more notable TODOs, in no particular order:

  * Certain corner cases (or odd usages) of the inline markups do not match GC's interpretations.
  * Our interpretation of "end of line" is stricter than Google's - we should collapse adjacent, non-block-markup lines which are separated only by a newline, to allow inline markup to be more compatible with GC.
  * Refactor the parser to generate an object tree. This could then be used to generate formats other than HTML.
  * Add a way to make the parser aware of other page names within the project, so that it knows which WikiWords to auto-link.
  * `<wiki:comment>` (http://code.google.com/p/support/wiki/WikiSyntax#Comments). Very low priority.

# Non-TODOs #

Things which i don't imagine ever implementing...

  * `<wiki:gadget>`. My cursory reading about them implies that they only work via certain Google services, or otherwise require additional Google-specific support.
  * `#sidebar PageName`. That would require that the parser know about the page `PageName` (and how to fetch its contents). The sidebar also introduces a whole new level of layout element surrounding the output, and adding sensible click behaviours to the links requires browsers support.

When considering features, keep in mind that the main parser uses only core JS-language features so that it can work in non-browser environments. (Yes, some of us _do_ use JavaScript [for things other than browsers](http://code.google.com/p/v8-juice/)!)