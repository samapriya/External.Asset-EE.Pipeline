# External.Asset-EE.Pipeline-->>DG Only
This section is designed to support if you are only running DigitalGlobe imagery including Quickbird, GeoEye, WorldView-2 and WorldView-3 using associated metadata files. 

DigitalGlobe is an company that is currently running request based remote sensing data acquisiton and runs an array of high resolution satellites and its interest also include machine learning algorthms for object detection. The current DG system does not allow for a data download pipeline but this setup is for automated metadata parsing and asset uploading to Google Earth Engine. 

Google Earth Engine is a distributed computing based planetary remote sensing system which is build on a scalable architecture approach and allows for the processing and handling of data. GEE only hosts publicly available data and additional data can be added by the user using a storage quota. The system evolves and change log is maintained at GEE (https://earthengine.google.com/)

1) Digital Globe datasets are requests directly or via third party vendor along with additional IMD and XML files. The image must be converted to geotiff if they are not already standard geotiff.

3) The metadata file is sliced from the xml input files accompanying each asset into a csv file to be read along with asset/image id.

3) Take both the downloaded tiles and the batch ingestion manager created by Lucas (https://github.com/tracek/gee_asset_manager) and upload the imagery to Google Earth Engine (This is push function and requires google credentials)

The project will allow for the service to be a seamless pull, parse and push service(for Planet) and mostly (Parse & Push) for Digital Globe. The Pipeline serves as temporary storage upto a certain volume before a copy of the pull is pushed to both archival/long term storage and Earth Engine.

## Table of contents
* [Installation](#installation)
* [Prerequisites](#prerequisites)
* [Getting started](#getting-started)
    * [Parsing metadata and download](#parsing-metadata-and-download)
    * [BoxFTP Upload Assets](#boxftp-upload-assets)
* [Usage examples](#usage-examples)
    * [Downloading an aoi](#downloading-an-aoi)
    * [Upload assets to Box](#upload-assets-to-box)
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

## Getting started
The first step is to create the directories of interest. 
Create empty directories using the following
```
mkdir dgxml dg
```
 
## Parsing metadata and download
This toolset allows the user to use the aoi.json file to query, activate and download the assets of interest.The digital globe assets are acquired seperately and the metadata files for digital globe(xml are to be placed in the dgxml directory). 

## BoxFTP Upload Assets
If you have an enterprise Box account you can use this tool to directly upload them to a folder in your Box account. It uses the mirror function so it adds files from the local path to the remote path but does not delete existing remote files. This only works for Enterprise accounts since filesize limitation on box
personal accounts are 250MB.

## Usage Example
Once you have downloaded and placed map.geojson file into the JSON Parser folder
Migrate to folder first in Bash

```
./DG_distv2.sh.x

"Metadata will be emailed to you:This is the same email associated with Earth Engine account"
"Enter from email: You should have password for this account"
  abc@gmail.com

"Enter to email"
  def@gmail.com

"Enter password"
 password (Invisible Entry)

"Enter DigitalGlobe asset destination in GEE users users/username/path"
 users/abc/DigitalGlobe
 
 Asset upload is included into this script
 Do you want to upload to upload assets?(y/n)
 ```

## Upload assets to Box
The next step if the asset upload is selected is ftp upload onto Box. The ftp login is
```
ftps://ftp.box.com
port: 990
```
The script needs specific input from user

```
"Enter username"
Enter ftp username

"Enter password"
Enter ftp password (invisible entry)

"Enter Local Path"
This is the local path where PlanetScope or RapidEye data is stored
eg> /home/user/Downloads/PlanetScope

"Remote Path"
This is the remote path where PlanetScope,RapidEye or Digital Globe data is to be uploaded on ftp
for example: root folder can be /PlanetScope, /RapidEye, /DigitalGlobe and it will create those directiories
```

# Credits

[JetStream](https://jetstream-cloud.org/) A portion of the work is suported by JetStream Grant TG-GEO160014.

Also supported by [Planet Labs Ambassador Program](https://www.planet.com/markets/ambassador-signup/)
