# Faculty Data Import

## Faculty Photo Importer

Live URL: https://faculty-photo-importer-hbc9gvf6fwceedc4.westus-01.azurewebsites.net/

The faculty photos are imported from the URL above. When the "Import" button is clicked, the photos are retrieved from Workday via the Workday API, then uploaded to each faculty members post based on the Faculty employee ID.

This will take roughly 10 minutes to get photos from API, decode, then update WordPress.

## Faculty Data Importer

Live URL: https://www.nu.edu/wp-admin/admin.php?page=faculty-settings

You will need to be signed in as a super admin in the WordPress dashboard. 

### Instructions:

IMPORTANT NOTE! This sequence is designed to be ran in order. Please follow the steps below in the order they are listed

1. Click "Import New Faculty Data" (This will import the new faculty data and create a post in the faculty cpt)
2. Click "Update Faculty Data" (This will update every faculty post with the current API information)

Note: the API call takes a while so be patient, there will be a confirmation message when it is complete

