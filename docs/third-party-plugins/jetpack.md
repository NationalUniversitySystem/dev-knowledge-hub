# Jetpack

!> Provided free with WPVIP hosting

Jetpack Search has occasionally shown .ddev (TBF local environment) links in production www.nu.edu. WPVIP support's response to this is:


To avoid future Jetpack syncing issues, we'd like to suggest the following:

- Jetpack-related testing should preferably be done on a non-production environment like develop due to Jetpack's need to have an active connection between the testing environment and WordPress.com.
- When testing on a local development environment is required, vendors and your internal dev team should locally run  wp jetpack status  to confirm the app is locally in offline mode. It should respond "Jetpack is in Offline Mode".
- Please suggest to your development team and vendors to use VIP Local Development Environment, as we provide support for it and it'll ensure Jetpack is setup correctly for local development: https://docs.wpvip.com/technical-references/vip-local-development-environment/
- If an unsupported local environment is used, your team should review https://jetpack.com/support/jetpack-for-developers/ and https://jetpack.com/support/offline-mode/ to make sure the local environment is in offline mode and not connecting to production.
- If a local environment is connected to production, it should be disconnected. In addition, production should then be reindexed to remove any locally changed content that was sent to the production index, for example testing pages that would appear in production search results.

We have suggested TBF try using the WPVIP local development environment, but it's not feasible because they would then only be able to have WPVIP local sites, and due to having other clients they need to be able to code in an environment that works for more than just WPVIP.