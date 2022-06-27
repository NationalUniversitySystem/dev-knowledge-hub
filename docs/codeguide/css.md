# CSS / SASS Codeguide

Misc notes from brand microsite development:
- Avoid excessive nesting as much as possible (i.e. don't use SASS for code organization. We can do that via comments & splitting into separate files)
	- Can create problems with specificity later on, i.e. force us to use !important when we shouldn't have to
- Try to rely on bootstrap for simple padding & margin, i.e. "pt-3", "mx-5", etc.
	- This lets us easily adjust for responsiveness ("pt-md-3", "mx-lg-5", etc), so we can cut down on having to write extra media queries for minor spacing/padding.
	- We have a customization to extend the numbering system of these utility classes. Instead of the standard bootstrap 1-5, we now have 1-26.
		- Source file: /src/scss/00_base/_bootstrap-overrides.scss
- Use specific properties when possible, i.e. `background-color:` instead of `background:`
	- Easier to adjust/override from other classes, less reliance on !important


## Syntax

- Use soft tabs with two spaces. (Should be set up in the project's `.editorconfig` file.)
- When grouping selectors, keep individual selectors to a single line.
- Include one space before the opening brace of declaration blocks for legibility.
- Place closing braces of declaration blocks on a new line.
- Include one space after `:` for each declaration.
- Each declaration should appear on its own line for more accurate error reporting.
- End all declarations with a semi-colon.
- Comma-separated property values should include a space after each comma (e.g., `box-shadow`).
- Include spaces after commas _within_ `rgb()`, `rgba()`, `hsl()`, `hsla()`, or `rect()` values, but do not include a space after the initial paranthesis nor before the closing parenthesis.
- Don't prefix property values or color parameters with a leading zero (e.g., `.5` instead of `0.5` and `-.5px` instead of `-0.5px`).
- Lowercase all hex values, e.g., `#fff`. Lowercase letters are much easier to discern when scanning a document as they tend to have more unique shapes.
- Use shorthand hex values where available, e.g., `#fff` instead of `#ffffff`.
- Quote attribute values in selectors with single quotes, e.g., `input[type='text']`. [They’re only optional in some cases](http://mathiasbynens.be/notes/unquoted-attribute-values#css), and it’s a good practice for consistency with our SASS guidelines.
- Avoid specifying units for zero values, e.g., `margin: 0;` instead of `margin: 0px;`.
- Use double colons `::` for [pseudo-elements](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements). This distinguishes pseudo-classes from pseudo-elements.

```css
/* Bad CSS */
.selector, .selector-secondary, .selector[type=text], .selector:before {
  padding:15px;
  margin:0px 0px 15px;
  background-color:rgba(0, 0, 0, 0.5);
  box-shadow:0px 1px 2px #CCC,inset 0 1px 0 #FFFFFF}

/* Good CSS */
.selector,
.selector-secondary,
.selector[type='text'],
.selector::before {
  background-color: rgba(0, 0, 0, .5);
  box-shadow: 0 1px 2px #ccc, inset 0 1px 0 #fff;
  margin-bottom: 15px;
  padding: 15px;
}
```

## Best Practices
## Gotchas
### Margin collapse
Avoid adding `margin-top` and `margin-bottom` on elements that are commonly found together (i.e. heading and paragraph tags). If a heading has `margin-bottom` and the paragraph has a `margin-top`, while trying to space things out the space would take the margin of the largest value.<br>
This is known as "margin collapse" and can lead to multiple values being overwritten, unnecessary code being added, spaghetti code, and overall bad practices.<br>
Adding both top and bottom margin to a paragraph tag also becomes redundant since they are commonly placed one after another.

## Linter
We utilize [stylelint](https://stylelint.io/). A few of our repos or themes have legacy code which uses [sass-lint](https://github.com/sasstools/sass-lint).
By all means, if you have the time go ahead and update those repos and themes.

### Linter rules
Dot files in our knowledge hub should include the `.stylelintrc.js` that should be used across all projects.
This file is a set of rules that are not necessarily set in stone. Team members should keep an open mind and understanding that the web itself, standards, and ideas all change and so if anyone has feedback, better implementation methods, etc for the linter then please do mention it or brainstorm on it with team members.
