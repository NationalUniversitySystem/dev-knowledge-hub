# Custom Settings

## Blocked Domains

Occasionally our paid media will identify large amounts of "bot traffic" creating form submissions on `info.nu`, generally identified as a large amount of entries in a short amount of time coming from unique email domains like __@driveplus.my.id__. When this happens, we have custom functionality built-in to our forms to allow us to block certain form submissions from reaching our CRM, based on the email address entered on the form.

Menu option **Forms >> Settings >> GF Nus Addon**

Under **Blocked Domains**, add the offending email domain (__driveplus.my.id__) to the existing list.

This functionality will still allow the form to be submitted on the front-end (entry data will still appear in wp-admin), however it will prevent any webhooks from firing and thus the entry will **not** be sent to Eloqua, DoublePositive, or whatever CRM we're using by the time you read this.

The code for this lives in our GravityForms-NUS-Customization plugin.

Code reference: https://github.com/wpcomvip/nu-edu/blob/master/plugins/gravityforms-nus-customization/inc/class-custom-validation.php#L50
