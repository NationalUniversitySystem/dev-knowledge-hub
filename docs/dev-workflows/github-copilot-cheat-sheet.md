# GitHub Copilot Agent Mode – WordPress Cheat Sheet

## 🧩 Best Practices

* **Be specific:** Include functions, APIs, and styling systems.
* **Provide context:** Specify whether it’s a theme, plugin, or block.
* **Define expected output:** Describe what you want Copilot to return or create.
* **State constraints:** Mention frameworks like Tailwind or conventions like BEM.
* **Iterate & refine:** Start general, then narrow down with follow-ups.

---

## 🧱 Prompt Structure

1. **Task** – What do you want built or updated?
2. **Context** – Where does this code live?
3. **Requirements** – PHP/JS logic, styling, WordPress APIs.
4. **Output** – Full code, function only, or explanation.

---

## 🧰 Example: Custom Block

> Build a Gutenberg block `nuedu/reviewed-by`.
>
> * Editor: Select an author (dropdown), show avatar + name.
> * Frontend: Styled author card linking to the author’s archive.
> * Use Tailwind for styling.
> * Register with `block.json` and a PHP `render_callback`.

---

## 🧩 Example: Template Part

> Update `template-parts/content-article.php`.
>
> * If category = **News** → show date above title.
> * If category = **Blog** → show author byline with archive link.
> * Use semantic HTML (`<article>`, `<header>`, `<footer>`).
> * Apply BEM-style CSS classes for styling.

---

## 🖥️ Example: Responsive Template

> Create a page template **“Earned Media Archive.”**
>
> * Layout: 2-column grid (desktop), stacked (mobile).
> * Left: Sticky filter dropdown (categories + years via AJAX).
> * Right: Post card grid (3 desktop, 2 tablet, 1 mobile).
> * Add active filter chips under the title.
> * Use Tailwind for styling.
> * Include reusable **“Get in Touch”** template part.

---

## 🚫 Avoid

* “Make me a block.” (too vague)
* “Build a template.” (missing layout/styling details)
* “Update this file.” (no clear direction)

✅ **Always include what, where, how, and why.**

---

## 🧾 Prompt Template

```
Task: [What to build or update]
Context: [Theme, block, plugin, or template part]
Requirements: [Layout, APIs, PHP/JS logic, styling system]
Output format: [Full code, function, explanation]
```
