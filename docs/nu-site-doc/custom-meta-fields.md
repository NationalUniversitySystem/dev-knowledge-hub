# Custom Meta Fields

We use FieldManager to create custom fields on the WP content editor.

FieldManager documentation: https://fieldmanager.org/docs/fields/

Fields are stored as post metadata, and thus can be called in the front-end via `get_post_meta()` function.

Note that many custom meta fields on various content editor pages are legacy items that are not in use anymore.

There was once a project in motion to convert our custom fields from FieldManager to CMB2. However this involves a large amount of database modification. Progress was started, however paused due to personnel departures. Some sites probably still have feature branches in github for the work-in-progress.