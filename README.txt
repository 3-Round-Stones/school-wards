====================
*   Introduction   *
====================

This application shows how Callimachus interacts with more familiar HTML form fields, such as radio, checkbox, and select options.

  1. Access the Home Folder by clicking the main menu in the upper right and selecting "Home folder"
  2. From there, select the red "Create" dropdown and choose "Folder".
  3. Name your folder and click "Create".
  4. Click the main menu and select "Import folder contents"
  5. Click "Choose files" and select the School Wards Callimachus ARchive (CAR) - school-wards.car.

====================
*     Details      *
====================


====================
*       Data       *
====================

This webapp ships with a few UK wards and the schools locate within them. These and other ward can be queried from the http://data.gov.uk/sparql end point using a query like the one below. The included school-data.rdf has been modified to use relative URIs for schools and wards.

[[
PREFIX school: <http://education.data.gov.uk/def/school/>
PREFIX ward:<http://statistics.data.gov.uk/id/local-authority-ward/>

CONSTRUCT { 
	?school ?rel ?resource . 
	?resource ?property ?content 
} WHERE {
  ?school school:administrativeWard ward:00CNGU
  	; ?rel ?resource
  
  OPTIONAL { 
  	?resource ?property ?content 
  }
}
]]