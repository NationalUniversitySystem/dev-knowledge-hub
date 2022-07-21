# RFI Data Routing

There's lots of hidden fields that get set dynamically, based on various criteria.

Data from form submissions typically get sent DoublePositive and Eloqua. The Enrollment team uses OnDemand, which pulls data from DoublePositive sometimes, and from Eloqua sometimes. Nobody really knows how it works (yet!).

WES-related RFI forms will (soon) send data to Marketing Cloud as opposed to Eloqua (?)

You can view/edit the routing via Form Settings->Webhooks

'Designated Team' used to be determined based on zipcode (data stored in wp_zip_data table) but is now manually tagged on a program-by-program (meta field taxonomy) basis

## MarketingCloud
- Standard GravityForms 'Webhooks' functionality doesn't play nice with MarketingCloud, so we have custom functionality built into the back-end.

Plugin: gf-nus-marketingcloud
- Auth token storage + renewal
- Formatting API payload into MarketingCloud-specific JSON format

To check data routing:
Salesforce -> MarketingCloud login (Dan Scott account)
Email Studio -> Email -> Subscribers -> Data Extensions -> **B2B Partners** -> Records
