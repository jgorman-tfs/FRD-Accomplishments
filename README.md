# FNRM-Accomplishments 
This repository contains information related to creating the FNRM Accomplishments Map and calcuating the UCF community stats.<br>

*Last updated 1-8-2026*
## Purpose
The FNRM Accomplishment Map is included in the FNRM Accomplishment Report that is written by Gretchen and sent to Al every quarter of the fiscal year. The map serves as a visualization of all the quarterly accomplishments. Other ancillary information is also collected and reported. 

The data from ELMR and Chris is straightforward and easy to put into a map because it's a list of counties with the assist count for each county under each category. The data from Urban and Community Forestry is less straightforward because it is just a list of cities and counties with the associated assist type. 

The FNRM_Accomplishments script automates everything from start to finish, but there are a few things that need to be in place before running through the script. 

You will need to download the Texas_Places_WithCounties and Template layers along with the Q5_2024 lyrx for symbology.
The Texas_Places_WithCounties layer has all Texas Places and the respective county they are in. This is important to match the UCF cities to the counties for accomplishments.
The Template layer is just a general county layer used to generate the final layer.

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

Steps before running through script:
1. Open the FIA Report From Chris.
2. Change the COUNTY CODE column to SHORT TEXT and convert to 3 character length. In excel, its =TEXT([CellReference], "000")
3. Open the FRD Quarterly Accomplishments Microsoft Access Database. If you do not have it, get with Brad Barber.
4. Import the FIA Data from Chris and overwrite the current one.
5. Open the FIA table and ensure it loaded correctly.
6. Input the year and quarter and click submit.
7. Save the excel file as CSV
8. Open the UCF SPAM Report
9. Create 2 sheets: spam_raw and elmr_raw
10. Copy the data from SPAM into rows City , Activity Name - delete the blank rows and totals so its just the city and activity rows
11. Open the ELMR spreadsheet and copy the City, Activity Name, and County into elmr_raw.
12. Make sure the Column titles are as shown above for each sheet

**Run through the FNRM_Accomplishments Script**

Send map and community acres count to Melissa/Gretchen




