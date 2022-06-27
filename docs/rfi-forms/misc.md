## Misc Notes

Currently Zipcode entry is required on all RFI forms, regardless of whether or not you toggle it as 'required' in GravityForms. This is because we have some back-end processing built around zipcode data.
- '00000' signifies an international entry
- We have a `get_zip_data()` function in `plugins/gravityforms-doublepositive/inc/class-utils.php` which fetches data based on the user's entered zipcode. This function uses a custom `wp_zip_data` table that we have created in the wpdb.
	- This table includes values that are then set for 'designated team' and 'designated military team', which are (presumably?) used in Eloqua/OnDemand/DP.

- In plugins/gravityforms-nus-customization/fields/class-nu-zip-field.php, we have a `fetch_usps_api()` function, which uses the USPS api to check that the entered zipcode is valid. Is this a free API or do we have an account?
	- We also do $wpdb->wp_zip_data lookup here?
	- This file auto-populates 'state' field and attaches to form


### Student Referral Program
Form #1 generates custom URL, form #2 RFI that auto-populates custom 'referral ID' field based on URL parameter