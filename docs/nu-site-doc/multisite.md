# Multisite

Notes about our Multisite setup
- Certain things are handled differently by WP on multisite, vs. single-site
	- example: code (including SVGs) gets stripped out of content editor unless user is 'superadmin'. Can't override this via custom user permissions.
	- When consulting google for problem solving, keep in mind that those solutions are generally geared towards single-site installs. If a given solution isn't working, investigate whether multisite might be the cause.

Database structure is different under multisite setup.

WPVIP handles subdomains for subsites differently on production vs. test environments. i.e.: `info.nu.edu` -> `nu-edu-preprod.go-vip.co/info/`

Also need to keep in mind when running any WP-CLI commands, may need to specify the specific subsite URL you're targeting, with the `--url=[site]` flag

### Superadmin Access
Our current internal approach is to grant full superadmin account privileges to everyone on the dev team as well as TBF. We understand that it’s generally considered "bad practice" to have lots of people granted superadmin privileges, but in evaluating our current situation it is the best approach for us. We have previously investigated other solutions, including creating a custom user role, however we determined it is not worth the time/effort it would require to come up with a viable solution.

Wordpress treats admin capabilities a little differently on multisite installs, which is what we use. The biggest issue that we encountered is how wordpress will strip out any code-related tags (svgs, javascript, custom css) from the content editor for non-superadmins. Normally we could just add the extra 'user capability' to solve this, but WP doesn’t allow that on multisite for security reasons. We’re using multisite a bit differently than the standard use-case, so those security concerns don’t apply to us.

In addition to stripping out code-tags, non-admins under multisite are also prevented from accesing the 'tools' menu (where our URL redirect tool lives), and the 'widgets/customizer' menu as well. There are probably other areas/problems too.

The main argument **against** granting widespread superadmin access would be around managing plugins and wordpress version updates, however we already have safeguards built in regarding these. For plugins, we currently have it set up so that installations/updates can only be performed locally and then pushed live via git. For wordpress version updates, those are handled exclusively by WPVIP and we do not have access to that via wp-admin.

In short, as long as the wp-admin is being accessed solely by our own internal team (and TBF), we believe the best approach is to grant superadmin access by default.