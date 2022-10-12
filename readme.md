# Form A Story Fork
This fork of [Codecademy's Form A Story project](https://www.codecademy.com/courses/learn-html/projects/form-a-story) is my work into extending it.

## Changes made
- [Added `pattern` attribute to `#verb-1`](#added-pattern-attribute-to-verb-1) to ensure that only a single word ending in ing can be entered into the text field
- Added `min="1"` attribute to `#num-1` to prevent 0 and negative numbers from being accepted in the numeric input field

### Added `pattern` attribute to `#verb-1`
The label attached to `#verb-1`'s textfield describes what to enter in it as a <span>Verb (ends in -ing)</span>.

#### Problem solving process
- Researched HTML's `pattern` attribute, which lead to learning about regular expressions in JavaScript (as `pattern` uses JS syntax)
- Found [RegExr](https://regexr.com/) to get a better handle on matches without having to constantly reload and fill in the form
- Developed [tests](https://regexr.com/6vpco) on RegExr to ensure that I had covered all possibilities while trying to put the regular expression together
	- Explored unicode property escapes even though I didn't end up using them

#### Explanation for `(?<![\s\S])(([a-z]{1,})(ing))(?![\s\S])`
`(?<![\s\S])`  
Negative lookbehind that will match any (non-)whitespace character. Any characters appearing before the first capture group will not validate.  

`(([a-z]{1,})(ing))`  
First capture group containing two capture groups. Works without this capture group, but the intent is better communicated using it:
- `([a-z]{1,})`  Second capture group. This capture group looks for a minumum of one lowercase a-z character, designed to prevent ing being entered in the field on its own.
- `(ing)`  Third capture group. Searches for the characters ing in order.  

`(?![\s\S])`  
Negative lookahead that will match any (non-)whitespace character. Any characters appearing after the first capture group will not validate.

#### Limitations
This particular solution will not work on Safari, as [lookbehind assertions are yet to be implemented in WebKit](https://bugs.webkit.org/show_bug.cgi?id=174931). As Safari makes up 22.24% of total browser use (46.62% in Australia), this solution could realistically only be used for internal websites where browser choice can be locked down.

I failed to consider [compound single-word verbs](https://www.thesaurus.com/e/grammar/compound-verbs/#four-types) using either hyphens and spaces.

## Next steps
- See if `#verb-1`'s regular expression can be rewritten without the negative lookbehind to maximise browser compatibility
	- Research alternative ways of implementing pattern matching on forms using JS
- Adjust `#verb-1`'s regular expression to account for compound single-word verbs
