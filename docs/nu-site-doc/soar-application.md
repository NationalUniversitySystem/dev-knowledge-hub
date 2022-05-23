# SOAR Application

- Maintenance Mode
- Entries that are unsuccessful generate an automated "Error" email that gets sent to the dev team.
- How to manually re-send unsuccessful submissions to SOAR

--------------------------------------------------------
The below was copy/pasted from Mike's 'SOAR Maintenance Documentation' file on Sharepoint, dated 1/25/22


### SOAR Maintenance Documentation 

The SOAR system is run by IT and is where a lot of HR and intranet data is managed. Said system is used on the marketing website to manage Faculty pages content and it is also used to send POST requests from application submissions. The marketing website usually points to the SOAR application process anywhere the “Apply Now” CTAs are present by redirecting to the SOAR page or a marketing website page when SOAR is receiving maintenance. 

Although at the time of writing this document part of the application process is being taken out of the SOAR system, previously POST requests were only sent to SOAR when it was in maintenance mode. Maintenance occurs once monthly with IT sending emails to specific people about the schedule, when maintenance has started, and when it has ended. During that maintenance period, the marketing website takes over for partial applications on the page https://www.nu.edu/online-app/. 

In order for the “Apply Now” CTAs to point to that page instead of the SOAR website, a checkmark in the www.nu.edu website needs to be turned on. You can get to that option by navigating to the admin side of the website -> Appearance -> Customize (a new page will load) -> SOAR Maintenance -> SOAR Maintenance Status -> check the box and then hit “Publish” CTA at the top of the page. This will need to be done at the IT defined time (usually 4pm on a Saturday). 

Once IT is done with maintenance, an email will be received the next day (Sunday) and the same option can be checked off. This will trigger all the entries that were submitted at the Application form https://www.nu.edu/online-app/ to be sent to SOAR. 

Some entries may fail due to time outs. In order to identify those entries, visit the following URL to see the form’s entries and check for empty values in the “soarUUID” column. https://www.nu.edu/wp-admin/admin.php?page=gf_entries&id=56 

There are two options to resubmit the entries: 

Select all the entries that are missing the “soarUUID” and then select the “Bulk options” dropdown on the page -> “Submit to SOAR” -> “Apply” button. 

View an entry individually. There should be a meta box that will have a “Submit to SOAR” button. 

If successful, a “soarUUID” value will be returned and displayed for the entries. 