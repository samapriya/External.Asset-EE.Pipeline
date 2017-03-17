# External.Asset-EE.Pipeline (Windows Executable)
This project supports Planet assets such as PlanetScope and RapidEye imagery along with Digital globe assets including Quickbird, GeoEye, WorldView-2 and WorldView-3 using associated metadata files. For now the tool in windows has limited features compared to the unix implementation.

Planet Inc is a company that is currently trying to map the entire planet every single day and as the constellation size increases the data value and repeat cycle increases as well.(https://www.planet.com/) The planet labs API consists of searching for satellite imagery type assets using a structured geojson

DigitalGlobe is an company that is currently running request based remote sensing data acquisiton and runs an array of high resolution satellites and its interest also include machine learning algorthms for object detection. The current DG system does not allow for a data download pipeline but this setup is for automated metadata parsing and asset uploading to Google Earth Engine. 

Google Earth Engine is a distributed computing based planetary remote sensing system which is build on a scalable architecture approach and allows for the processing and handling of data. GEE only hosts publicly available data and additional data can be added by the user using a storage quota. The system evolves and change log is maintained at GEE (https://earthengine.google.com/)

1) Planet API is first used to define a bounding area and download the images to a storage can be Amazon S3 bucket/Google Cloud Storage Bucket of local or hosted storage held in volume. (This is pull function and requires API Key from Planet)

2) Digital Globe datasets are requests directly or via third party vendor along with additional IMD and XML files. The image must be converted to geotiff if they are not already standard geotiff.

3) The metadata file is sliced from the xml input files accompanying each asset into a csv file to be read along with asset/image id.

3) Take both the downloaded tiles and the batch ingestion manager created by Lucas (https://github.com/tracek/gee_asset_manager) and upload the imagery to Google Earth Engine (This is push function and requires google credentials)

The project will allow for the service to be a seamless pull, parse and push service(for Planet) and mostly (Parse & Push) for Digital Globe. The Pipeline serves as temporary storage upto a certain volume before a copy of the pull is pushed to both archival/long term storage and Earth Engine.

## Table of contents
* [Installation](#installation)
* [Prerequisites](#prerequisites)
* [Getting started](#getting-started)
    * [Parsing metadata and download](#parsing-metadata-and-download)
* [Usage examples](#usage-examples)
    * [Downloading an aoi](#downloading-an-aoi)
    * [TOA Radiance and TOA Reflectance Calculations](#toa-radiance-and-toa-reflectance-calculations)
* [Credits](#credits)

## Installation
For now the tools can only be run on a linux distribution and has been developed on Ubuntu 16 LTS. Download the respository along with all folders and navigate to folder for specific application


## Prerequisites
It assumes you use Python2.7 hopefully >=2.7.12

Install the following

  * sudo apt-get install ssmtp

  * sudo apt-get install sendemail libio-socket-ssl-perl libnet-ssleay-perl

  * sudo apt-get install zip
  
  * pip install planet, pandas
  
for Earth Engine (https://developers.google.com/earth-engine/python_install)

  * sudo pip install google-api-python-client

  * sudo pip install earthengine-api

  * type earthengine authenticate and a browser will open up asking you to login to google account(This should be the same gmail account
  used to send metadata email)

Copy the Key and paste back to bash

Your earthengine account is now active and linked to that account 

Create empty directories using the following
```
mkdir rexml psxml dgxml PlanetScope RapidEye dg
```

## Getting started

The first step is to define a area that is available for download under your Planet API license. 
 * Go to geojson.io and once you have defined your area of interest click on save as GeoJson(A map.geojson file is created)
 * Place the map.geojson file inside the JSON Parser folder
 
## Parsing metadata and download
This toolset allows the user to use the aoi.json file to query, activate and download the assets of interest. For now only PlanetScope analytic and RapidEye analytic are enabled for downloading of assets or metadata. The metadata for both planetscope and rapideye are downloaded into the psxml and rexml folders respectively. The digital globe assets are acquired seperately and the metadata files for digital globe(xml are to be placed in the dgxml directory). 

## Google Earth Engine Upload
This section allows the user to upload all the assets, including PlanetScope, RapidEye and Digital Globe assets to Earth Engine, you will need to provide password for the GEE account during upload.

## Usage Example
Place the aoi.json file in the folder after restructuring

## Downloading an aoi

#### Modify _download.py_ files
Edit the line with your Planet API Key and save 

```
os.environ['PLANET_API_KEY']="Enter Your Planet Key Here"
```

## TOA Radiance and TOA Reflectance Calculations
Multiply by radiometricScaleFactor to convert DNs to TOA Radiance (watts per steradian per square metre)

Multiply by reflectanceCoefficient to convert DNs to TOA Reflectance

Migrate to folder first in Bash

```
run Windows_AssetPipeline.exe

"Enter wait time for asset activation"
  200

"This is the same email associated with Earth Engine account"
"Enter from email: You should have password for this account"
  abc@gmail.com

"Enter PlanetScope asset destination in GEE users users/username/path"
  users/abc/PlanetScope

"Enter RapidEye asset destination in GEE users users/username/path"
  users/abc/RapidEye
  
"Enter DigitalGlobe asset destination in GEE users users/username/path"
 users/abc/DigitalGlobe

 "Prompt start upload to GEE and asks for user password related to GEE account"
 "password will be asked"(Invisible Entry)
 ```

# Credits

[JetStream](https://jetstream-cloud.org/) A portion of the work is suported by JetStream Grant TG-GEO160014.

Also supported by [Planet Labs Ambassador Program](https://www.planet.com/markets/ambassador-signup/)
