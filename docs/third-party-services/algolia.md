# Algolia

Agamero  8:36 PM
@here - I talked with Mike about the Algolia issue and it seems we are going to need to push any fix we have live and test it out on production. Definitely, not a good practice but that is what he used to do.

If we comment out [these lines](https://github.com/wpcomvip/nu-edu/blob/master/plugins/nuedu-core-functionality/inc/search/class-init.php#L17-L19), we might end up syncing our local stuff with Algolia and that could create some sort of sync issues with production.