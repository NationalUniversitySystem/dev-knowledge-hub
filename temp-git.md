- GUI vs CLI
- Installation (WIN vs MAC)
	- WIN: Git bash, emulates unix-based 'bash' command line




- GravityForms -> Salesforce integration
Note: Different from MarketingCloud

Salesforce has a 'web-to-lead' API that makes it easy to create new leads in SF via a web form submission.

Salesforce admin panel -> Setup -> Web-to-Lead
Generate Form (doesn't matter what fields you select, we won't be using the actual HTML generated here)

GravityForms webhook:
URL: https://webto.salesforce.com/servlet/servlet.WebToLead

POST
FORM

Select Fields
*IMPORTANT:
- key: "oid" value: "00D8Y000000G7AI"
(find the specific org ID from either the salesforce admin settings, OR by looking at the above-generated HTML, form "action" attribute)