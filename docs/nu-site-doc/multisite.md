# Multisite

Notes about our Multisite setup
- Certain things are handled differently by WP on multisite, vs. single-site
	- example: code (including SVGs) gets stripped out of content editor unless user is 'superadmin'. Can't override this via custom user permissions.
	- When consulting google for problem solving, keep in mind that those solutions are generally geared towards single-site installs. If a given solution isn't working, investigate whether multisite might be the cause.

Database structure is different under multisite setup.

WPVIP handles subdomains for subsites differently on production vs. test environments. i.e.: `info.nu.edu` -> `nu-edu-preprod.go-vip.co/info/`

Also need to keep in mind when running any WP-CLI commands, may need to specify the specific subsite URL you're targeting, with the `--url=[site]` flag