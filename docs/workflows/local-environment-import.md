# Local Environment Import

?> _TODO_ Below content is from prior dev documentation, may be outdated.

?> _TODO_ Add description for WPVIP's docker-based local dev environment tool

----------------------------------------------------------------------

- Set up local environment for WPVIP development.
  - [WPVIP's guide to setup local environment](https://docs.wpvip.com/how-tos/local-development/)
  - [Our team's code standards](https://github.com/NationalUniversitySystem/nusa-code-standards). "All code in any code-base should look like a single person typed it, no matter how many people contributed".

Here are some helpful steps and info to import a WPVIP site's database (DB) into a local environment so that devs can work with data that is as close as possible to the live environment.

- Download database(s) from [VaultPress](https://dashboard.vaultpress.com/).
	- If you need to download a WP network/multisite install, VaultPress stores backups divided into one per site (i.e. each subdomain is it's own backup).
	- Use the option to download the whole DB (all tables).
- Once downloaded, delete the `wp_users` table and Gravity Forms related tables, if present.
- Remove the **Jetpack** related rows from the `wp_options` table(s).
	- At the very least, `jetpack_options` row needs to be removed but it is heavily adviced to remove _all_ `jetpack` options and also all `vip` related ones.
- Combine all the tables into a single `.sql` file by running the following CLI command in the folder where all the files are.
	- If there was multiple sites (subdomains) downloaded, you will need one file per site. Recommendation is to name each file as the subdomain slug.
	- `cat *.sql > all_files.sql`
	- Tip: save the command as an `alias` for convenience and later use as `alias sqlall='cat *.sql > all_files.sql';`.
- Place the `all_files.sql` (or multisite names) file(s) itself into the root of your site (same level as the site's `wp-config.php` file).
- For importing the DB into your local environment there are a few methods:
	- **TablePlus** (or other DB management software)
		- While managing your local DB, find the **Import** option which will allow the use of a SQL dump file.
		- In [TablePlus](https://tableplus.com/) the option is under `File -> Import -> From SQL Dump...`
	- **Vagrant / VVV**
		- SSH into your vagrant server via `vagrant ssh`.
		- Navigate to the very top level of your VM: `cd ../..`.
		- CD into the site in question `cd srv/www/{site-setup-slug}/public_html`.
		- Use [WP-CLI](https://developer.wordpress.org/cli/commands/db/import/) to import the DB file `wp db import all_files.sql`. If there were multiple subdomains, this command will need to be used once per subdomain with the `--url` flag (e.g. `wp db import subdomain.sql --url=https://subdomain.nu.loc`).
		- Exit the VM/server `exit`.
- Using **WP-CLI**, Do a search and replace for the source environment URL.
	- This needs to be done while inside the Vagrant VM.
	- First a dry run to confirm there will be data replaced `wp search-replace old-site.com new-site.dev --dry-run`
	- Then run without the `--dry-run` flag.
	- If the import of a site that is part of a multisite installation, remember to use one of the following flags:
		- `--url=subdomain.url.tld` if the site being imported is _not_ the main top site (blog ID = 1).
		- `--network` if importing multiple sites and need to replace on all registered to `$wpdb`.
		- `--all-tables-with-prefix` flag for all the tables with the predefined prefix (usually `wp_`).
		- If all else fails, `--all-tables` for literally _all tables_ in the DB.
		- For more information, visit the [WP CLI docs](https://developer.wordpress.org/cli/commands/search-replace/).
- Some SQL queries and DB modifications need to be done on the local DB now.
	- Update the authors in _all_ your `wp_posts` tables (`wp_posts`, `wp_2_posts`, etc) `UPDATE wp_posts SET post_author = 1 WHERE post_author <> 1;`
	- If your local site setup is a multisite, the row where `meta_key` column is "site_admins" in the `wp_sitemeta` table will need to be updated to include your local username, or fully replaced. Use any online tool to unserialize the data (it is an array of user names), add your username or replace completely, and then serialize back to place in the corresponding `meta_value` column.
- Tip: At this point run `wp cache flush` while SSH'ed into the Vagrant VM and in the proper folder.
- Tip: VaultPress does not immediately provide a back up of the `uploads/` folder and therefore all media. To make things easier and not request a full backup of that folder from WPVIP, we use a custom option in **VVV** that will fetch the source environment's files if missing locally. Add the live URL to the vagrant custom option of your local setup and run `vagrant provision` command.
```yml
	custom:
	  live_url: https://production.com
```

Some of the above is taken from WPVIP's own guides:
- [WPVIP — Sites Content in Local Development](https://wpvip.com/documentation/vip-go/local-vip-go-development-environment/#using-the-sites-content-in-local-development).
- [WPVIP — Search & Replace (step 14 on page)](https://wpvip.com/documentation/vip-go/vip-go-local-setup-windows/).

Additional helpful links:
- [VVV — Setting Up HTTPS](https://varyingvagrantvagrants.org/docs/en-US/references/https/)
---

## Troubleshooting

### Fix ERR_TOO_MANY_REDIRECTS

<img src="https://kinsta.com/wp-content/uploads/2018/01/ERR_TOO_MANY_REDIRECTS-error-in-chrome.png" width="700" alt="Screenshot of Google Chrome browser displaying an error.">

1. Clear browser data (suggested time range: 24 hours).
1. Delete Cookies on that specific site where this issue is happening.
1. Flush DB cache:
	- `vagrant ssh`
	- Navigate to the very top level of your VM: `cd ../..`
	- Access the site where you are having the issue: `cd srv/www/{$site_slug}`
	- `wp cache flush`
1. Check HTTP to HTTPS Redirects on the following tables:
	- wp_options - `siteurl` & `home` (http should be included)
	- wp_site - domain (url without http)
	- wp_sitemeta - `siteurl` (http should be included)
1. Confirm local domain are correct on `wp_blogs` table.

Helpful links:
- [How to Fix ERR_TOO_MANY_REDIRECTS on Your WordPress Site](https://kinsta.com/blog/err_too_many_redirects/)
- [How to Fix err_too_many_redirects in WordPress](https://www.hostinger.com/tutorials/how-to-fix-err-too-many-redirects#1-Deleting-Browser-Data)

### Fix redirect to the production environment
An issue you might run into when importing a site from production (or any other environment) to your local, is the your local URL redirecting to the source environment URL. To fix this try the following in Google Chrome:
- Open a new tab (_not_ in incognito mode).
- Open the dev console before doing going to any URL.
- Under the **Network** tab, make sure the "disable cache" option is checked.
- Go to your local environment's admin URL `{local-url.loc/wp-admin/}`.
- If this does not redirect, log in.
- Navigate to the Settings -> Permalinks settings page.
- Save/update settings without actually changing anything.
