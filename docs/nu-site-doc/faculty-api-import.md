# Faculty Data Import

Live URL: https://faculty-photo-importer-hbc9gvf6fwceedc4.westus-01.azurewebsites.net/

The faculty photos and data are imported from the URL below. When the "Import" button is clicked, the photos and data are retrieved from:

 -Workday via the Workday API ('https://wd2-impl-services1.workday.com/ccx/service/customreport2/nus_preview/900010002/INT180_Faculty_Profile_RaaS?format=json';)
 -"Department" custom post type via the WordPress REST API ('https://nu.edu/wp-json/wp/v2/department')
 -"Colleges" custom post type via the WordPress REST API ('https://nu.edu/wp-json/wp/v2/colleges')
 -"Faculty" custom post type via the WordPress REST API ('https://nu.edu/wp-json/wp/v2/faculty')

then the data is compared and uploaded to each faculty members post using the custom fields based on the Faculty employee ID. The fields below are what will be pulled and how they will be mapped in the code to each faculty member.


### Faculty data mapped to the posts custom field

  faculty_employee_id: 'Employee_ID',
  faculty_first_name: 'First_Name',
  faculty_last_name: 'Last_Name',
  faculty_bio: 'Professional_Statement',
  faculty_degree: 'Degree',
  faculty_department: 'Department',
  faculty_department_id: 'Department_ID',
  faculty_education: 'Education',
  faculty_email: 'Email',
  faculty_location: 'Location',
  faculty_major: 'Major',
  faculty_phone: 'Phone',
  faculty_prefix: 'Prefix',
  faculty_title: 'Title'

The faculty members data will be updated only if the data from Workday differs from what is on the nu.edu site. If there is not an update then to faculty member will be skipped and nothing will be updated.

Once a faculty members post is updated their page on the nu.edu site should be updated with the new data from Workday. 


### Instructions:

The instructions for this are simply going to be a button click which will then run the process of updating the data.

### Note

This is currently in progress still to be setup on the live site. The faculty members are developing a workflow to update their profiles on Workday. Once they give the thumbs up this will go live and we will need to set a cron job so the process runs on a schedule. There will also be the option to manually update the posts with the button click

