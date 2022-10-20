# Placeholder to Expand on in the Future

We have a handful of 3rd party plugins that it seems like we do not use anymore. At some point we should do a more in-depth audit of all of these and uninstall if possible.

## AMP

?> Plugin Site: https://amp-wp.org/

Currently installed & activated on `nu.edu`, deactivated on `info.nu.edu`

Settings accessed via WP-Admin >> AMP. Currently only enabled for content type 'Posts', which we only use for Press Releases. 

"AMP mode" enabled by appending `/amp/` to a page URL.
- Example:
	- Normal version: https://www.nu.edu/news/meb-keflezighi-to-deliver-keynote-address-at-national-university-commencement/
	- AMP version: https://www.nu.edu/news/meb-keflezighi-to-deliver-keynote-address-at-national-university-commencement/amp/


## Better Search Replace Pro

?> Plugin Site: https://bettersearchreplace.com/docs/

I don't think this is something we need anymore. Database search/replace can be handled via WP-CLI/WPVIP. It looks like this plugin was installed in 2018, possibly pre-dating WPVIP?

## Enable Media Replace

?> Plugin Site: https://wordpress.org/plugins/enable-media-replace/

Adds a "Replace media" upload option, when viewing an attachment from the WP media library. 

Useful for when we need to update PDF's that are manually linked within the content, across of lots of different pages.

[Example](https://www.nu.edu/ouruniversity/theuniversity/partnerships/smud/): Many partnership pages will include a "Degrees Offered Flyer" PDF link in the sidebar. Occasionally this flyer will get updated. Rather than auditing all our partnership pages and manually replacing the links, we can simply utilize this plugin.

## Export All URLs

Lets us export Title, URL, etc. of any post types on our site.

Currently deactivated on nu.edu. 

Was added to the site in December 2021, no idea if it's been used. Seems like it could be helpful for content migration to the new site.

## Post Type Switcher

Adds simple admin dropdown to switch post type.

Currently deactivated on nu.edu. Was added to the site in July 2021, no idea if it's been used or is still needed.

## Widget Logic

Adds 'display logic' field to all widgets, and displays additional settings at the footer of the WP Admin wigets page.

@TODO We're currently using this plugin on both `www` and `info` for a couple widgets, but I feel like there are better ways to accomplish this. Might be worth re-visiting how we use widgets, and if there are better ways we can incorpate these components into the site.

## Algolia Search Plugin

?> Plugin Info: https://wordpress.org/plugins/wp-search-with-algolia/

Integrates with Algolia (third party service) to provide enhanced search features.

Settings accessed via: WP Admin>>Algolia Search

See Also: [Third Party Services: Algolia](../third-party-services/algolia.md)

## Duplicate Post (Yoast)

?> Plugin Info: https://yoast.com/wordpress/plugins/duplicate-post/

Currently deactivated. Useful to have, can probably just activate on an as-needed basis.