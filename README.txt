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

This application demonstrates the ability to modify underlying RDF data via familiar HTML form elements. While the templates may look
the same on the surface the underlying code reveals that modifications are being made to the actual RDF via Callimachus' unique
RDFa template syntax. 

The starting page is a list of three school wards. Click through these to see the schools located within each ward. You can then
click through each of those schools to learn more about each specific school. This is where things get interesting. Click the "Edit"
tab in the top right quadrant of the screen when viewing a school and you will be brought to a Callimachus Edit Template for that
school. From here you can make modifications to the underlying data simply by interacting with the form. Click "Save" to update the data. 
You will then be redirected back to the "View" tab where you can see the new data reflected.

To better understand how this works, take a look at the edit tab of the school edit template (school-edit.xhtml?edit). We see here that
inside a classic HTML form element there are some interesting attributes being applied to different elements. It's this {bracket} notation
that communicates to Callimachus, "The value of this form element represents the RDF property denoted here." For example:

[[
<input type="text" id="name" class="form-control" value="{school:establishmentName}" />
]]

Everything about this input tag is standard except for the @value attribute. Notice how we've given the @value attribute a value of "{school:establishmentName}".
This is how the page communicates with Callimachus' database to say "Whatever value the user inputs into this text field - set it as the object of the 
school:establishmentName property in the underlying RDF. Since there is already a value for that property it appears in the input field when the ?edit
tab is loaded. However, if you type something completely new there and click "Save" that new value will replace the old one.

This change is reflected in the view template (which is more frequently used) but the change can also be seen in the "Describe" tab of a given 
resource. Go ahead and give it a try.

 1. Select the "Describe" tab for a specific school
 2. Find the line that starts with "school:establishmentName" and take note of the name following it 
 3. Select the "Edit" tab for that same school
 4. Change the value in the input field underneath "Name"
 5. Click "Save"
 6. Notice how the name has been updated in the View tab
 7. Select the "Describe" tab for that same school
 8. Notice how the name has also been updated in the Describe tab following "school:establishmentName"
 
Any of the values you see in the Describe tab can be modified via the edit template if the appropriate markup is used. You'll notice text inputs
aren't the only options - radio buttons, checkboxes, textareas, and others are also supported. 

Explore the edit template (school-edit.xhtml) and the full documentation at http://callimachusproject.org to learn more about Callimachus templates 
and how to use them. 

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