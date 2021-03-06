# Program Updates

On NU.edu there are specific steps and details that anyone updating a program should be aware and attentive to.

## Adding a program
- In the WP admin create the program in both `www` and `info` domains.
	- Make sure it has a **Department**.
	- No hero is necessary since (at the time of publishing this guide) the template file does not include a hero type image.
	- The "Why NU?" and quote sections trickle down from College -> Department -> Program, so it's not absolutely necessary to define those sections.
	- The "Opportunity Scholarship" section is managed as a Widget in the admin with exclusion handled through the Widget Logic plugin.
- If the program belongs to the school **Workforce Education Solutions Training & Development** (WES T&D), previously known as Extended Learning, then please also **add** it to the field of program options in the form that is specific to WES T&D / EL.
- Update the [Google Sheet](https://docs.google.com/spreadsheets/d/1p6620uGHOfmMa74E8X6vRXxZCVzLto72sg2p_5ESDtU/edit?pli=1).

## Moving a program
If a program is being moved from one department to another, please be mindful of the following:
- SEO: There may be links out there or Google might take time to update it's links in the Google results pages so add a redirect when moving a program.
- Update any references to the previous College or Department.
- If the program is being added to the school **Workforce Education Solutions Training & Development** (WES T&D), previously known as Extended Learning, then please also **add** it to the field of program options in the form that is specific to WES T&D / EL.
- Update the [Google Sheet](https://docs.google.com/spreadsheets/d/1p6620uGHOfmMa74E8X6vRXxZCVzLto72sg2p_5ESDtU/edit?pli=1).

## Removing a program
- In the WP admin for www.nu.edu, set the program's status to "Draft".
- Add a redirect from the program to it's parent **Department** (SEO!).
- If the program belongs to the school **Workforce Education Solutions Training & Development** (WES T&D), previously known as Extended Learning, then please also remove it from the field of program options in the form that is specific to WES T&D / EL.
- Remove any references to the program by doing a search for the full name of the program, and any known abbreviations, in the admin search(s). "Known abbreviations" include MA {program name} and M.A. {program name} for Master of Arts, RN for Registered Nurse, MBA for Master of Business Administration, etc.
- Draft the program in the `info` subdomain as well.
- Update the [Google Sheet](https://docs.google.com/spreadsheets/d/1p6620uGHOfmMa74E8X6vRXxZCVzLto72sg2p_5ESDtU/edit?pli=1).


## Future helpful implementations
One plugin and feature that at one point was considered was/is [Distributor](https://distributorplugin.com/) by [10up](https://10up.com/). This would allow for syncing between the multisite installs (`www` and `info`) and things would only be updated in one main site, likely `www` as the parent and top domain.
If you would like to vet the plugin and implement it, or have other ideas, please discuss with the team.
