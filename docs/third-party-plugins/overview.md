# Third Party Plugins

As a general rule, it's almost always better to custom-code plugin functionality as opposed to installing a third-party plugin. A big reason for this is site security, but there are typically also pretty significant performance considerations (third party plugins generally try to be 'everything to everyone' and thus usually include tons of unneeded features/bloat). 

Third party plugins should be heavily vetted, and examined in terms of "internal ROI" -- for example, given that RFI forms are mission critical for us, and that those forms have a lot of moving parts between the front end and back end, and tons of edge cases across various browsers/etc, this is a case where it makes sense for us to use a reputable third-party plugin (gravity forms). Conversely, despite the fact that there are numerous 'event calendar' plugins available, the nature in which we use events on nu.edu makes it easier to just build it ourselves with a custom post type.

## Plugin update procedures

We have it set up so that plugins **cannot** be installed or updated via the wp-admin dashboard. This is to ensure that all plugin changes are tested in a local environment first, and then submitted as pull request via git.

?> *@TODO* revisit plugin update procedures below

When updating plugins there are a few main methods:
- Download from source.
- Update plugin via admin dashboard locally.
- Composer dependencies update.

### Download from source
Straight forward manual method of updating. Usually reserved for premium plugins like [Gravity Forms](https://www.gravityforms.com/).
- Download plugin from website.
- Install locally and test.
- Branch off `develop` using branch naming convention `plugins/{plugin-slug}`.
- Commit with message structure "Update {Plugin Name} plugin vX.X.X -> vX.X.X".
- When doing PR into `develop`, if possible, in the **Description** area include the Changelog or a link to the changelog.

### Update plugin via admin dashboard locally
The more traditional way of updating WP plugins.
- In the Plugins page for the site (or network page for MU installs), update one plugin per Pull Request.
- Branch off `develop` using branch naming convention `plugins/{plugin-slug}`.
- Commit with message structure "Update {Plugin Name} plugin vX.X.X -> vX.X.X".
- When doing PR into `develop`, if possible, in the **Description** area include the Changelog or a link to the changelog.

### Composer dependencies update
In the root of the project files there _should_ be a composer.json file with project dependencies.
These will include plugins and sometimes one or more of our own skeleton/parent themes.

The team utilizes [Dependabot](https://docs.github.com/en/github/administering-a-repository/about-github-dependabot) to help us manage dependencies. They are usually set up to check for WP plugin updates on a weekly basis on Wednesdays, but they should generally be focused on every other week (not an option for time in Dependabot config at time of this guide's publishing). Dependabot will create PRs which can be used to update the pugins that _should_ have the head set as `develop`.

- Switch to the appropriate branch created by Dependabot.
- While in the root folder of the project, run `rm -Rf vendor && composer clearcache && composer install`.
	- To save time, an alias can and should be created. Example: `alias gitcomposerupdate='rm -Rf vendor && composer clearcache && composer install';`.
- Review changes and confirm that the update works with the rest of the project's codebase.
- Make a commit to the branch with _only_ files from the intended plugin being updated.
	- Commit with message structure "Update {Plugin Name} plugin vX.X.X -> vX.X.X".
- Keep both the Dependabot "bump" commmit and your Update plugin commit (i.e. do not squash the commits).
- Manage PR per usual.
