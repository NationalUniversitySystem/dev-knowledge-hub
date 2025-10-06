# Team Guide: Writing Effective Instructions for GitHub Copilot (Agent Mode)

## 1. General Best Practices

* **Be specific:** Include details about WordPress APIs, functions, and coding standards.
* **Describe context:** Mention where the code lives (plugin, theme, block editor, template).
* **Define output:** Tell Copilot what the result should look like or do.
* **State constraints:** Libraries, CSS frameworks (e.g., Tailwind, Bootstrap), or coding conventions we follow.
* **Iterate:** Start broad, then refine with follow-up prompts.

---

## 2. Instruction Structure

When giving Copilot Agent Mode instructions, use this four-part format:

1. **Task** – What do you want to build/update?
2. **Context** – Where does this code live in our WordPress setup?
3. **Requirements** – Functional details (PHP, JavaScript, styling, WordPress APIs).
4. **Output format** – What you want Copilot to return (full code, just a function, explanation).

---

## 3. WordPress-Specific Scenarios

### A. Custom WordPress Block Builds

When building new blocks, include:

* **Registration:** Block name, namespace, attributes.
* **Editor UI:** Fields (`RichText`, `MediaUpload`, `InnerBlocks`, etc.).
* **Frontend:** How it renders in PHP (`render_callback`) or JSX.
* **Styling:** Which CSS system we use (Tailwind, SCSS, etc.).

#### Example Instruction

> Build a custom Gutenberg block named `nuedu/reviewed-by`. It should let the editor select a post author (dropdown of users with `role=author`). In the editor, show the selected author’s name and profile picture. On the frontend, render a styled author card with name, avatar, and link to their archive page. Use Tailwind for styling. Register with `block.json` and a `render_callback` in PHP.

---

### B. Custom Template Parts

When working with template parts:

* **Location:** `template-parts/content-*.php` or block-based theme parts.
* **Conditional logic:** e.g., show different markup for posts in “News” vs “Blog.”
* **Reusable structure:** Should work across archive, single, or custom pages.

#### Example Instruction

> Update the template part `template-parts/content-article.php`.
> If the post is in category "News", display the date above the title.
> If the post is in category "Blog", display the author byline under the title with a link to their archive.
> Keep markup semantic and responsive, using `<article>`, `<header>`, `<footer>`.
> Add BEM-style CSS class names for styling.

---

### C. Responsive Page Template Design

When designing responsive templates:

* **Layout method:** CSS Grid, Flexbox, or Tailwind.
* **Breakpoints:** Define tablet/mobile/desktop behaviors.
* **Content sources:** `WP_Query`, custom loops, or `get_template_part`.
* **Components:** Which template parts or blocks should appear.

#### Example Instruction

> Create a WordPress page template named `Earned Media Archive`.
> Layout: two-column grid on desktop, stacked on mobile.
>
> * Left column: sticky filter dropdown (categories + years via AJAX).
> * Right column: grid of post cards (3 per row desktop, 2 tablet, 1 mobile).
>   Include active filter chips under the page title.
>   Use Tailwind for responsive breakpoints.
>   At the bottom, include the reusable “Get in Touch” template part.

---

## 4. Tips for Better Results

* **Reference existing code:** Paste snippets so Copilot follows project conventions.
* **Specify reusability:** If code should work across multiple templates/blocks.
* **Ask for explanations:** Add “Explain decisions in comments” if you want rationale.
* **Refine iteratively:** If the first output is too generic, ask Copilot to refactor for our conventions.

---

## 5. What to Avoid

❌ “Make me a WordPress block.” (too vague)
❌ “Build a page template.” (missing layout/styling details)
❌ “Update this file.” (doesn’t tell Copilot how)

✅ **Instead:** Always specify *what*, *where*, *how*, and *why*.

---

## 6. Reusable Prompt Template (Copy-Paste)

Here’s a structured form you can reuse when instructing Copilot:

```
Task: [What do you want built or updated?]
Context: [Where does this code live? Theme file, block, plugin, template part?]
Requirements: [Layout, WordPress APIs, PHP/JS details, styling system, logic]
Output format: [Full code, function only, explanation, or step-by-step]
```
