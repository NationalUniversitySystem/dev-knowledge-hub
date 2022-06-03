# Program Updates

?> _TODO_ Below content is from prior dev documentation. We should revisit and update once the new program page templates are live on the new site.
On NU.edu there are specific steps and details that anyone updating a program should be aware and attentive to.

## Adding a New Program
!> **Important**: Program page URLs are custom generated based on college/department/degree. When creating a new program post, select an applicable 'Area of Study', 'Degree Type', and 'Academic Hook'. If Academic Hook is not visible on the content entry screen, populate the other two values and hit Publish/Update, and it should now be visible.

- In the WP admin create the program in both `www` and `info` domains.
	- Make sure it has a **Department**.
	- No hero is necessary since (at the time of publishing this guide) the template file does not include a hero type image.
	- The "Why NU?" and quote sections trickle down from College -> Department -> Program, so it's not absolutely necessary to define those sections.
	- The "Opportunity Scholarship" section is managed as a Widget in the admin with exclusion handled through the Widget Logic plugin.
- If the program belongs to the school **Workforce Education Solutions Training & Development** (WES T&D), previously known as Extended Learning, then please also **add** it to the field of program options in the form that is specific to WES T&D / EL.
- Update the [Google Sheet](https://docs.google.com/spreadsheets/d/1kE1lnYFgwN1gENHdYV_Tq75_zDeQ0LkRacOorCFs28g/edit#gid=0).

## Moving a program
If a program is being moved from one department to another, please be mindful of the following:
- SEO: There may be links out there or Google might take time to update it's links in the Google results pages so add a redirect when moving a program.
- Update any references to the previous College or Department.
- If the program is being added to the school **Workforce Education Solutions Training & Development** (WES T&D), previously known as Extended Learning, then please also **add** it to the field of program options in the form that is specific to WES T&D / EL.
- Update the [Google Sheet](https://docs.google.com/spreadsheets/d/1kE1lnYFgwN1gENHdYV_Tq75_zDeQ0LkRacOorCFs28g/edit#gid=0).

## Removing a program
- In the WP admin for www.nu.edu, set the program's status to "Draft".
- Add a redirect from the program to it's parent **Department** (SEO!).
- If the program belongs to the school **Workforce Education Solutions Training & Development** (WES T&D), previously known as Extended Learning, then please also remove it from the field of program options in the form that is specific to WES T&D / EL.
- Remove any references to the program by doing a search for the full name of the program, and any known abbreviations, in the admin search(s). "Known abbreviations" include MA {program name} and M.A. {program name} for Master of Arts, RN for Registered Nurse, MBA for Master of Business Administration, etc.
- Draft the program in the `info` subdomain as well.
- Update the [Google Sheet](https://docs.google.com/spreadsheets/d/1kE1lnYFgwN1gENHdYV_Tq75_zDeQ0LkRacOorCFs28g/edit#gid=0).

## WP Caching
- We use the [WP Object Cache](https://developer.wordpress.org/reference/functions/wp_cache_get/) to store & display Program data on Department pages ([example](https://www.nu.edu/ourprograms/collegeoflettersandsciences/mathematicsandnaturalsciences/)), in order to reduce unnecessary WP Queries and boost page speed.
- This means that after we remove a Program, we need to update the cache. Otherwise the Program will continue to be shown on Department pages.
- We have functionality built-in to the Programs CPT to auto-flush the cache whenever a Program is published/updated/removed. **However** if for some reason we still need to manually flush the cache, do the following steps:
	- Rather than flushing the cache for the entire site, we can delete the cache object for the specific Program we just removed:
		- via WP-CLI: `wp cache delete programs_list_[DEPARTMENT-ID]`
		- via VIP-CLI: `vip @1161.production -- wp cache delete programs_list_[DEPARTMENT-ID]`
		- `[DEPARTMENT-ID]` is the WordPress ID for the removed post's parent Department, can be found from WP Admin.
		- `@1161.production` specifies that we want to run the wp-cli command on the nu.edu production environment.
- References: [WP-CLI wp cache delete](https://developer.wordpress.org/cli/commands/cache/delete/) -- [VIP-CLI](https://docs.wpvip.com/technical-references/vip-cli/basic-usage/) -- [wp_cache_get()](https://developer.wordpress.org/reference/functions/wp_cache_get/) -- [NU.edu Programs cache usage](https://github.com/wpcomvip/nu-edu/blob/master/plugins/nuedu-core-functionality/inc/shortcodes/class-programs-list.php#L176)

## Future helpful implementations
One plugin and feature that at one point was considered was/is [Distributor](https://distributorplugin.com/) by [10up](https://10up.com/). This would allow for syncing between the multisite installs (`www` and `info`) and things would only be updated in one main site, likely `www` as the parent and top domain.
If you would like to vet the plugin and implement it, or have other ideas, please discuss with the team.
