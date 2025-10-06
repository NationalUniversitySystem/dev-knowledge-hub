# Main Data Object API

## Program Data API

Endpoint: https://nu-api-data-eqbehkgpfceqh2ht.westus-01.azurewebsites.net/nu-api/programs

This an Express API endpoint that is hosted on our Azure environment, it is an application named "nu-api-data" composed off all of the data from all of IT's program tables, grouped by their program ID.
This endpoint has become the main source of truth with the program data integrated with our forms and state restrictions so we will need to be careful when updating. 

## Front End Interface

Live URL: https://nu-api-data-eqbehkgpfceqh2ht.westus-01.azurewebsites.net/login.html

- Username: marketingdev
- Password: NatMDev2025!

This is a dashboard where you can see all of the Program data that is in the Express API

## Updating the API Endpoint

If IT pushes an update to the program table, the endpoint will need to be updated with the new JSON file that has been updated. All of the JSON files are in the "data" folder of the "nationaluniversitysystem/nu-api-data" repository. Once the JSON file(s) is updated and the change is committed, the API data will update automatically in the Azure environment