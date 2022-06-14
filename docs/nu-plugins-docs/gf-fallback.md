# Gravity Forms - Fallback

This custom plugin was developed with the stated intention of providing fallback functionality to our forms in the event that "Gravity Forms or the server is down". It is currently only activated on info.nu.

?> @TODO investigate the use-case of this plugin. According to Chet it creates a conflict with newer versions of Gravity Forms.

-----------------------------------------------------------
**June 6, 2022:**
According to Chet(TBF), this plugin clashes with Gravity Forms v3.6

Unclear on the specific use-case of this plugin. If the server were down (and thus WP_Query below returned an error status code)... wouldn't this code also not load? 

I pulled all our historical form submissions for info.nu to see if/when this functionality has been used. Forms that are submitted via the fallback function have a `?fallback-form` tag appended to their formID URL in Eloqua. **As of June 2022 the only form entries that have this tag are Mike Estrada's dev-test entries from May 2020.**

-----------------------------------------------------------

Disabled on NU, enabled on info.nu

- For each gravity form rendered on a page, the plugin creates an identical "fallback" form based on HTML hardcoded into the plugin.
- Plugin creates a custom REST endpoint `https://info.nu.edu/wp-json/gravityforms-fallback/v0.2.0/faux/`
- This endpoint runs a WP Query and returns the 3 most recent post IDs. Per comments, it sounds like this is 'junk data' and just intended to prove that we can successfully ping the server.
- On page load, javascript runs axios request to above endpoint
- If response status !== 200, then we run revealFallBackForms() and activateFallBackForms(), which I guess activates the fallback forms created in the first step above.
- Otherwise if WP_Query returns a response, remove the fallback form created in step 1 from the DOM