# Facebook CAPI (Conversion API Gateway)

Facebook Developer Documentation: https://developers.facebook.com/docs/marketing-api/conversions-api

- We self-host Facebook's Conversion API Gateway program via AWS
- https://vawpob.nu.edu -> Login info stored in logins doc

In Feb 2023 we had an issue where the domain-level SSL for vawpob expired, which caused our Facebook Lead Scores to drop substantially.
Because there was no prior documentation left for vawpob, we had no way of logging in to re-generate the certs.
Solution was to delete and re-create the entire instance on AWS, using the same domain name.
This was possible because we don't have any custom code on vawpob, it was just the Facebook CAPI code which we were able to deploy via FB Business Manager dashboard.