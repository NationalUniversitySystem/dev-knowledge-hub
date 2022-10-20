## Build Workflow

### CircleCI

CircleCI requires an active SSH key in order to authenticate with the GitHub of the repository it's building. These SSH keys rarely-but-occasionally expire and need to be renewed.

If this happens, CircleCI will throw a build error:
`Could not find a usable config.yml because you deleted the CircleCI OAuth app.`

Documentation here: https://circleci.com/docs/github-integration/#enable-your-project-to-check-out-additional-private-repositories