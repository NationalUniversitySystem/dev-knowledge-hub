# Code-specific Best Practices/etc

## General
It's not necessary to be "clever" with your code. Keep in mind that other devs (and/or your future self) may in the future need to revisit/troubleshoot your code, always try to make it as easy to understand as possible. Add comments if something isn't clear! You don't need to narrate every single line of code, but at the very least try to provide a "30-second overview" so anyone looking at the code for the first time has some context as to what's happening.

## HTML
**Reducing Markup**
Whenever possible, avoid superfluous parent elements when writing HTML. Many times this requires iteration and refactoring, but produces less HTML.

```html
<!-- Not so great -->
<span class="avatar">
	<img src="...">
</span>

<!-- Better -->
<img class="avatar" src="...">
```

## CSS/SASS
**Misc notes from brand microsite development:**
- Avoid excessive nesting as much as possible (i.e. don't use SASS for code organization. We can do that via comments & splitting into separate files)
	- Can create problems with specificity later on, i.e. force us to use !important when we shouldn't have to
- Try to rely on bootstrap for simple padding & margin, i.e. "pt-3", "mx-5", etc.
	- This lets us easily adjust for responsiveness ("pt-md-3", "mx-lg-5", etc), so we can cut down on having to write extra media queries for minor spacing/padding.
	- We have a customization to extend the numbering system of these utility classes. Instead of the standard bootstrap 1-5, we now have 1-26.
		- Source file: /src/scss/00_base/_bootstrap-overrides.scss
- Use specific properties when possible, i.e. `background-color:` instead of `background:`
	- Easier to adjust/override from other classes, less reliance on !important

**Linter** Many of our repos previously used [stylelint](https://stylelint.io/) or [sass-lint](https://github.com/sasstools/sass-lint). I don't think these were kept up to date and are probably disabled in lots of cases. At some point we should look into re-implementing them in order to ensure consistent code standards across the team. This will include re-examining and/or updating our .stylelint dot-files.

## PHP & Wordpress
All of our PHP is written in object-oriented format. https://wpengine.com/wp-content/uploads/2017/02/WP-EBK-LT-UltimateGuideToPhp-FINAL.pdf

As much as possible, all features should utilize wordpress hooks (actions & filters), and all front-end code (CSS & JS) should be loaded via wp_enqueue
