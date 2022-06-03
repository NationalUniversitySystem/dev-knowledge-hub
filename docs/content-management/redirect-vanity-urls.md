# Redirects & Vanity URLs

We use a third-party Redirection plugin to handle all of our redirects and vanity URLs.

Accessed via **Tools >> Redirection**

For vanity URLs, please select 'vanityURL' from the 'Group' dropdown.

When deleting a page (for example, a Program is no longer active), it's generally best practice to create a redirect to an applicable 'parent' page.
Example: `/ourprograms/college-of-professional-studies/healthsciences/programs/clinical-regulatory-affairs/` now redirects to `/ourprograms/college-of-professional-studies/healthsciences/`. When in doubt, just redirect to `/` (home page)

?> *@TODO* we have LOTS of redirects that have accumulated over the years. Many of these look like they haven't been hit in a loooong time, if at all. It also looks like we have some instances of chained redirects (i.e. A redirects to B, but B then redirects to C, etc). Aside from the unnecessary complexity, this also adds some extra bloat to our database. Might be worthwhile to do a 'redirect audit' at some point in the future.