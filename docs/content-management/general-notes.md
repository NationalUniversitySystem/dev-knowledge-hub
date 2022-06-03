# General Notes - Content Management



- Alt text for ALL images (accessibility). For hero images that feature NU students/alumni, we should include the student's name & graduation year.
- For internal links, can only link the folder path, i.e. `<a href="/admissions/">` rather than `<a href="https://nu.edu/admissions/">`
	- One benefit of this is that it's easier to replicate across preprod/dev/prod
	- Always include a trailing slash in URLs, gives us one less redirect
	- When pushing content from preprod to production, always double check ALL internal hyperlinks to make sure that nothing on production links back to our preprod site. Check all image paths for the same thing.

- Preprod/prod workflow
	- Ideally preprod & prod should be identical, but over time the content tends to diverge. Somewhat inevitable but we should still do our best to keep them in sync.
	- Current best practice for accomplishing this is to manually re-create posts/changes across both environments. This is labor intensive, but as of right now there's not really a better solution.
		- Plenty of plugins exist that let you sync content across different wordpress sites/environments, **however** these generally deal with syncing 'content' as a whole (i.e. the entire wp database), as opposed to pushing/pulling single posts on an individual basis. Because of how wordpress stores content in the database, this is much harder to accomplish and generally carries a pretty big risk of 'breaking things' or corrupting the database.
		- One potential solution we vetted in the past is [Distributor by 10up](https://distributorplugin.com/), however according to their documentation it typically struggles with handling post meta entered via third-party custom field managers, which is something we make heavy use of. **@TODO** it looks like that plugin has been under constant development over the past year, might be worth re-visiting and re-vetting at some point.


- Wordpress-specific quirks
	- Code disappearing (SVG issue), superadmin user account
	- How to revert to a prior revision (but note that metadata isn't shown in revision history slider)
	- Sometimes content is housed in the **Appearance->Customizer** menu. Although this generally isn't considered best practice, it was a much more common approach to wordpress development in the past, and some of our sites (Harmony, I think?) still make heavy usage of it.
	- Sometimes content is housed in the **Appearance->Widgets** menu. Ideally this should be limited to content that is 're-used' across many different pages, however some sites (info.nu.edu) makes heavy usage of it for individual pages.