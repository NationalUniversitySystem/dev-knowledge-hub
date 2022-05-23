# Partnership page workflow:

?> _TODO_ Below content is from prior dev documentation. May be out-of-date.

## NU (WES):

- Go to [NU Pre-production Site](https://nu-edu-preprod.go-vip.co/wp-admin/)
- [Add or edit a partnership page](https://nu-edu-preprod.go-vip.co/wp-admin/edit.php?post_type=partnership)
- [Compress any given PDFs](https://smallpdf.com/)
- [Compress any given images and logos if necessary](https://compressor.io/)
- Beautify the name of the files. Example: `NU_Tulare_County_Flyer_06.2021.pdf` to `Tulare_County_Flyer.pdf`
- Add the content given by copy
- Update `Page Attributes`:
    - Parent: `No Parent`
    - Template: `Standard Hero Sidebar`
    - Request `Campaign Activity` and `Organization` field values:
        - Once page is in development, add the URL in the [NU_Partnerships_Organizational](https://docs.google.com/spreadsheets/d/1CEYuLWvMCTCFmRUPbL8ZS9cw-igYbr7VZauYH1utfhQ/edit?ts=5e7e76d5#gid=1054635506) and notify April Resurreccion (to direct a comment type `+` followed by her email address: AResurreccion@nu.edu)
        - April will add the **Organization MKT_WES** and **Campaign Activity** values in the spreadsheet and notify web dev
        - Apply these values to the `Form Setup` metabox
            - **Campaign Activity** field value
            - **Organization** field value
    - Unless otherwise noted in the job description, there is no need to add a hero image. It should be automatically displayed from the "parent" `/partnerships/`.
    - If you need to add the partner logo to the sidebar, create a `custom field` with the name `sidebar_content` and add any HTML you need in the value field. (i.e. `<img src="/wp-content/uploads/xxxx/xx/partner_logo.png" class="any-class-here" alt="The Partner logo.">` - **Do not forget to include the `alt` attribute.**)
    - Every added media coming from wp library itself should **NOT** include `https://www.nu.edu/` or `https://nu-edu-preprod.go-vip.co/`. It should be `src="/wp-content/uploads/.."`
- For `Final Page Internal Upload/Review`, you need Juvanie, a copywriter, a designer, and Megan or Gabby as approvers. You can check for deadlines and approvers in the JIG task's schedule tab
- For `Client Review Template Upload`, you only need the account manager, Megan or Gabby, as approvers
- After `Client Review` round is approved, launch live by adding or editing the partnership page at [NU.edu](https://www.nu.edu/wp-admin/edit.php?post_type=partnership)
- Once the page goes live, switch the development URL to the live URL in the [NU_Partnerships_Organizational](https://docs.google.com/spreadsheets/d/1CEYuLWvMCTCFmRUPbL8ZS9cw-igYbr7VZauYH1utfhQ/edit?ts=5e7e76d5#gid=1054635506) spreadsheet


## NUS
- Create a new page
- Add content from copy
- Update `Page Attributes`:
    - Parent: `(no parent)`
    - Template: `Default template`
- Add `Featured Image`
    - This will be the hero image for desktop
- Update `Page Info`
    - Add `Hero Sub-title` if required from the copy
    - Add `Mobile Hero`.
        - This will be the hero image for mobile. Size should be 600x700 pixels.

