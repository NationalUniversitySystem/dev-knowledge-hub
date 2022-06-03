# WPVIP

WPVIP is our hosting provider. It is the enterprise hosting service provided by Automattic, the company behind wordpress.

## Support Tickets
Support Ticket URL: [https://wordpressvip.zendesk.com/hc/en-us/requests/new](https://wordpressvip.zendesk.com/hc/en-us/requests/new) (login required)
- 'Urgent' priority should only be given to mission-critical, time-sensitive problems (i.e. site outages, workflow-blocking problems)
	- In the past year, the only time we've have to submit an 'urgent' ticket was when logging in to `nu.edu/wp-admin` started redircting us to `preprod`.
- We're allowed to open support tickets asking for "coding advice/best practice guidance". I did this once and they actually provided a really helpful, in-depth response, where they even dug into my code a bit and highlighted specific lines. Definitely a good resource to keep in mind. [Example](https://wordpressvip.zendesk.com/hc/en-us/requests/142667)

## Caching
WPVIP provides platform-wide caching. When developing/launching new features, we will often need to manually flush the cache. This can be accomplished either via the CLI, or on a single-page basis by visiting the page while logged in as an admin, and selected 'Flush Cache for Page' from the top admin menu bar.

Reference: [https://docs.wpvip.com/technical-references/caching/](https://docs.wpvip.com/technical-references/caching/)

Note: We also currently use Cloudflare which provides extra caching for us. If flushing the WPVIP cache does not have the intended effect, try cloudflare.

## Salesforce
WPVIP is building a custom integration tool for Salesforce Marketing Cloud. Not released yet -- might be worth revisting later this year once we're up and running with Salesforce and WPVIP has officially launched the service.


-----------------------------------------------------
Todo/Info to add:
- How to set up new user accounts
- Platform quirks/etc
	- i.e. requires you run either the latest or second-latest version of WordPress
	- Certain 'code standards' it enforces, VIP review bot scans all code pushes
	- etc.
- MU-Plugins
-----------------------------------------------------