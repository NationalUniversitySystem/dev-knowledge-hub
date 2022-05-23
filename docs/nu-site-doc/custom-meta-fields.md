# Custom Meta Fields

We use a third-party plugin **FieldManager** to create custom fields on the WP content editor.

FieldManager documentation: https://fieldmanager.org/docs/fields/

Fields are stored to the $wpdb as post metadata, and thus can be called in the front-end via the WP `get_post_meta()` function.

**Note**: Many custom meta fields on various content editor pages are legacy items that are not in use anymore. It might be a good future project to audit these fields to identify & remove ones that are no longer in use.

**Note**: FieldManager is *not* widely, and does not appear to be actively maintained anymore. There was once a [project](https://github.com/wpcomvip/nusystem-org/issues/412) in motion to convert our custom fields from FieldManager to [CMB2](https://cmb2.io/). However, this migration requires a certain degree of database modification, since FM and CMB2 store certain types of data in the database in different formats. Progress was started but then put on hold due to personnel departures. Some sites have feature branches in github for the work-in-progress. [Example](https://github.com/wpcomvip/nusystem-org/tree/cmb2-migration/plugins/nus-core-functionality/fm-to-cmb)

Although [ACF](https://www.advancedcustomfields.com/) is generally considered the "gold standard" for implementing custom fields in WordPress, there is a good development rationale for instead using FieldManager/CMB2 for larger-scale sites like ours. [This Article](https://salferrarello.com/cmb2-vs-acf/) does a good job of explaining the major reasons why.