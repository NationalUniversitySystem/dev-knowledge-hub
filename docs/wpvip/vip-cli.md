# VIP CLI

WPVIP provides a command line tool you can use to interact with live and staging sites. This includes the ability to run most (but not all) standard WP-CLI commands as well.

Certain WP-CLI commands (`wp db`, possibly others) are disabled by default, we need to open a support ticket and they will run it for us. This is typically for more complex SQL-queries, and not a frequent occurance.

The history of all WP-CLI commands run on live & staging servers can be found via the WPVIP application dashboard.

-----------------------------------------------------

**WPVIP CLI** Reference: [https://docs.wpvip.com/technical-references/vip-cli/](https://docs.wpvip.com/technical-references/vip-cli/)

**WP-CLI** Reference: [https://developer.wordpress.org/cli/commands/](https://developer.wordpress.org/cli/commands/)

-----------------------------------------------------

## Commonly Used Commands

```vip @1161.preprod -- wp cache flush```

Flush the cache for the site


`vip @1161.preprod -- wp search-replace nu.pubs.curriqunet.com/Catalog/ nu.pubs.curriqunet.com/Preview/1/ --all-tables --dry-run`

Search & Replace in the database to provide sitewide updates. In this example, Curriqunet unexpectedly changed their URL structure. Rather than auditing all of our program pages to update external links to the course catalog, we were able to run this command to replace all database instances of `nu.pubs.curriqunet.com/Catalog/` with `nu.pubs.curriqunet.com/Preview/1/`

Note: always do a `--dry-run` first for wp search-replace commands to make sure they work as intended. If they do, remove the --dry-run flag to make the actual update.

`vip @1161.preprod -- wp transient get [modal_exclusions]`
`vip @1161.preprod -- wp transient delete [modal_exclusions]`

We sometimes use WP Transients as a way of caching certain content. Sometimes when developing/testing changes you'll need to manually delete the transient in order for it to re-set with your new changes.

-----------------------------------------------------

### NOTES TO COMMONLY USED COMMANDS

Note: `@1161` identifies our site. 1161 is our WPVIP 'app ID' for nu.edu. If needing to run commands on a different site, visit the WPVIP application dashboard to find the relevant app ID.

Note: `.preprod` identifies the environment we want to run the command on. **All examples above use preprod**, to prevent any errant copy/pastes, but replace this with `.production` to run on the live site. When running on production, WPVIP will typically ask a "are you sure you want to do this?" confirmation.

Note: For multisites, the command will run on all sub-sites unless a single URL is specified via an additional flag: `--url=info.nu.edu`, `--url=nu-edu-preprod.go-vip.co`, etc. Also sometimes need to include `--all-tables` flag