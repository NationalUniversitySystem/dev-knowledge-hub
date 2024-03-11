# NU Website Forms 

!> Forms are considered "mission critical" to our website. Do not edit anything form-related unless you are sure of what you are doing, and are ready to communicate the change to the broader team. Don't be afraid to ask for help or double check with someone! Even a seemingly-inconsequential change could end up breaking things.

**Context**: At it's core, our website is a marketing channel with the goal of generating leads (aka prospective students) who eventually enroll at the university. The way that our website accomplishes this is by getting website visitors to fill out an "RFI" (Request for Information) form. This is why nearly every single page on the website has an RFI form of some type. Form submissions are how we are able to measure the ROI of the website, and thus any problem affecting form submissions is considered a "Level 1" event which requires immediate attention. 

**Process Flow**
1) User submits RFI form
2) Custom processing occurs on the backend (supplier ID, etc)
3) Entry gets saved to wordpress
4) Webhooks fire -> Data sent to third-party platform(s)

## GravityForms

We manage all of our form functionality via GravityForms, a third-party plugin. While normally our internal dev goal is to build out all custom functionality as opposed to rely on a third-party plugin, in this instance it makes sense. Forms are generally labor-intensive to manually build, with lots of edge cases to account for and things that can go wrong, not to mention storing & routing form submission data. Given all that, along with the fact that forms are mission-critical for us, as well as the fact that GravityForms is created by a reputable company and actively maintained/updated, using GravityForms is a no-brainer here.

We have an "elite" subscription license to GravityForms, which renews annually. This gives us access to tech support, as well as premium GF Add-on's.
- GravityForms Dashboard: [link] (login data can be found via google doc)
- GravityForms Documentation: https://docs.gravityforms.com/
	- This includes both wp-admin documentation (i.e. How to set up a form) as well as developer documentation (code stuff)

**Plugin Versioning**: Most of our sites are currently (Oct 2022) using GF version 2.6.x, however some of our sites are still using version 2.4.xx. We should make it a point to keep this up to date. Given the mission-critical nature of forms, however, all updates should still be thorougly vetted & tested before reaching production.

## Add-on's & Extensions

### GF Official Add-on's

GravityForms offers a wide array of official "add on" plugins, to extend the functionality of GravityForms. The full list of these can be found from our GravityForms account dashboard, and we have access to any & all of them thanks to our elite-tier subscription. Most of the official addons are e-commerce related and thus not relevant to us, however there are a couple that we use:
- **GravityForms Webhooks**: This is mission-critical for our current implementation of GravityForms. More on this below
- **GravityForms Advanced Post Creation**: This is (was?) used on community.nu.edu and anniversary.nu.edu. Unclear the extent to which it is used, or if we still need it.
- **GravityForms Chained Selects**: As of Oct 2022, unclear if we still use this anywhere. My hunch is that we initially (years ago) used this to dynamically populate our "Select Degree" -> "Select Program" form dropdowns, but then our custom-coded solution replaced that. Should look into whether or not we still use this anywhere.

### NU Custom Add-on's

One of the benefits of GravityForms is that it's built in a very developer-friendly manner, meaning that it's relatively easy to build custom plugins that extend/modify it's functionality. We have a handful of custom add-ons we have developed internally, most of which help GravityForms integrate with NU's various business platforms & CRMs.
- **GravityForms DoublePositive**: This adds functionality related to how form data gets processed before being sent to DoublePositive. DoublePositive is a platform used by the NU enrollment team to follow up with prospective students via phone call -- this plugin dynamically generates certain metadata (supplier ID, Lead Flag, designated team assignment) that enables that business process to work effectively.
- **GravityForms Fallback**: [Unclear if this is still used or needed... or what the actual use case even was. [See additional info here](nu-plugins-docs/gf-fallback.md)]
- **GravityForms NUS Customization**: This is where most of our GravityForms customizations live. This creates all of our custom fields that can be used on GravityForms. For example, while GravityForms provides us with a standard "zip code" input field, we have a custom version that we use instead because it better integrates with our broader business logic.
- **GF-NUS-MarketingCloud**: Custom functionality that allows GravityForms Webhooks add-on to be compatible with MarketingCloud
- **GF-NUS-Sparkroom**: Custom functionality that allows GravityForms Webhooks add-on to be compatible with Sparkroom

## Form Fields

GravityForms provides us with a wide array of "standard" and "advanced" form fields to use. These are all pretty straightforward and thus will not be covered here. The only thing to note is that if adding one of these fields, check to make sure we don't have a custom version instead. For example while GravityForms provides us with a "phone number" field, we have our own version.

GravityForms also provides us with a selection of "post" and "pricing" form fields. These are not applicable to how we use our forms, and can be ignored.

### NU Fields

We have a wide array of custom fields that we have created. Some are self-explanatory, while others are a bit more complicated.
- **Honeypot field**: This is a "trap" field, designed to catch bot submissions. This creates a field labeled "Form Email Field" which is not displayed on the form's actual front end. On legitimate form entries, this field will be blank because it is hidden. Bots, however, will usually fill this out because they see it labeled "email", which is usually a required field. We have back-end functionality that will auto-delete any form submissions that have a value in this field. While we could use something like recaptcha for this, this method provides a better UX as the user doesn't need to check an "I'm not a robot" box or select a series of images. Allows for less "friction" in the form submission process.
- **Journaya**: Journaya field is not currently used. This was part of a very large and hastily-planned third-party platform integration, which turned out to be a monumental waste of everyone's time due to poor leadership.

### Hidden Fields

We make extensive use of hidden fields throughout our forms. These often consist of values that will be dynamically generated for purposes of data analytics/tracking/etc, such as UTM's, Google Analytics IDs, referral domains, etc.

Hidden fields can be set to auto-populate via URL parameters. Under Field Settings->Advanced, checkbox for "Allow field to be auto-populated", and add the URL parameter we want to check for. Some hidden fields are also auto-populated via custom code.

## Webhooks

Webhooks are what allow us to automatically send form submission data to various external platforms (DoublePositive, Eloqua, Sparkroom, etc). While we could build this out manually, GravityForms provides us with an official Add-On that handles this for us and is super easy to use.

After a form submission is saved as an entry to wordpress, GravityForms will look for any Webhooks enabled for the form and send out API requests based on that.

Specific configuration values (URL, request type, data format) will be specified/provided by the target platform. We may need to check that platform's developer documentation, or reach out to that platform's tech support contact.

**Key/Value Mapping**: The 'key' values need to match what they're called in the target platform. For example, all of our RFI's have a "First Name" input field. DoublePositive saves this field as "FirstName", while Eloqua refers to it as "fname". We need to make sure our 'key' reflects that for each webhook, otherwise data will be lost. If we need to clarify external platform field names, reach out to Claire Leong.


### Platform-specific Integration Notes

[certain platforms (marketingcloud) aren't compatible with out GF Webhooks works out-of-the-box. We have custom "helper function" that solves this on the back end. Key value pairs need to be named a certain way though]

## Testing & QA

[Eventually, ghost inspector]
[Adding 'debug' and 'test' hidden fields]

