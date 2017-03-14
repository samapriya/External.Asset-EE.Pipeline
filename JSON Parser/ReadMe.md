# JSON Parser
This allows you to structure the aoi.json files used to download assets.

Make sure your area of interest is licensed with your API Key
Select area of interest json using [geojson.io](geojson.io) and download as map.geojson

# Prerequities
It assumes you use Python2.7 hopefully >=2.7.12

The script needs specific input from user

```
./JSONParser.sh.x

"enter startdate"
This is start date for asset search (eg. 2016-01-01)

"enter enddate"
This is end date for asset search (eg. 2016-12-31)

"cloudcover"
Enter maximum cloudcover percentage(minimum is set to 0)

aoi.json file is created in the folder 

Copy and paste into "Asset Download Parse & GEE Upload"

