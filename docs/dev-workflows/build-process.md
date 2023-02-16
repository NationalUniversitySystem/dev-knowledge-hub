# Build Workflow

Basic Process:

1) Code pushed to "live" branch (preprod, develop, or master)
2) CircleCI runs the build process (generally takes a couple minutes)
3) If successful, CircleCI pushes all changes to the appropriate '-built' branch (preprod-built, develop-built, master-built)
4) WPVIP takes the code from the '-built' branch and deploys it to our live site (generally takes a couple minutes)
5) Caches will generally need to be cleared, including Cloudflare if applicable

## CircleCI

We use a service called CircleCI to run our build & deploy process. This is necessary because we do not include asset files (i.e. final CSS & JS) in our git repos. In our local environments, we solve this by running `npm run gulp` -- for our live server environments CircleCI essentially does this for us.

CircleCI "watches" all of our "live" branches (i.e. preprod, develop, master) and runs the build process anytime there is a change to one of those branches in Github. It then runs the build process as configured in the `.circleci/config.yml` file.

When the build process is complete, CircleCI notifies our slack channel #nu-github. If there is a problem and the build process fails, it will notify the slack channel and also send you an email.


### Troubleshooting

CircleCI requires an active SSH key in order to authenticate with the GitHub of the repository it's building.

SSH keys will periodically need to be re-generated. There are 3 components to this: First, delete and re-generate from within CircleCI->Project Settings->SSH Keys. Second, delete and re-add to the relevant Github repo Deploy Keys. Third, update the codebase's .circleci/config.yml file to update the 'fingerprint' value provided by CircleCI.

## WPVIP

WPVIP is set to "watch" our '-built' branches, and deploy changes to our site whenvever there is a change to one of those branches.