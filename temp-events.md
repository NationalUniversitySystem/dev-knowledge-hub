
## Event CPT Overhaul/Revamp

Most of our event-related code is 2+ years old, and seems to contain waaay more features/functionality than what we're currently using. At some point we should go through and discover/map out/document everything that's in here. This can be an ongoing project.

Back-end: /plugins/nuedu-core-functionality/post-types/event/
Front-end (calendar): /themes/national-university-hotb/archive-event.php [live URL: nu.edu/calendar]
Front-end (single): /themes/national-university-hotb/single-event.php


### General/Guiding Questions
- What functions/features are built in to the CPT?
	- At first glance, looks like a lot of functionality for "in-person" events/physical locations
		- For example, looks like functionality to generate a google maps view based on a tagged latitude/longitude for the event

- class-schema.php
	- This file was last updated 2 years ago. What does it do? Is it still working? Is it still necessary? If so, can we improve/modernize it?

- class-metadata.php -> function save_default_form_leadin()
	- ...what is this? Do we still need it? What's a form leadin?

**Don't feel the need to go through every single function or understand every single line of code.**

**Documentation doesn't need to be super in-depth or technical. Aim for 'easy summary' that gives an overview**




- Better front-end
	- Templates + Archive/Calendar page + Sorting
	- "Read More" button only for Webinars category? Can we expand that to all? Or conditionally check if there's "more" to read?