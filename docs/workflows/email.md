# Email Builds

## Legend
*CR: Creative Review*

*CE-AS: Channel Expert & Account Services*

---

## Steps
The following steps are based on the [Email Project Schedule Breakdown](https://docs.google.com/spreadsheets/d/1-YDvSdWL7-4Rg9_A_a0Sr51ORVJpds756IwNvv0iFI4/edit#gid=0):
- Use copy deck from Copy team member that should be tagged for dev in Jig.
- Choose affiliate and type of HTML template that is needed or referenced job # on Google Drive/Workamajig. References for templates can be found in the [Email Templates Google sheet](https://docs.google.com/spreadsheets/d/1iidUG-57gmt0lOa988mLr1Ilt1ThcGN29fJQzQr54yc/edit#gid=1872926667).
- Email template development:
	- Add template as new folder in the [email-dev](https://github.com/NationalUniversitySystem/email-dev) repo.
	- Add/Delete what snippets will be needed base on copy.
	- Add the copy from the deck into the correct snippets within the HTML template.
	- Update HTML email template to add images if necessary. Keep images in repo using relative paths. Some commonly used images are in the root folder in `/images/`.
	- Commit changes with the message being prefixed with the Jig job number.
	- **Notes / Tips:**
		- Wait until review rounds are completed by all reviewers to make template updates, because sometimes decisions are changed in the process.
		- If single file, use `index.html` in the email project's folder to share shorter URL.
		- If multiple files being delivered, exclude Jig job in file name to make the URL less redundant, use only part name (e.g. `webinar.html` and `webinar-reminder.html`).
		- Optional: update the `index.html` file in the root of the [email-dev](https://github.com/NationalUniversitySystem/email-dev) repo for easy access.
		- The [email-dev](https://github.com/NationalUniversitySystem/email-dev) builds take ~30 seconds max and are hosted at [nus-email-dev.netlify.app](https://nus-email-dev.netlify.app/).
- Workamajig Proofs
	- Template Internal Review (CE_AS Internal Review)
		- **Deliverable name**: HTML Template: Internal Review
		- **Approval list**:
			- Copy writer: Deb, Adam, Karaline, Andrea, Brooke, or other copy writer.
			- Design: Alicia
			- CE Email: April
			- Account Manager:
				- NU, NUS & NUVHS: Gabby || Megan
				- NCU & CityU: Denisse
				- The Programs (Harmony - Fundraising Academy - Inspire): Kirsten
				- NUS HR Emails: Danielle
		- **Notifications**: yourself, Juvi, Lynda || Danielle, & the selected people from options above.
		- **Deliverable file**: Use the URL from Email tool.
	- Client - Review
		- **Deliverable name**: HTML Template: Client Review
		- **Approval list**:
			- NU, NUS & NUVHS: Gabby || Megan
			- NCU & CityU: Denisse
			- The Programs (Harmony - Fundraising Academy - Inspire): Kirsten
			- NUS HR Emails: Danielle
		- **Notifications**: yourself, Juvi, April, Lynda || Danielle, Alicia, whoever wrote the copy, & the person from option above.
		- **Deliverable file**: Use the URL from Email tool.
	- Final Proofread - Review
		- **Deliverable name**: HTML Template: Final Proofread
		- **Approval list**:
			- Whoever DIDN’T write the copy. Person should be the one who's assigned for this task on the "Schedule" tab.
		- **Notifications**: yourself, Juvi, Lynda || Danielle, whoever wrote the copy, & the person from option above.
		- **Deliverable file**: Use the URL from Email tool.
- Email Template prep
	- Upload images to ELQ (ELQ login > components > images).
	- Replace image URLs in template.
- Test email template on [Acid](https://www.emailonacid.com/) (fix issues)
	- Use the name of the project for the *subject line* so it is easy to reference in the future.
	- Make sure the tests that ran include the following (should already be included in default settings for account):
		- iOS and Android mobile devices
		- Tablet
		- Mac Desktop Outlook and Mail
		- Windows Outlook and another mail client
		- Dark mode tests
- Upload and save template to Eloqua under the correct folder location (i.e. All > NU > Newsletter > [Workamajig number & job name])
	- Under Emails menu: Create an Email > Blank HTML Email > paste code > add "From" options (name & email from deck) > save )
- Save in the correct location:
	- [Google Drive](https://drive.google.com/drive/folders/1QmKy2TpwRX23dFknkixXDEHUb_eAkcdY?usp=sharing) (HTML file and image(s))
- Delete folder from [email-dev](https://github.com/NationalUniversitySystem/email-dev) repo.
- Send confirmation in Jig.
