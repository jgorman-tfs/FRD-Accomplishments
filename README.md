# FRD-Accomplishments 
This repository contains information related to creating the FRD Accomplishments Map and other needed information.<br>

*Last updated 9-11-24*
## Purpose
The FRD Accomplishment Map is included in the FRD Accomplishment Report that is written by Hughes and sent to Al every quarter of the fiscal year. The map serves as a visualization of all the quarterly accomplishments. Other ancillary information is also collected and reported to Hughes. 
## Key Components
Primary data is collected from 2 sources: Brad and Mac in the form of excel reports. 
Brad's report contains ELMR information that is gathered through SQL queries and is generally good to go. 
Mac's report contains ELMR and SPAM (federal reporting) information that is only related to Urban and Community Forestry, and generally needs re-working.
Seconday data includes County Boundaries, City Boundaries, and U.S. Census Bureau Places (Texas) 

Download Shapefiles from:
https://texasforestservice.sharepoint.com/:f:/s/Share-ForestAnalytics/EhiEZHqHIFlMuBF89EYSjMYBi2phThOwS_X_64GVVGmDmA?e=0VKab2
## Structure
Q1 - September, October, November (Map due in December) <br>
Q2 - December, Janruary, February (Map due in March)<br>
Q3 - March, April, May (Map due in June)<br>
Q4 - June, July, August (Map due in September)<br>

Accomplishments are symbolized by County layer in the following Classes:<br>

Conservation Education<br>
Management Plans<br>
Technical Assistance<br>
FIA Plots<br>

Brad's report already has information in this format <br>
Mac's report needs reworking to conform to this format <br>

*From ELMR Sheet:* <br>

**Conservation Education**: <br>
*  Arbor Day Program <br>
*  UF Presentation <br>

**Technical Assistance**<br>
*  Tree Planting Event<br>
*  Tree Board Assist<br>
*  UF Incidental/Individual Assist<br>

*From SPAM Sheet:* <br>

**Conservation Education**<br>
*  Tree City USA<br>
*  Brochure<br>
*  Conference<br>
*  Education/Outreach<br>

**Technical Assistance** <br>
*  EAB Pest Detection<br>
*  Landscape Plan<br>
*  Management Plant<br>
*  Tree Inventory<br>
*  Tree Planting<br>

These categories may change over time, depending on what Hughes or Gretchen wants to show. 
Symbology is **Dot Density**<br>

Also needed is number of communities assisted (U&CF) and acres of those assisted

## Methodology
The workflow for this report is somewhat tedious because of the structure of the raw data. It is also difficult to automate because of the amount of checks required along the way. <br>
Here is the general workflow pattern:

**For getting the acres of the communities**
 1. Copy all cities and type of assistance from SPAM and SSPR into a separate sheet.
 2. Copy all office locations and types of assistance from ELMR into the same sheet, right below the others. (This is because ELMR shows assists by county, not city. So were substituting the office city as a "community").
 3. Create a table and filter the categories to show only the needed categories (see above)
 4. Copy fitlered data into a new sheet and create a new table. (This is to preserve data along the way in case you need to go back)
 5. In the cities column, replace all "City of, Village of, CDP of, etc so you only have the city name.
 6. Remove all spaces and punctuation. (This is to match the data in the City shapefile. If you are using you're own city shapefile, remove all the spaces. This makes all the names the same and prevents join errors.)
 7. Remove duplicates to you only have unique cities in your column. (I find it better to highlight and manually delete them. This lets me comb through and check for misspellings and get a better look at the cities.
 8. Use your own judgement when you delete cities and duplicates. For example, you may see Austin and Austin South. Just keep one Austin.
 9. You now have a PRELININARY list of all the unique cities for this Quarter.
 10. Import the table into ArcGIS Pro.
 11. Run a Join Field from the Texas_Cities_WithCounties into your newly imported table and transfer one of the fields. Match City name to City name. (This will allow you to see which cities from your table do not match the larger city shapefile)
 12. Sort your your table by your newly joined field to see the null values.
 13. Figure out why they aren't joining. Some common reasons include:<br>
     -They aren't actually cities but counties. In this case, just delete them.<br>
     -They are misspelled. In this case, edit to match the shapefile.
 14. Create a new field in your table named "Acres for FY?? and Quarter??"
 15. Calculate the acres to 0. (This will let you select the cities that are not null when you join fields)
 16. Join Field from your table to the city shapefile, matching city names, and transfer only your newly created field.
 17. Select the Acres that are not null, calculate the acres.
 18. Run Summary Statistics for the sum of the acres.
 19. The out put table is your total acres this quarter's communities

**For getting the accomplishments of each county**
1. These initial steps are similar to above, but there are a couple key differences. You will not remove duplicate values and you will not copy the cities from ELMR. (This is because ELMR already records the county.)
2. Copy the ELMR Counties and types of assistance into a new sheet and insert into a table.
3. Filter the table, keeping only the neccessary categories. (See structure section above).
4. Import this table into ArcGIS Pro, name it FY??Q??_CountiesFromELMR
5. Import the spreadsheet from Brad into ArcGIS Pro, name it FY??Q??_CountiesFromBrad
6. Copy the Cities and Types of Assistance from SPAM and SSPR into a sepeate sheet and insert to table.
7. Filter the table, keeping only the neccessary categories. (See structure section above)
8. Remove spaces and punctuation from the cities.
9. Add a Column called "category" and type in either Conservation Education or Technical assistance to the corresponding assistance type. See above for reference.
10. Import table into ArcGIS Pro, name it FY??Q??_CountiesFromSPAM_SSPR
11. Run a Join Field from the Texas_Cities_WithCounties to your FY??Q??_CountiesFromSPAM_SSPR, transfering the county names. (This checks for cities that don't match.)
12. Figure out why they are not matching, see above for common reasons.
13. Once they are fixed and you can match all counties to your cities, you should now have 3 tables
    FY??Q??_CountiesFromBrad<br>
    FY??Q??_CountiesFromELMR<br>
    FY??Q??_CountiesFromSPAM_SSPR (now with counties to match your categories)<br>
14. Merge the FY??Q??_CountiesFromELMR and  FY??Q??_CountiesFromSPAM_SSPR, ensuring the the field names are the same for County Name and Category. Name it FY??Q??_CountiesFromUCF
15. Run Summary Statistics with the following parameters:<br>
    Input table: FY??Q??_CountiesFromUCF<br>
    Field: County Name   Statistics Type: Count<br>
    Case Field: Category, County Name
16. This will give you a table that gives County Names and count of each category, CE and TA
17. This next part is the most tedious. There might be a better way to do it, but this is the best I got for right now.
18. Create two new fields in the FY??Q??_CountiesFromUCF called Conservation_Education_NEW and Technical_Assistance_NEW
19. Calculate the conservation_education_NEW field to 0
20. Select only the counties with Conservation Education categories. 
21. Calculate conservation_education_NEW again under the selection setting it equal to conservation education category
22. Repeat steps 19-21 for Technical_Assistance_NEW
23. Join field from FY??Q??_CountiesFromUCF to FY??Q??_CountiesFromBrad, transfering the Technical_Assistance_NEW and Conservation_Education_NEW. Join by County Name
24. Create two new fields in FY??Q??_CountiesFromBrad called Conservation_Education_FINAL and Technical_Assistance_FINAL.
25. IMPORTANT STEP. Select the NULL values in the original CE,TE, the NEW CE, TA, and FINAL CE,TA to 0. (We will add them together and it doesn't like adding null values)
26. Calculate the FINAL CE, TA categories as original + NEW.
27. You now have all accomplishments by county and category. 

**For making the map**
1. Insert a new map
2. with any county shapefile, join field from FY??Q??_CountiesFromBrad to counties, transfering all 4 categories. (FIA, Management Plans, NEW TA, NEW CE)
3. Rename the shapefile FY??Q??
4. change symbology to dot density
5. Change the map frame in the layout to the new map
6. Print to PDF

Send Map, number of communities, and acres to Hughes



