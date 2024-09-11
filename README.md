# FRD-Accomplishments 
This repository contains information related to creating the FRD Accomplishments Map and calcuating the UCF community stats.<br>

*Last updated 9-11-24*
## Purpose
The FRD Accomplishment Map is included in the FRD Accomplishment Report that is written by Hughes and sent to Al every quarter of the fiscal year. The map serves as a visualization of all the quarterly accomplishments. Other ancillary information is also collected and reported to Hughes and Gretchen. 
## Key Components
Primary data is collected from Mac, Chris, and ELMR. Brad Barber wrote the SQL in Microsoft Access to get the ELMR data. Mac send the Urban and Community Forestry report and Chris sends the FIA report. 
Seconday data includes County Boundaries, City Boundaries, and U.S. Census Bureau Places (Texas) 
Texas_PlacesWithCounties is an important feature because it contains a field for County each Place is in. 

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

ELMR's report already has information in this format <br>
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

## Methodology for the UCF Community Stats

**Clean the UCF Report for Getting the UCF Community Stats**
 1. Copy all CITIES and type of assistance from SPAM and SSPR into one sheet..
 2. Copy all OFFICE locations and types of assistance from ELMR into the same sheet, right below the others. (This is because ELMR shows assists by county, not city. So were substituting the office city as a "community").
 3. Create a table and filter the categories to show only the needed categories (see above)
 4. Copy fitlered data into a new sheet and create a new table. (This is to preserve data along the way in case you need to go back)
 5. In the cities column, replace all "City of, Village of, CDP of, etc so you only have the city name.
 6. Remove all spaces and punctuation. (This is to match the data in the City shapefile. If you are using you're own city shapefile, remove all the spaces. This makes all the names the same and prevents join errors.)
 7. Remove duplicates to you only have unique cities in your column. (I find it better to highlight and manually delete them. This lets me comb through and check for misspellings and get a better look at the cities.
 8. Use your own judgement when you delete cities and duplicates. For example, you may see Austin and Austin South. Just keep one Austin.
 9. You now have a PRELININARY list of all the unique cities for this Quarter that si ready to be put in the UCF Community Processor script. Take note of what you call your final sheet for all unique communities.

**Run through the UCT_CommunityProcessor script**
You MUST have a layer loaded in the map that has Texas Places with a field containing the county for each place. Change the first cell block to update the paths to your files. 

**Keep track of the community stats**
A new field is added to the Texas_Places_WithCounties Layer for the acres of each community. You can select the non-null communities and export to keep track of them. 

## Methodology for Accomplishments 

**Getting the ELMR Data**

1. Open the FIA Report From Chris.
2. Change the COUNTY CODE column to SHORT TEXT and convert to 3 character length. In excel, its =A1(TEXT, "000")
3. Open the FRD Quarterly Accomplishments Microsoft Access Database. If you do not have it, get with Brad Barber.
4. Import the FIA Data from Chris and overwrite the current one.
5. Open the FIA table and ensure it loaded correctly.
6. Input the year and quarter and click submit.
7. Save the excel file as CSV

**Clean the UCF Report for Accomplishments**

These initial steps are similar to the first cleaning, but there are a couple key differences. You will not remove duplicate values and you will not copy the cities from ELMR. (This is because ELMR already records the county.)

2. Copy the ELMR Counties and types of assistance into a new sheet and insert into a table.
3. Filter the table, keeping only the NECCESSARY CATEGORIES. (See structure section above).
6. Copy the Cities and Types of Assistance from SPAM and SSPR into a sepeate sheet and insert to table.
7. Filter the table, keeping only the neccessary categories. (See structure section above)
8. Remove spaces and punctuation from the cities.
9. Add a Column called "category" and type in either Conservation Education or Technical assistance to the corresponding assistance type. See above for reference.

**Run through the FRD Accomplishments Script**

You MUST have a Texas County Layer loaded in the map. This is a template and will be copied to make the final layer for dot density. You should only need to alter the first cell to update the paths to your files. 

**For making the map**

Change symbology to Dot Density

Send Map, number of communities, and acres to Hughes, Gretchen, and Rebekah



