# General Notes - Content Management



- Alt text for all images (student name, if applicable)
- For internal links, can only link the folder path, i.e. `<a href="/admissions">` rather than `<a href="https://nu.edu/admissions/">`
	- One benefit of this is that it's easier to replicate across preprod/dev/prod
- Preprod/prod workflow
	- Ideally preprod & prod should be identical, but over time the content tends to diverge. Somewhat inevitable but we should still do our best to keep them in sync.
- Wordpress-specific quirks
	- Code disappearing (SVG issue)
	- How to revert to a prior revision (but note that metadata isn't shown in revision history slider)