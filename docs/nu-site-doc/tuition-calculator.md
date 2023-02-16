# Tuition Calculator

Live URL: https://www.nu.edu/admissions/financial-aid-and-scholarships/calculator/

Allows students to calculate estimated tuition costs based on their desired degree program and any applicable tuition reductions or scholarships.

**Cost/numbers are inputted by us via WP-Admin**
These can be updated by **WP-Admin->Tuition Reductions** and **WP-Admin->Tuition Tiers**
*Unclear who provides us these numbers*

The Tuition Calculator is built in react.js and embedded within the page, via [/page-templates/tuition-calculator.php](https://github.com/wpcomvip/nu-edu/blob/master/themes/national-university-hotb/page-templates/tuition-calculator.php). 
This template then calls the 'enqueue_react_assets' hook (custom hook created by us), which loads the tuition calculator to the page. 

**IMPORTANT: actual page needs to include `<div id="financial-planning-calculator"></div>`, as this is the target div to load the actual react app**

## React Component
The react code for this is included in our custom plugin nus-react-wp (this plugin includes various react-based features used across the site, tuition calculator is only one of them).
https://github.com/wpcomvip/nu-edu/tree/master/plugins/nus-react-wp

## PHP Component
The PHP code for this lives in our custom plugin nuedu-core-functionality >> inc/tuition-calculator/
This code creates a custom REST API which links our React front-end with the actual tuition cost data that's stored in wpdb.
https://github.com/wpcomvip/nu-edu/tree/master/plugins/nuedu-core-functionality/inc/tuition-calculator

Additionally, CPTs for 'Tuition Tiers' and 'Tuition Reductions' are created here:
https://github.com/wpcomvip/nu-edu/tree/master/plugins/nuedu-core-functionality/post-types
(also creates custom taxonomy 'student-affiliation')

## WP Admin Component
We have two custom post types: Tuition Tiers and Tuition Reductions. These 'posts' then contain the actual dollar-cost data for various degree programs, scholarships, etc.


@todo: Lots of moving parts/logic with how the calculator actually calculates. Worth a deeper dive

@todo: Where do we get the cost data from?