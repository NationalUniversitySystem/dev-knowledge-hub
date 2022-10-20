# WPVIP Website Code Release Procedure

## Important notes
- If the branch/environment exists, always do a pre-release into `preprod`.
- Make sure releases/merges to `preprod` and `master` are of the "merge commit" type.
	- The green button for merging the PR will be labeled "Merge pull request" and in the drop down it is named "Create a merge commit".
- Feature merges into `develop` should be merged in the rebase method where the green button will be labeled "Rebase and merge".
	- This is done so that `develop` has all our features' commits and the commits in `master` + `preprod` stay as clean as possible.
- The [GitHub CLI](https://cli.github.com/) is a great tool to remove redundancies and manual parts of this procedure. This guide will give examples for with/without that tool.

---

## Defining the changelog
- There should be a Release template for the merge description under `~/.github/PULL_REQUEST_TEMPLATE/release_template.md`
- Gather the Pull Requests(PRs) that were merged into `develop` since the last release (i.e. those that have the HEAD as `develop`), using your preferred method. Options, but not limited to:
	- Using **GitHub CLI**.
		- `gh pr list --state merged --search "NOT preprod in:title sort:updated-desc"` (at time of publishing) will list most of the information needed.
	- Manually through GitHub UI.
		- Visit the repo URL `{repo-url}/pulls?q=is%3Apr+is%3Amerged+NOT+preprod+in%3Atitle+sort%3Aupdated-desc+`
		- Collect the #, title, and note what it affected (theme, plugin, workflow, etc) to match with the Release PR template.
- Make sure to exclude any PRs that were merged into `master` since they should not be in the release notes/changelog.
- Place the PR messages into the corresponding section of the Release Template.
- If applicable, add mentions or closing keywords for issues in the corresponding `## Issues` section.
- Release names can be found/saved in the site's corresponding sheet in the team's [Google Sheet](https://docs.google.com/spreadsheets/d/19Y3imaw_jkhg2IKVWzxl7G-3eZUpxMWwxSdikmEUcX8/edit#gid=0).
- **GitHub CLI use:** Save as markdown file and note it's path.

---

## Release steps
### GitHub CLI
Run the following command line commands to generate the PRs and create the release. Commands should work in both Mac and Windows.<br>
Replace the whole string(s) in the commands with the appropriate values, yes including the curly brackets: `{note}`.<br>
The `--draft` flag is optional.<br>
Each command will echo the URL of the actual PR.
- `gh pr create --draft --title "{release version/number} pre-release" --body-file ~/{path/to/release/notes.md} --assignee @me --base preprod --head develop`
- `gh pr create --draft --title "{release version/number}" --body-file ~/{path/to/release/notes.md} --assignee @me --base master --head develop`

Example:
- `gh pr create --draft --title "v2.17.0 pre-release" --body-file ~/Desktop/nu.edu-v2.17.0.md --assignee @me --base preprod --head develop`

Once the last PR is merged into `master`, run the command below to create a release.<br>
**Note:** Major and Minor releases get names (v1.XX.XX and v1.1.XX) but not patch releases (vX.X.1).
- `gh release create {release version/number} --title "{release version/number} - {name of release}" --draft --notes-file ~/{path/to/release/notes.md}`

Example:
- `gh release create v2.17.0 --title "v2.17.0 - Agua de Jamaica" --draft --notes-file ~/Desktop/nu.edu-v2.17.0.md`

### Manual
- First do a `vX.XX.XX pre-release` PR from `develop` to `preprod` so the environments stay in sync and let any CI tests complete.
	- Paste the perviously determined release notes into the description.
	- Assign yourself to the PR.
- After the above, do a PR from `develop` to `master` with the release number `vX.XX.XX`.
	- Paste the perviously determined release notes into the description.
	- Again, assign yourself to the PR.
- Tag the release under `/releases`
	- Use the same release notes as the PR into `master` branch.
	- Major and Minor releases get names (v1.XX.XX and v1.1.XX) but not patch releases (vX.X.1).

### After GitHub Release Creation
- If applicable, monitor the CI dashboard for completion.
- Run any post-launch tests.
	- Confirm that features in the release are working either manually or through any CI processes.
	- If the site includes an `info` subdomain, or marketing landing pages, there should be a Cypress testing workflow in the team's [form-tests repo](https://github.com/NationalUniversitySystem/form-tests). Run the reports generator script for the corresponding site and save the files to Google Drive.
- If accessible, add an annotation of the release and version number to Google Analytics.

---

## Housekeeping
- Clean unused and already merged `branches`. Make sure you exercise good housekeeping by deleting unused branches locally and remotely.
- Close `issues`. Make sure you close those issues that have been fixed, in case they were not automatically closed via keywords in the release notes.




------------- Temp notes

Agamero
  2:57 PM
go ahead and create the PR, please. I'm assuming there'll be a bunch of commits. I'll show you how to "clean" that and squash them
we dont want that cause there is no point for having all those commits since I guess they are all related to the same feature, the SMS Pilot

please create a new PR from your branch to merge all those changes into develop. I think, you are going to need to practice the git rebase command to squash those commits as much as possible, please.

Agamero
  3:27 PM
so while you're on that branch where you are working on (plugins/nuedu-forms/sms-pilot) and you have the latest version of the branch where you want to merge your changes pulled down (in this case develop ):
you should use the command git rebase -i develop
hopefully you should have a rebase setup to open in your editor…
then squash your commits. Remember, at least one commit should have the option pick.
(replace pick with squash)
save and close that tab on your editor
new tab editor opens up and remove those commit messages that you no longer need
and at then use git push --force to push your changes to the PR that you created




Mike
  10:59 AM
i saw that the modality feature is now approved. i can include it in tomorrow’s release. should be early in the day.
to include it into develop though we’ll have to do a git rebase, since it was originally “branched off” preprod  but it is now intended for develop.
If we dont do this, there will be extra commits and irrelevant features from preprod when we’d put the themes/national-university-hotb/modality-links branch into develop.
the main command(s):
while on any branch: git rebase --onto origin/develop 4787c361c themes/national-university-hotb/modality-links
 If already on the modality links branch: git rebase --onto origin/develop 4787c361c
after that’s done you’ll have to git push --force to actually push the branch.
explanation:
what the command(s) does is “snap/cut” off the branch from the commit with hash 4787c361c and places on top/on the tip of origin/develop .
 notes:
4787c361c  is where preprod used to be at. because the HEAD of preprod has moved, we have use the specific commit hash instead of just the name.
using the origin/develop just to make sure the branch is placed at the top of the remote version of develop, in case you can’t fetch and have your local develop branch up to date.
if you’d like to clean up the commits as well, you can add the --interactive / -i flag to squash/remove/edit/etc commits.
template:
git rebase --interactive --onto {branch name or hash of where you want to go} {originally where you branched off} {the branch youre moving (optional)}
finally, theeeeen create the PR in Github towards develop. you can make it the same as #1505






- Feature `branch` off of `develop`
- Commits during development of feature
- github PR `branch` -> `preprod`
- git rebase -i preprod => squash commits [or maybe not, don't have to?]
- Approve PR and merge into preprod (merge commits, already squashed)

- github PR `branch` -> `develop`
- Rebase merge


- [test 1] currently on same path as develop

- feature branch PR into develop [rebase]


- 

undo last merge (or just revert commits)
https://www.freecodecamp.org/news/git-undo-merge-how-to-revert-the-last-merge-commit-in-git/