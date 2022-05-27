# Accessibility (a11y)

## Educational Resources / Training
- [LinkedIn Learning - Accessibility for Web Design](https://www.linkedin.com/learning/accessibility-for-web-design/welcome?u=2168252)
  - Real world examples
  - Visual issues
  - Navigating with keyboard
  - Touch
  - Images/video
  - Forms
- [A360 Docs](https://hub.accessible360.com/kb/articles) (must be logged in)
- [a11y Project](https://www.a11yproject.com/)
- [Seven ways to test for accessibility of your web site with browser Developer Tools](https://christianheilmann.com/2021/01/11/seven-ways-to-test-for-accessibility-of-your-web-site-with-browser-developer-tools/)
- [WPVIP recommendations](wpvip/a11y.md)

---

## Tools

### Accessibility Testing Browser Plugins
- [Wave Plugin (Chrome and Firefox)](https://wave.webaim.org/extension/)
- [Lighthouse (Chrome)](https://developers.google.com/web/tools/lighthouse)
- [Siteimprove Accessibility Plugin (Chrome)](https://siteimprove.com/en-us/core-platform/integrations/browser-extensions/)

### VS Code Extensions
- [Web Accessibility](https://marketplace.visualstudio.com/items?itemName=MaxvanderSchee.web-accessibility)

### Screen Readers
- [NVDA](https://www.nvaccess.org/download/) - Free, PC Only
- [JAWS](https://support.freedomscientific.com/Downloads/JAWS) - Free, PC Only

---

## Common Issues
This is a guide of the most common accessibility issues and how to avoid them. Please note where specific site suggestions are mentioned, since those suggestions may only apply to specific sites.

### No `:focus` Indicator Visible
All focusable elements (anchors, buttons, inputs, etc) must have a distinct style applied when focused, differing from the `:hover` styles. This is extremely important for keyboard users, who rely on this visual indicator to navigate our sites.

In order to avoid our `:focus` styles being visible when an element is actually clicked/tapped, instead of `:focus`, use `:focus-visible` in your scss. This will only apply the focus styles when keyboard navigation has occurred.

#### An example `:focus-visible` style:

```css
:focus-visible {
    outline: 2px solid $color-brand-primary;
    outline-offset: 5px;
}
```

### Not Trapping Focus in Modals
When a user triggers a previously un-seen element to display, such as a modal, custom JavaScript is needed to "trap" the focus inside of the component.

For example, let's say we've clicked a "Read More" button that triggers a modal window to pop-up. The native `:focus` is currently still on that button we clicked, so when you `TAB` next, the `:focus` will jump to the next focusable element on the page, which is normally not the modal. This is where custom JavaScript comes in.

You'll need to manually set the focus inside the newly opened modal, and once it's there, do not let it `TAB` out of the modal until the user has explicitly pressed the close button or `ESC` key. Hence the term "Focus _Trapping_ - we trap the focus in a loop inside of the modal.

**Note:** Boostrap v4 modals do this natively *if the standard markup is used*.

### Nested Navigation Not Accessible via Keyboard
Most often, when implementing nested navigation, we show the child `<ul>` on `:hover` of the parent `<li>`/`<a>`. While this works fine for mouse users, this renders the hidden nested menus unreachable for keyboard users. Like the above issue, this requires a custom JavaScript implementation.

[Example nested menu keyboard navigation script](https://github.com/wpcomvip/nusystem-org/blob/master/themes/nusystem/src/js/theme/navigation/sub-menus.js)

### Using `tabindex`
Any use of `tabindex` is _highly_ discouraged, unless you have a very specific reason for doing so. By using `tabindex`, you destroy the native keyboard navigation of the site and open the door for confusion.

### Forms
All form fields _must_ have a corresponding `<label>`, with the appropriate attributes. Even if the `<label>` is not needed visually (not best practice), it should still exist, just with a class of `.sr-only` added.

#### Example:
```html
<label for="fname">First Name</label>
<input type="text" id="fname" name="fname">
```

### Hiding HTML Elements
Usually, to hide an element, we apply `display:none;`. Screen readers will ignore/skip anything with this rule, however there are many ways in which we may visually hide content, for example setting the `opacity:0`. In this instance, although it is visually hidden, a screen reader will pick this element up. In order to make the element invisible to screen readers as well, we need to add the `aria-hidden="true"` attribute to the element.

### Link Identified Only By Color
This issue occurs when color is the only distinguishing feature about links in blocks of text. Make sure there are other visual indicators of links besides the color, such as underline or bold

How to fix this issue specifically on...
- **National University (www)**:
  - Wrapping an anchor element within a `<p>` will add `text-decoration: underline` to the link.
  - For links within ordered `<ol>` or unordered `<ul>` lists, make sure to add `list list--reset list-gold` classes to the `<ul>/<ol>` tag.

### Generic Link Text
Oftentimes the copy is outside of our control, but try and push for more descriptive call to action copy when possible, as "Read More" does nothing for the user.

### Heading Not Nested Properly
The headings on the page must be hierarchically organized. Headings should also go in order and not skip levels, ie:

```html
    <h2>Heading 1</h2>
        <h3>Heading 1.1</h3>
        <h3>Heading 1.2</h3>
    <h2>Heading 2</h2>
        <h3>Heading 2.1</h3>
        <h3>Heading 2.2</h3>
            <h4>Heading 2.2.1</h4>
            <h4>Heading 2.2.2</h4>
    <h2>Heading 3</h2>
```

Tip for **National University (www)**: If you need to add custom styles to a heading element (`<h1>` - `<h6>`), use our utility classes: `heading--one`, `heading--two`, `heading--three`, `heading--four`, `heading--five`, `heading--bold`.

[How to Structure Headings for Web Accessibility](https://www.nomensa.com/blog/2017/how-structure-headings-web-accessibility)

### Image With No `alt` Attribute
The image does not have an `alt` attribute (`alt=""`). **It’s important all images have the attribute for alternative text regardless of whether an alternative text is added.**

If the image is part of a link, the `alt` text should include what action the link will induce.

#### Example:
```html
<a href="/apply-now" target="_blank">
  <img src="images/apply-image.png" alt="Visit the apply now page!">
</a>
```

### Images Containing Text
We should, under no circumstances use images that contain text, large or small. All text should be live, using a background-image if needed.

### Non-distinguishable Landmarks
The page contains two or more `HTML5` or `WAI-ARIA` landmarks of the same type that has not been named. Users might not know the difference if it's not somehow explained. Use the WAI-ARIA attributes `aria-label` or `aria-labelledby` to create unique names that describe the purpose of each landmark.

There are three ways to label a sectioning element:
- Method 1: Add an `aria-label` attribute
- Method 2: Add a `<h#>` element to it
- Method 3: Use an `aria-labelledby` attribute
[You need to label your sections. Here are three methods.](https://css-tricks.com/how-to-section-your-html/#you-need-to-label-your-sections-here-are-three-methods)
