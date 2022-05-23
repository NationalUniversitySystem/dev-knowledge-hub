?> _TODO_ This whole section copy/pasted from prior dev docs. May want to re-visit/update as needed.

# Fundamentals
General rules and best practices to follow.

## Golden Rule
> Every line of code should appear to be written by a single person, no matter the number of contributors.
>
> -- <cite>[Mark Otto](https://markdotto.com/)</cite>

## Mobile First Design/Coding
`min-width` only with media queries (max-with definitely seems like a dev started from desktop and is now adapting code for smaller screens).
Remember, start with the most basic version of your idea (code), then layer/add to it.

## Default Values
Do not include default values in your code for any language. Browsers and frameworks will fallback to the default values and properties.

Learn the default display values for HTML elements, CSS properties, WP_Query options, etc.

Some examples:
- The `target="_self"` for links attribute does not need to be defined.
- The `"post_type" => "post"` in a WP_Query build.
- The `display: inline;` for img elements in CSS.

## Tips to live/code by
- Try to do things correctly the first time. Ask yourself, when was the last time you went back and refactored a project's code?
- It's not necessary to be "clever" with your code. code should be optimized to be read by devs in the future, including yourself.
> “Programs are meant to be read by humans and only incidentally for computers to execute.”
> - Donald Knuth, The Art of Computer Programming.

## Comments
Code itself should be readable and comments should be used to explain _why_ something is being coded (function block comments), _why_ it is happening, or a helpful reminder or explanation for future self.
Use comments as informative, warnings (e.g. legacy code present), to-do, explain a block of code that explains some of the logic or flow.

Do **not** add comment for every line of code when it is clear what the code does. This will restate the obvious leading to the following scenario:
A dev new to the codebase (or even just file) will/should read every comment present to understand the code. If there is comments that just state what the code itself explains, that could lead to precious time being wasted.
