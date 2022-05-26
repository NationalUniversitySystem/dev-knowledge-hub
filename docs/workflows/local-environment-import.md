# Local Environment Import

!> Important: *Most* of our live sites are setup as multisite installations. Even sites that don't actually have any subdomains are generally still installed as a multisite. This is often important to specify when setting up a local environment as there are some behind-the-scenes differences with how WordPress handles multisites. We don't want a situation where a new feature is developed locally, only to have it break when pushed live because of the multisite aspect.

----------------------------------------------------------------------

## WPVIP Local Dev Tool

WPVIP recommends setting up a local development environment with the VIP Local Development Environment feature built into VIP-CLI. This has the benefit of making it easy to create a local environment that is nearly identical to our live site. This environment is based on Docker, however only minimal knowledge of Docker is actually required.

Please see [WPVIP - Create a VIP Local Development Environment](https://docs.wpvip.com/how-tos/local-development/use-the-vip-local-development-environment/) for WPVIP's official documentation. This tool is under constant development by the WPVIP, so refer to that link for the most up-to-date info. That being said, WPVIP's documentation is also usually not very clear, so the below is a walkthrough example to be used in conjunction with the official documentation.

### Below steps will focus on setting up a local environment for fundraising-academy.org (nu-sip-org)

1) Check all prerequisites required in the WPVIP documentation. i.e. VIP-CLI, Docker Desktop, etc.

2) Clone our site's [Github repo](https://github.com/wpcomvip/nu-sip-org) to your local computer. Ideally to your desktop or somewhere that is easy to access.

3) Via command line, run `vip @1570.production dev-env create --slug=sip-org` to create your local dev environment.
	- This launches the VIP dev env setup wizard
	- `@1570.production` tells the tool we want to create a local environment that matches the **production** version of our nu-sip-org site (which is VIP app ID **1570**)
		- Running `vip app list` will give a list of all of our sites along with their VIP app ID #'s
	- `--slug=sip-org` tells the tool to give a certain name to your local environment. You can call this anything you want, but it's generally best to have it match with whatever we call it on WPVIP.
	- All of our sites use WordPress **v6.0** and PHP **v7.4** as of May 2022, but double check the live site you're cloning to make sure you're using the same versions.
	- Prompt to redirect to live site for media files -- **true** (this is recommended as it means you won't have to pull images locally)
	- Prompt for vip-go-mu-plugins -- **image** (this is code that WPVIP runs on the back-end of all sites)
	- Prompt for source site-code -- **local** and paste the full folder path to the repo you cloned in Step 2
	- Prompt for Enterprise Search -- **false** (I don't think we use this on any of our sites)
	- Prompt for phpMyAdmin -- **true** but it's up to you. I personally like having access to it, but if you have a different preferred method of interacting with the database then go for it.
	- Prompt for XDebug? -- ?? [this is a newer feature WPVIP recently added, not sure. @todo investigate]

4) Run `vip dev-env --slug=sip-org start` to launch the local environment you just created.
	- This may take few minutes to run, as it is spinning up a docker container, pulling down wordpress, pulling down the vip-mu-plugins, and setting up the environment. 
		- In the future you can run the command with the `-S` flag to skip rebuilding, for a somewhat faster load time.

5) We now need to import the database to our local environment. [Please see the full WPVIP tutorial on this here](https://docs.wpvip.com/how-tos/dev-env-add-content/).
	- Export the most recent database backup from WPVIP dashboard (or VaultPress). Note that for nu.edu it will probably take awhile to 'prepare' the file for download, as the database is very large.
	- The export file will be a .gzip and needs to be unzipped until you're able to access the .sql file(s)
		- If using VaultPress each table is exported as its own file and you need to concat them into a single file.
		- If using WPVIP dashboard, export is a single .sql file that will have a timestamped name. To make things easier in the CLI, rename to **sip-org-db.sql**
	- Open the .sql file and **delete** any existing data for the **'wp_users'** and **'wp_usermeta'** tables. 
		- The easy way to do this is to CTRL+F and search for your @nu.edu email. Assuming you have an account on the live site, this will bring you to the relevant sections in the .sql file. 
		- This is important because WPVIP's dev-env tool creates a special "vipgo" user account for our local dev environment, and we don't want to overwrite that.
![Faculty Import](../_images/sql-delete.png)
	- For sites with larger databases, can also delete the entire **'wp_gf_entry_meta'** and **'wp_gf_entry'** tables. We don't need these locally. For nu.edu the import process might actually time-out if you don't delete these tables first.
	- Run `vip dev-env --slug=sip-org import sql sip-org-db.sql --search-replace="https://fundraising-academy.org,http://sip-org.vipdev.lndo.site`
		- This imports our database, and changes our "live" URL to instead be our localhost URL.
	- Run `vip dev-env --slug=sip-org exec -- wp search-replace --url=www.fundraising-academy.org www.fundraising-academy.org sip-org.vipdev.lndo.site`
		- This step is needed for multisite installations. This takes the database we just imported, selects a specific sub-site, and then updates all instances of that URL to point at our localhost url. 
		- For multisites with additional subsites, repeat this step for each subsite (i.e. `--url=info.nu.edu info.nu.edu nu-edu.vipdev.lndo.site`)
	- Run `vip dev-env --slug=sip-org exec -- wp cache flush`
	- Alternatively, you can also import the database via phpmyadmin or another tool of your choice. Be sure to import to the database named 'wordpress'. Note that you will need to manually perform the search & replace functions above.

6) Visit your local URL admin: `sip-org.vipdev.lndo.site/wp-admin` (or whatever URL what generated when you ran step #4 above)
	- Login username `vipgo` password `password`

7) Run `vip dev-env --slug=sip-org exec -- wp super-admin add vipgo`
	- vipgo user is automatically a super-admin on single-site installs, but for multisite you need to manually add.
	- To verify this was successful, reload the wp-admin page. You should be able to see 'Plugins' on the menu, and the top admin bar under 'My Sites' should have a 'Network Admin' option.

8) Build theme assets
	- At this point, visiting your local site `http://sip-org.vipdev.lndo.site/` will show the correct content, but with severely broken styling. 
	- Navigate to `themes\sip` and run `npm install` and then `npm run gulp`
		- This will build our CSS & JS assets, which are in our `/themes/sip/assets/` folder. This folder is excluded from git, as we use CircleCI for our build process on the live sites.
		- This also launches its own 'development server' localhost process, but since we're running our environment via WPVIP/docker, we can close the process once the build is complete.
	- At this point, your local site should be *nearly* identical to the live site.
		- Certain images are going to be missing, and that's (probably) okay. During the `dev-env create` setup wizard, we had an option for `--media-redirect-domain`. This enables our local site to pull images from the live site, but it only works for images that are attached/loaded via wordpress (i.e. featured images, or anything loaded via wp_get_attachment, etc). Images that are hard-coded as HTML or manually set as background-image via CSS will usually not load locally. This could probably be fixed, but unless it is mission-critical for a specific dev task, it's probably not worth the effort. Note that you can still upload images to the local site via WP-Admin and they will be available to use as you would on the live site.

9) Certain custom plugins *might* require assets to be built
	- For sip-org used in above examples, not necessary.
	- For nu.edu, definitely the react-based plugin, probably some others too. For each plugin, navigate to the folder and run `npm install` and `npm run build`

10) At this point your local development environment is now officially up and running.
	- To stop your dev environment: `vip dev-env --slug=sip-org stop`
	- To restart your dev environment: `vip dev-env --slug=sip-org start`
	- To view all your available local dev environments: `vip dev-env list`
	- To view all vip dev env commands: `vip dev-env -h`

11) Add our [internal 'dev toolbox' plugin pack](https://github.com/NationalUniversitySystem/dev-toolbox) to your local site's repo, by cloning the repo into the /client-mu-plugins/ folder.
	- Follow steps included in the repo's readme.
	- These files should already be excluded from git via gitignore, but if they are not, then add them.
	- @TODO Some of these dev plugins are a bit outdated, or now rendered obsolete based on functionality we get elsewhere. Probably good idea to revisit these at some point. 
		- For example 'show-template' and 'footer-queries' are now included in our standard query monitor. Also 'vip-activate-qm' is now included in all WPVIP sites by default.
	- Included: Helper function to stop links from trying to force https on localhost
	- Included: Helper function to create `write_to_log()` function, which makes for easy PHP error logging similar to console.log() in javascript.

12) If you haven't already, install our [Code Standards Package](https://github.com/NationalUniversitySystem/nusa-code-standards) on your system.
	- This is important because, in addition to our own internal code standards, WPVIP enforces us to adhere to certain wordpress-specific standards.
	- After installing the packages from Github, install  the VSCode extension 'phpcs' -- this will enable VScode to show you errors/warnings in your code editor in real time.


**Additional Notes for WPVIP Local Dev Environment:**
- Wordpress Debug Log: can be found at C:\Users\\[user]\\.local\share\vip\dev-environment\sip-org\log (windows specific)
- wp-config.php can be found at: C:\Users\\[user]\\.local\share\vip\dev-environment\sip-org\config (windows specific)
	- Certain sites/plugins might require certain 'development constants' to be set here, i.e. `define( 'JETPACK_DEV_DEBUG', true );` 


--------------------------------------------------------------------------------

## VVV setup

> Old documentation below, might still work.

[WPVIP - Setup VVV for VIP Development](https://docs.wpvip.com/how-tos/local-development/set-up-vvv/)

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
