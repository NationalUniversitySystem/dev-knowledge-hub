# RFI Forms

!> **Important -- "Request for Information" forms are __mission-critical__ for the marketing department. Please be careful when making form-related updates on production.**

!> **Important** When migrating form-related content from preprod to production, please double-check form IDs if applicable. Form ID's are often different across various environments (i.e. a certain form might be form ID #82 on preprod, but ID #86 on production).

## UUID

For any forms that send data to Sparkroom, we add a unique user identifier (UUID). This must be set up on each individual form. The steps to enable UUID on a form include:

- Check in Form > Webhooks to confirm the form goes to Sparkroom.
- In Form > Settings, toggle on "Include UUID" and save.
- In Form > Edit, drag a new hidden field directly after the email field. Name this hidden field "mktattributionid".
- In Form > Webhooks, add one new key-value pair to the Request Body. The key needs to be "MKTAttributionID" (with capitalization) and for the value, choose the "mktattributionid" field from the dropdown.

If the new hidden field does not appear immediately, clearing Cloudflare cache may be needed. The hidden field automatically checks cookies and local storage, and if necessary calls a marketing Azure endpoint, to determine the UUID. This process is started once the first name and last name fields contain more than 2 characters, and once the email field contains a valid email address (characters @ characters . characters).

## Form details

Most RFI's across the site are 'RFI - Default' (form ID #1)

However certain pages have special RFIs:

### RFI - B2C (Partnership Pages)

### RFI - B2B
Currently working to transition these from routing to Eloqua, to instead route to Marketing Cloud. Work-in-progress.

### RFI - Military Outreach
> Gravity Form ID 76

Military outreach advisor pages have their own special RFI version, as these leads are treated differently on the enrollment side. 

This form is similar to our default RFI, but with the following key differences:
- Form includes a "Military Location" dropdown select
- These forms DO NOT route to DoublePositive, and thus there is no SupplierID being generated.
- Lead Routing Group is auto-populated to 'military-outreach'

Example Page: https://www.nu.edu/military/zollie-allmond/

?> *@TODO* These forms still include the military affiliation checkbox option. Would it make sense to auto-check this, or can we even just get rid of it altogether? Need to look into how that checkbox affects routing on default RFI, and whether or not that's already happening automatically on these forms.

### RFI - [other examples...]