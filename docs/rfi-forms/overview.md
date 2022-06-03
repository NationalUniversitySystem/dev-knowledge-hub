# RFI Forms

"Request for Information" forms are mission-critical for the marketing department. Please be careful when making form-related updates on production.

When migrating form-related content from preprod to production, please double-check form IDs if applicable. Form ID's are often different across various environments (i.e. a certain form might be form ID #82 on preprod, but ID #86 on production).

Most RFI's across the site are 'RFI - Default' (form ID #1)
However certain pages have special RFIs:

## RFI - B2C (Partnership Pages)

## RFI - B2B
Currently working to transition these from routing to Eloqua, to instead route to Marketing Cloud. Work-in-progress.

## RFI - Military Outreach
> Gravity Form ID 76

Military outreach advisor pages have their own special RFI version, as these leads are treated differently on the enrollment side. 

This form is similar to our default RFI, but with the following key differences:
- Form includes a "Military Location" dropdown select
- These forms DO NOT route to DoublePositive, and thus there is no SupplierID being generated.
- Lead Routing Group is auto-populated to 'military-outreach'

Example Page: https://www.nu.edu/military/zollie-allmond/

?> *@TODO* These forms still include the military affiliation checkbox option. Would it make sense to auto-check this, or can we even just get rid of it altogether? Need to look into how that checkbox affects routing on default RFI, and whether or not that's already happening automatically on these forms.

## RFI - [other examples...]