# General tips and help

Recommended to scheduling some of these, but might _require_ later (set up calendar recurring events or Slack reminders for yourself).

Tools and habits developed over the years.

## Coding
- Always, always, and always understand what something does before changing it and committing it to a codebase. That being said, it's ok to not understand a piece of code sometimes, that's why "legacy" code exists. BUT if you're going to change it, fully understand what it does and what other parts of the codebase it affects (i.e. run a search in the project folder for `function function_name(` to easily find a function definition).
- Load projects one at a time from their root folder, not the folder you are working on. This has the following benefits:
	- This will allow the code editor to follow the appropriate `.editorconfig` rules (especially if you have auto format on save enabled).
	- Git extensions will highlight files and code changes appropriately.
	- Code editor will respect the correct hierarchy of dot files (e.g. `.editorconfig`, `.stylelint`, `.eslintrc`, etc).
	- PHPCS will load the right rules per project if it needs to (VIP level or not).
	- Settings can be controlled on a "workspace"/project level in your code editor.
	- Whole projects can be opened easily if you save your "workspace".
- Update code standards at least once a month, no more than every other week.
	- All your cloned code standards should live in the same grouped folder like your user folder, documents, or with other code projects (outside of your local vagrant environment though please).
	- Do a `git pull` for each code standards folder/repo (there should be at least 3; ours, WP, WPVIP)
	- Might need to run the `phpcs` command to refresh the global code standards installed. For tips on how to do that refer to the team's [code standards repo](https://github.com/NationalUniversitySystem/nusa-code-standards#tips-and-recommendations).

## Git
- Use `--committer-date-is-author-date` when rebasing to keep time from the previous author. Note: will not work with `--interactive`.
- Do not use `git add .` before running `git status`. Make sure the right files are being committed. Using a GUI helps. A lot of times the wrong files have been added to commits and results in extra code sniffing done by bots in the CI process, dirtying up pull requests and extra work.

## NPM
- If a task runner in a project is not working (`npx gulp`), there could be conflicts with your system setup. Try deleting the `node_modules` folder and the `package-lock.json` file, then run `npm i` again.
- Do not update `gulp.config.js` files from projects, instead follow the instructions in said file to create a `gulp.config.local.js` to run local URLs if you set up a different URL than the one in `gulp.config.js`. If having problems, ask for help.

## WordPress
- Always add the trailing slash `/` when adding URLs in content of pages, and in code for that matter. You may think it is only one redirect from non-slash to slash, but you may be unaware of other redirects in place or that may be added in the future. Redirects can add to load times and add to bad UX.
- VIP updates their `mu-plugins` repo(s) quite often.
	- Updating them for each project we are working on should be done periodically so we have the latest codebase of their setup so we make sure *our code* works with theirs.
	- Run `git pull` inside the `mu-plugins` folder for each project whenever you have a chance, but not required every single time you're working in a project.
- Install the team's [dev tools mu-plugin](https://github.com/NationalUniversitySystem/dev-toolbox) in all projects but never commit it.
	- If the files are not being ignored, please add them to the project's `.gitignore` file, and add them to your global `.gitignore` file as well.
	- Among other tools, the plugin has the very useful function `write_to_log()` which can be utilized like `console.log()` in JS. The function will log whatever is passed to it to the `debug.log` file so you can inspect strings or any form of data that you are working on instead of printing blocks of code and shifting the layout of the site you are working on.
- Add **all** the CONSTANTS below to `wp-config.php` at the beginning of all projects.
	- Among other things, they will help a lot during debugging and overall development of code. White screen of death won't catch you off guard.
	- This will generate any and all warnings and errors that the codebase might be generating.
	- Helps learn how code blocks, functions, etc actually work and to keep the code as clean as possible.
	- It is recommend splitting your code editor into two columns and having the project's `debug.log`.
	- If you're using the [custom-site-template](https://github.com/Varying-Vagrant-Vagrants/custom-site-template.git) with VVV, there is also custom option for `wpconfig_constants` that will allow adding the constants below while Vagrant provisions your project.

```php
define( 'WP_ENV', 'local' );
define( 'VIP_GO_ENV', 'local' );

define( 'WP_DEBUG', true );
define( 'WP_DEBUG_DISPLAY', true );
define( 'WP_DEBUG_LOG', true );
define( 'SCRIPT_DEBUG', true );

define( 'SAVEQUERIES', true );
define( 'MEDIA_TRASH', true );
define( 'WP_POST_REVISIONS', 5 );
```
