# RODEO WP6: OPERA Open Radar Data Sharing Requirements

### Annakaisa v. Lerber, Stuart J. Matthews, Roope Tervo, Gijsbert Kruithof, Mikko Rauhala, Vegar Kristiansen, DMI (Morten?), Vera Meyer, Christoph Müller, Daniel Heintze, Steffen Kremer 
.


## Abstract

This is the Requirements Document for the the RODEO WP6 for sharing weather radar data. This document outlines the technical requirements and objectives for the development of radar data supply, which utilizes components developed in the the EUMETNET Federated European Meteorological Data Infrastructure (FEMDI) programme. The objective of work in WP6 is utilize the data sharing done in the EUMETNET OPERA programme already over a decade and, build on this collaboration a data supply for the third-party users in line with the World Meteorological Organization’s (WMO) Information System 2.0 (WIS 2.0) strategy and the European Union’s (EU) regulation on Meteorological High Value Data (HVD).

## Revision history
| Version | Date | Comment | Responsible
| :--- | :--- | :--- | :--- 
| 0.1 | 2024-01-14 | preliminary draft | Annakaisa v. Lerber
| 0.2 | 2024-02-09 | added dataset description, user requirements for review | Annakaisa v. Lerber
| | | |
| | | |


## Table of Content
- [Introduction](#Introduction)
- [Dataset description](#Dataset_description)
- [User requirements](#User_requirements)
- [System requirements](#System_requirements)
- [Functional and non-functional requirements](#Functional_and_non-functional_requirements)
- [Business requirements](#Business_requirements)
- [Dependencies](#Dependencies)
- [Constraints and assumptions](#Constraints_and_assumptions)
- [Risks](#Risks)
- [Conclusions](#Conclusions)

## Introduction
This is the Requirements Document for the RODEO WP6 for sharing weather radar data. This document outlines the technical requirements and objectives for the development of radar data supply, which utilizes components developed in the the EUMETNET Federated European Meteorological Data Infrastructure (FEMDI) programme. The objective of work in WP6 is utilize the data sharing done in the EUMETNET OPERA programme already over a decase and, build on this collaboration a data supply for the third-party users in line with the World Meteorological Organization’s (WMO) Information System 2.0 (WIS 2.0) strategy and the European Union’s (EU) regulation on Meteorological High Value Data (HVD).

This document is intended for the development team, stakeholders, and anyone interested in the technical specifications of WP6 weather radar data supply. It includes a detailed description of the system’s functional and non-functional requirements, acceptance criteria, and risks.

We hope that this document will serve as a clear guide for the development and implementation of work performed in WP6 for radar data supply and help ensure its successful integration with the FEMDI programme and within RODEO-project.

## Dataset description

In this section we describe the datasets that are planned to be supplied by the RODEO developed APIs. In short, these are stated in the Table 1. 


Table 1. Weather radar datasets in WP6 for supplying in RODEO 
| N | Data type | Spatial coverage | Temporal coverage | Timeliness |Availability| Data Owner/licensing | Period | Data model and format | Metadata standard | More Info
| :--- | :--- | :--- | :--- | :--- |:---| :--- |:--- | :--- | :--- | :---
| D01a| OPERA Composite: ODYSSEY maximum reflectivity  | 2 x 2 km, Cartesian grid covering the whole of Europe (area 3800 × 4400 km2) | every 15 minutes | delivery in (&#124;T2 – T1&#124; ≤ 1020 s) > 90 % |(&#124;T2 – T1&#124; ≤ 1800 s) > 99 % | EUMETNET | 2011 -  | ODIM (BUFR and HDF5) | ODIM |
| D01b| OPERA Composite: CIRRUS maximum reflectivity  | 1 x 1 km, Cartesian grid covering the whole of Europe (area 3800 × 4400 km2) | every 5 minutes | delivery (&#124;T2 – T1&#124; ≤ 420 s) > 90 % | (&#124;T2 – T1&#124; ≤ 600 s) > 99 % | EUMETNET | 01/2024 - | ODIM 2.4 HDF5 | ODIM |
| D01c| OPERA Composite: ODYSSEY Surface rain rate | 2 x 2 km, Cartesian grid covering the whole of Europe (area 3800 × 4400 km2)   | every 15 minutes | delivery in (&#124;T2 – T1&#124; ≤ 1020 s) > 90 % |(&#124;T2 – T1&#124; ≤ 1800 s) > 99 % | EUMETNET | 2011 -  | ODIM (BUFR and HDF5) | ODIM |
| D01d| OPERA Composite: NIMBUS Surface rain rate | 2 x 2 km,Cartesian grid covering the whole of Europe (area 3800 × 4400 km2)   | every 15 minutes | delivery in (&#124;T2 – T1&#124; ≤ 1020 s) > 90 % |(&#124;T2 – T1&#124; ≤ 1800 s) > 99 % | EUMETNET | 04/2024 -  | ODIM 2.4 HDF5) | ODIM |
| D01e| OPERA Composite: ODYSSEY 1 hour accumulation | 2 x 2 km,Cartesian grid covering the whole of Europe (area 3800 × 4400 km2) | hourly | delivery in (&#124;T2 – T1&#124; ≤ 1020 s) > 90 % |(&#124;T2 – T1&#124; ≤ 1800 s) > 99 % | EUMETNET | 2011 -  | ODIM (BUFR and HDF5) | ODIM |
| D01f| OPERA Composite: NIMBUS 1 hour accumulation | 2 x 2 km Cartesian grid covering the whole of Europe (area 3800 × 4400 km2)  |hourly | delivery in (&#124;T2 – T1&#124; ≤ 1020 s) > 90 % |(&#124;T2 – T1&#124; ≤ 1800 s) > 99 % | EUMETNET | 04/2024 -  | ODIM 2.4 HDF5 | ODIM |
| D02a| OPERA volume radar data: DBZH (filtered, "best possible" horirizontal reflectivty factor), TH (unfiltered horizontal reflectivity factor), VRADH (horizontal radial velocity)  | resolution varies 125 m - 1000 m covering 150 -300 km  | 5-15 minutes| >= 0 to < 5 minutes after the nominal time| >= 95%  | Data provider | 2011 - | ODIM (BUFR and HDF5)| ODIM |
| D02b| OPERA volume radar data: new variables  | resolution  125 m - 1000 m covering 150 -300 km  | 5-15 minutes| >= 0 to < 5 minutes after the nominal time| >= 95%  | Data provider | 2026 - | ODIM HDF5 or FM301 NetCdf| ODIM, FM301 |
| D03a | National products: reflectivity composite | resolution  125 m - 1000 m | 1-15 minutes | varies | varies| Data provider|  | varies ODIM HDF5, GeoTiff | |
| D03b | National products: precipitation composite  | resolution  125 m - 1000 m | 1-15 minutes | varies | varies| Data provider|  | varies ODIM HDF5, GeoTiff | |
| D03c | National products: wind profiles  | n/a | 1-15 minutes | varies | varies| Data provider|  | BUFR | |
| D03d | National products: echo top  | resolution  125 m - 1000 m | 1-15 minutes | varies | varies | Data provider|  |varies GeoTiff | |

### OPERA Composite Data D01

The composites cover the whole of Europe (area: 3,800 × 4,400 km2) in a Lambert Equal Area projection with appox. corner coordinates: 70 N 30 W, 70N 50E, 32N 15W, 32 N 30E. In ODYSSEY production (D01a, D01c, D01e) covering years of 2011- 2023, the composites are all updated every 15 minutes, and issued ca. 15 minutes after data time with 2 x 2 km resolution. In the new production (2024 - ) the CIRRUS products are with higher spatial resolution of 1 x 1 km and update cycle of 5 minutes. The composite products are based on incoming polar scans and volumes of filtered reflecitvity. 

Four quality filters are applied to the volume data prior to compositing. Two methods were initially utilized since 2011: an anomaly-removal module and a hit-accumulation filter. The anomaly-removal module utilizes computer vision techniques to detect patterns often associated with non-weather-related sources, such as straight lines or single pixels. It assigns a probability of precipitation to the data as an initial quality indicator and discards non-precipitation pixels by setting values exceeding a threshold to nodata. 

The hit-accumulation clutter filter calculates a normalized echo count (or occurrence frequency) monthly. Pixels with a normalized echo count exceeding a threshold in each radar scan are identified as residual clutter, typically set at 0.6.

In late 2015, two additional methods were introduced: Beam blockage correction and a satellite-based filter for residual non-precipitation echoes. Beam blockage correction involves calculating beam blockage percentage in polar coordinates using a 1 km digital elevation model (GTOPO30) and a geometric propagation model. Pre-calculated values are then used to adjust reflectivity, with values in partially blocked sectors corrected and given less weight in composite products. Reflectivity values in sectors with blockage exceeding 70% are set to nodata.

The satellite filter is based on the EUMETSAT Nowcasting SAF Precipitating Clouds product, which provides a probability of precipitation. The filter considers the 49 surrounding satellite pixels for each radar pixel with a detected echo, accounting for time gaps between radar and satellite observations and parallax effects. The maximum probability serves as the third quality index, and if the probability of precipitation is 0, the reflectivity is marked as undetectable.

The used data sharing model in OPERA is in-house deveoped ODIM (OPERA Data Information Model) both in BUFR and HDF5 for older production, solely HDF5 for the new production. 
- Metadata description (Missing!)

There are three products on offer from the OPERA suite of products:
 
#### OPERA Instantaneous Maximum Reflectivity (in dBz) (D01a, D01b)
- In the maximum reflectivity composite each composite pixel contains the maximum of all polar cell values of the contributing radars at that location.
- ODYSSEY production 2012-2023 and CIRRUS production 2024 -

  
#### Instantaneous Surface Rain rate composite (in mm/h) (D01c, D01d)
- ODYSSEY production 2012-2023 and NIMBUS production 2024 -
- In the ODYSSEY rain rate composite, each composite pixel is a weighted average of the valid pixels of the contributing radars, weighted by a quality index, the distance from center of the pixel and an exponential index related to inverse of the beam altitude. Whereas in NIMBUS production the compositing algorithm is based on the lowest elevation angle only.
- Measured reflectivity values are converted to rainfall (mm/h) using the Marshall-Palmer equation.

#### OPERA One Hour rainfall Accumulation (in mm) (D01e, D01f)
- Rainfall accumulation is the sum of the previous four 15-minute rain-rate products.
- ODYSSEY production 2012-2023 and NIMBUS production 2024 -

### OPERA Database

OPERA Database is manually maintained table by the OPERA data providers and by the Croatian Met Services. It is sporadically updated, minimum twice a year. The available formats are json, xlsx and csv and it can be automatically pushed to service. The fields it includes are stated in the Table 2. 

Table 2. OPERA database contents
| Field | Unit/Format | Description | Example 
| :--- | :--- | :--- | :--- 
| Number | 1111 | Internal identifier of radar in database | 1218
| Country | x | Country | Croatia
| Country ID | CCCCii | Country ID |LDZM42
| Old Country ID | AA11Old | Country ID | (optional)RH42
| WMO Code | 11111 | WMO Code| 14256
| WIGOS Station Identifier | | WIGOS Station Identifier |
| ODIM Code |aaaaa | ODIM Code | hrbil| 
| Location | x | Name of location | Bilogora
| OPERA Status | 0 / 1 | OPERA active or inactive | 1 
| Latitude | 1.2345° | Latitude of radar (WGS84) | 45.8834
| Longitude |1.2345° | Longitude of radar (WGS84) |17.2008
| Height of Station | 1 m | Height of radar station | 258
| Band | S/C/X | S, C or X band radar |S 
| Doppler | Y/N | | Y
| Polarization | S/D |Single or dual polarization| S 
| Max Range | 1 km | Maximum range of radar (lowest elevation) | 240
| Start Year |YYYY | Year when the radar site first was taken into use | 1994
| Year of the most recent upgrade | YYYY | Year of the most recent upgrade | 
| Height Antenna | 1 m | Height of radar antenna + height of radar station | 275
| Antenna Diameter | 1.2 m | Antenna diameter | 3.7 
| Beam | 1.23° | Beam width | 2.1
| Gain | 1.2 dB | Antenna gain | 38.5
| Frequency | 1.234 GHz | Frequency | 2.800
  
### National volume radar data (D02a, D02b)
- DBZH, TH, VRADH
- can be sent as volumes, or scan-by-scan, radar variables can be in the same file or seprately
- two types of scans, reflectivity or velocity - optimized
- in VRADH aliasing is not always performed.
- ODIM Data format model vr. 2-2.4 not always reverse compatible
- archive in different national BUFR version, there are some manual how to encode these
- the newer files in HDF
- various national scanning strategies, definitions of scanning time, spatial and temporal resolution.
- different quality processing levels 

OPERA - CUMULUS incoming data:

EDZW: 145000 Files/d 13.5 GB/d

LFPW: 40000 Files/d 2G B/d

ESWI: 30000 Files/d 2.5 GB/d

EFKL: 17000 Files/d 1.5 GB/d

EKMI: 1200 Files/d 1.5 GB/d

BIRK: 1500 Files/d 850 MB/d

LEMM: 3500 Files/d 500 MB/d

LPMG: 15000 Files/d 800MB/d

LYMB: 300 Files/d 70 MB/d

LZIB: 3400 Files/D 1.4 GB/d

LDZM: 1000 Files/d 600 MB/d

LSSW: 6400 Files/d 750 MB/d

ENMI: 7000 Files/d 5.5 GB/d

OKPR: 1700 Files/d 500MB/d

EBUM: 7700 Files/d 2 GB/d

EGRR: 36000 Files/d 3.5 GB/d

HABP: 5000 Files/d 1 GB/d

YRBK: 750 Files/d 150 MB/d

EIDB: 4700 Files/d 170 MB/d

SOWR: 5500 Files/d 1.1 GB/d

LJLM: 570 Files/d 280 MB/d

EVRR: 140 Files/d 40 MB/d

LLBD: 280 Files/d 2.5 GB/d

LGAT: 300 Files/d 65 MB/d

Summary : ca. 340000 Files/d with ca. 45GB/d

Data Format:
Info to ODIM Format (V2.3) located here:
https://www.eumetnet.eu/wp-content/uploads/2019/01/ODIM_H5_v23.pdf

Used metadata in DWD:

	Metadata set definition: 
 
 General information:
 
		Metadata field: REFERENCE_DATE (d), type Date
  
		Metadata field: COUNTRY (ctry), type String
  
		Metadata field: COUNTRY_ID (ctryid), type String
  
		Metadata field: STATION_NUMBER (stno), type Integer
  
		Metadata field: STATION_LOCAL_ID (stid), type String
  
		Metadata field: QUANTITY (quant), type String
  
		Metadata field: FILENAME (fn), type String
  
		Metadata field: ANTENNA_ELEVATION (ae), type Float
  
		Metadata field: WAVELENGTH (wl), type Float
  
		Metadata field: LATITUDE (lat), type Float
  
		Metadata field: LONGITUDE (long), type Float
  
		Metadata field: HEIGHT (h), type Float

Special information:

		Metadata field: PROD_IDA1 (pida1), type String
  
		Metadata field: PROD_IDA2 (pida2), type String
  
		Metadata field: FILE_FORMAT (ff), type String
  
		Metadata field: FILE_MODE (fm), type String
  
		Metadata field: FORMAT_VERSION (fv), type String
  
		Metadata field: DECODE_DATE (dedat), type Date
  
		Metadata field: STORE_DATE (stdat), type Date

#### National composites or products (D3a-d)
 - formats?
 - temporal and spatial resolution
 - included metadata

**FMI national products D3**
FMI could demonstrate the RODEO interface with D3a (reflectivity composite), D3b (precipitation composites), and D3d (echo top):
1. Radar reflectivity factor in dBZ.
2. Rainfall intensity R, in units of mm/h and 1, 12, and 24-hour rainfall accumulation (mm).
Products for variables 1 and 2 are available with a 5-minute time resolution. Composite products are displayed in a Cartesian coordinate system with a 1 km resolution in GeoTIFF format.
In addition to the aforementioned products, FMI national suite has Echo top - product (etop_20), which represents the maximum height of strong or moderate echoes at each point. Its height unit is presented in kilometers and spatial resolution is same as with composites  with a 1 km resolution and offered format is GeoTIFF.

All data and resulting data products have undergone signal processing stages where:
* Stationary objects have been removed using ground clutter filtering.
* Weakest signals have been thresholded to prevent radar system-induced thermal noise from interfering with measurement data.
* Strongest ground clutter signals have been thresholded to ensure that the ratio between ground clutter signal and weather signal does not exceed a set radar-specific threshold.

In addition to these, the following post-processing steps have been applied to the radar compositing data:
* Distance correction derived from the rain vertical distribution to transform measurements made higher in the atmosphere to surface-level measurements.
* Removal of non-meteorological echoes.
* Transformation of radar reflectivity factor depending on precipitation type to rainfall intensity.




## User requirements

Description of use cases. Three of the use cases are stated also in the FEMDI documentation and four are related to E-SOH requirements. These are stated at each use case. The short descriptions of the use cases specified in the Table 2. aligned with teh datasets they are utilizing. 

Table 2. User requirements in short 
| User requirement | Description | D01 real-time OPERA composites | D01 archived OPERA composites| D02 real-time OPERA volume data  | D02 archived volume data | D03 real-time National products | More Info 
| :--- | :--- | :--- | :--- | :--- |:---| :--- |:--- | 
| U01 | Development of AI |  | X |  | X | | requires large amount of dat, but not with prioritized access| 


### U01 A company or public institute, where a data scientist who wants to use radar data in their machine learning model (training and operational) environment. 

Related to use cases in FEMDI 2.4.

“As a big data consumer, I want a single unified view of available meteorological datasets in machine-readable formats and large-scale data usage / re-processing, dataset needed for training a Machine Learning (ML) model and then running it. This innovative use of met data, will help bring step-change advances to technological solutions for understanding and forecasting the weather and its impacts events.”  

*Requirements:* 

- Requires either composite data or volume radar data
- Needs as long a history of data as possible, the big archive
- Needs a suitable access mechanism for bulk consumption (rather than download), e.g. through S3 in cloud native formats, to download directly, so no need to download, store, etc.
- Corresponding real-time data to drive the models?
- The real-time data for execution needs to be consistent with the data used for model training (i.e., from the same source) 

*Priority:* 
- secondary

*Clarifications:* 

*Acceptance criteria:* 

*Consequences and decisions:* 

### U02 A Small & Medium Enterprise (SME) application developer who wants to see what data sets are available and access them. 

Related to use cases in FEMDI 2.5 and E-SOH 4.3.

“As a new data consumer, I want a single unified view of available meteorological datasets which are updated on a regular basis, that is easily accessible and findable, is easily integrated into my systems and can be re-used (i.e., following FAIR principles). This will allow me to develop an application which makes best use of the available data to add value to the users and bring me in an income.”  

*Requirements:* 
- based on mainly composite data
- e.g. aviation application would like to have 3D- volume data
- A software developer builds a mobile application that needs ....
- They identify a dataset via the FEMDI Shared Catalogue and determine that the API for that dataset is suitable for the application.
- The mobile application quickly becomes popular and is installed on over 10,000 devices. Each device makes a few requests a day as the user changes location, and this adds up to lots of requests on the Data Supply component’s API. 

*Priority:*  

*Clarifications:* 

- Can lead to a lot of requests and processing on the data source. 

*Acceptance criteria:* 

*Consequences and decisions:* 

### U03 A member of a public organisation who wants to see real time weather radar visualised on their mobile.  

Related to use cases in FEMDI 2.6 and E-SOH 4.4, and 4.5
“As a traffic officer manager, I want to use my smart phone to regularly check the rainfall amounts across my country and bordering countries in Europe, so I can be prepared for different driving conditions, and potential impacts on the traffic network and people’s safety. This will allow me to rapidly respond with appropriate resources and equipment to incidents.”   
*Requirements:* 
- most likely composite data
 
*Priority:* 

*Clarifications:* 
- Visualisation is out of scope of FEMDI – another will provide the visualisation
- OPERA is EUMETNET’s radar programme; Also RODEO WP6.
- Potential additional use case to be considered 

*Acceptance criteria:* 

*Consequences and decisions:* 

### U04 - EUMETNET Members uses RODEO for data exchange

“EUMETNET members want to replace the bilateral data exchange with RODEO. They want the 3D-volume data as fast as possible, high priority user. They are familiar with the data formats and the radar data processing. They will build their national forecasting services on this data.”  

*Requirements:*
- 3D-volume radar data
- automized fetching of data from an interface
- 24 hour cache is suitable, doesn't require the large archive 

*Priority:*
- primary

*Clarifications:*

*Acceptance criteria:*

*Consequences and decisions:*

### U05 EUMETNET members are visualising OPERA products in the forecasting services

“EUMETNET members want to show the composite products on their forecasting services for official duty purposes. They want the composite data as fast as possible, high priority user. They are familiar with the data formats and the radar data processing. ”  

*Requirements:*
- basically they do receive this also directly through OPERA. Do we need this user case?
- composite data
- automized fetching of data from an interface

*Priority:*
- primary

*Clarifications:*

*Acceptance criteria:*

*Consequences and decisions:*


### U06 - National Met Service is supplying their national radar products (composites, echo tops, vertical wind profiles) to third party users 

“As a EU members I have to fulfill the HVD Implementation Act, and RODEO provides a common interface which is also good for the third-party users to obtain radar data products from the same interface. This user requirement is following the federated distribution of data.”  

*Requirements:*
- radar data products
- Should we state requirements for the product format/model, spatial and temporal distribution
- federated distribution, no archive, but should there be 24 hour cache or similar
- what is the SLA we promise here as it is nationally dependent.

*Priority:*

*Clarifications:*

*Acceptance criteria:*

*Consequences and decisions:*


### U07 - radar data observations from 3rd parties

Related to E-SOH requirement 4.5.

“I'm representative of e.g. hydrological services or a private company and I own radar data. I would like to include my radar data to the RODEO, e.g. MeteoPress”  

*Requirements:*

*Priority:*

*Clarifications:*

*Acceptance criteria:*

*Consequences and decisions:*

## System requirements
Is this separate from functional and non functional requirements?
Where to write SLAs of OPERA?

## Functional and non-functional requirements

These are copied from E-SOH directly, no changes!

### F01 - operational service

"As an E-SOH data consumer, I want E-SOH to be an operational service. So I can build my operational services based on E-SOH data."

*Priority:*
- primary

*Clarifications:*
- What is the meaning of "operational service"?
- E-SOH will be a fully operational service, providing core capability on behalf of EUMETNET Members. Requirements F02 to F06 describe the Service levels required. 

*Acceptance criteria:*

*Consequences and decisions:*

### F02 - 24/7 availability

"As a E-SOH data consumer,I want the service to be available 24/7 with minimal agreed downtime and maintenance slots. So, I can deliver the level of service required by my users."

*Priority:*
- primary

*Clarifications:*
- There is an expectation for data to be consistently available 24/7, although a minimum of downtime (<1%) is acceptable with no break in service > 24hours. There is also an expectation that to deliver this level of service a "service desk" capability will be required so incidents can be managed.
- We need to figure out the consequences of any downtime
- We need to separate between ingestion and data access downtimes
- Centralized and federated components also need to be viewed individually

*Acceptance criteria:*

*Consequences and decisions:*

### F03 - delivery within 1 minute

"As an E-SOH sub-hourly observations data consumer, I want observations to be available within 1 minute of data producer publishing their data. So, I can deliver the level of service required by my users."

*Priority:*
 - primary

*Clarifications:*

*Acceptance criteria:*

*Consequences and decisions:*

### F04 - file delivered within a minute of the youngest observation within the file

"As a E-SOH sub-hourly observations data consumer, when receiving batched observations within a file, I want the file delivered within a minute of the youngest observation within the file. So, I can deliver the level of service required by my users."

*Priority:*
- primary

*Clarifications:*
- Depending on who makes the batched file, this is a requirement on the data producer? Yes, but also on the system throughput - it needs to be fast

*Acceptance criteria:*

*Consequences and decisions:*

### F05 - data producers to make the data they create available with minimum delay

"As the E-SOH system manager, I want data producers to make the data they create available with minimum delay. So, I can deliver the level of service required by my users."

*Priority:*
- primary

*Clarifications:*
- Consequential requirement on E-SOH is to make an "easy-to-use" ingestion interface and high quality user guidance and documentation
- Ideally, the data producers should be able to reuse their existing capabilities

*Acceptance criteria:*

*Consequences and decisions:*

### F06 - agreed delivery data format and protocol

"As the E-SOH system manager, I want data producers to make the data they create available in an agreed data format and following an agreed delivery protocol. So, I can deliver the level of service required by my users."

*Priority:*
- primary

*Clarifications:*
- Does this refer to E-SOH ingestion service, or E-SOH API? It's the ingestion. From the ITT: "As well as requirements for the data provider (i.e., E-SOH) to meet, there are also requirements for the data producers (e.g., Members) ... to deliver the overall E-SOH service. "

*Acceptance criteria:*

*Consequences and decisions*:

### F07 - reports of the performance against agreed KPIs

"As a EUMETNET Member, I want monthly, quarterly, and annual reports of the performance, against (to be confirmed) agreed KPIs, of the E-SOH service. So, I am assured that the level of service is at agreed levels and meeting our users’ requirements. Also, so I have an indication of possible future investment needs."

*Priority:*
- primary

*Clarifications:*

*Acceptance criteria:*

*Consequences and decisions:*

### F08 - data application providers to only provide supported operating systems, libraries, and software

"As the E-SOH system manager, I want data application providers to only provide supported operating systems, libraries, and software. So, I can minimise the costs of managing the lifecycle of E-SOH."

*Priority:*
 - primary

*Clarifications:*
- The spirit of this requirement was to avoid any "exotic" or developer favourites being used. The requirement should be covered by the quality assurance process.

*Acceptance criteria:*

*Consequences and decisions:*

### F09 - access to real-time observations up to 24 hours after the observations data time

"As a data consumer, I want access to real-time observations, up to 24 hours after the observations data time. So, I can retrieve data I might have missed due to, for example, local technical incidents."

*Priority:*
- primary

*Clarifications:*
- Data consumers might choose to archive data themselves. This is common amongst Members as it, for example, allows Members to run re-analysis trials based on the data reception, rather than validity, time.

*Acceptance criteria:*

*Consequences and decisions:*

### F10 - access to the first iteration as well as corrected observations data

"As a data consumer of file-based E-SOH products, I want access to the first iteration of the observations data, as well as to late or subsequently corrected observations. So, I am able to handle all data."

*Priority:*
- secondary

*Clarifications:*
- Should E-SOH always return the last known value for an observation? Yes, only the latest iteration needs to be accessible
- By late or subsequently corrected observations, we interpret that observations that are corrected within the 24 hours window shall be exposed and pushed to the notification queue
- By "access to first iteration (..) as well as (..) corrected observations" we suggest to only keep the latest value in the 24 hours data store

*Acceptance criteria:*

*Consequences and decisions:*

### F11 - E-SOH as data provider role within FEMDI when data is exposed by producer via a pull API service

"Given a data producer exposes data via a pull API service, when new data are published by the data producer, then E-SOH must perform its data provider role within FEMDI."

*Priority:*
- primary

*Clarifications:*

*Acceptance criteria:*

*Consequences and decisions:*

### F12 - E-SOH as data provider role within FEMDI when data is exposed by producer via a push API service

"Given a data producer exposes data via a push service,when new data are received by E-SOH, then E-SOH must perform its data provider role within FEMDI."

*Priority:*
- primary

*Clarifications:*

*Acceptance criteria:*

*Consequences and decisions:*

### F13 - initially collect data before making it available to E-SOH

"Given a data producer operates or is responsible for multiple (>1) instruments, when those instruments make an observation, then the data producer initially collects the data before making them available to E-SOH."

*Priority:*
- primary

*Clarifications:*
- This requirement is here to highlight that the responsibility for the observation networks and initial collection of observations is with the members, and not the E-SOH project.
- So need to send multiple instruments for a station together, but stations can be sent separately?
- Given that the expected workflow for data producers is
  1) collect observations from station
  2) quality control/post-process(?)
  3) send to e-soh
 - it seems that we should support observations from each instrument on each station to be sent separately to e-soh.
 - A clear dataset definition may also be useful in this context

*Acceptance criteria:*

*Consequences and decisions:*

### F14 - sub-hourly observations from all operational land surface stations operated by EUMETNET Members

"As a current, or new, data consumer of land surface observations, I want access to sub-hourly observations from all operational land surface stations (approximately 5,000) operated by EUMETNET Members. So, I can improve the services (including forecasting of fog and convective events) I provide to my users."

*Priority:*
- primary

*Clarifications:*

*Acceptance criteria:*

*Consequences and decisions:*

### F15 - E-SOH must perform its data provider role within FEMDI when a data producer exposes data in an approved format

"Given a data producer exposes data in an approved format, when new data are received by E-SOH, then E-SOH must perform its data provider roll within FEMDI."

*Priority:*
- primary

*Clarifications:*
- There is likely to be variability in the format of "supplementary" observations produced by Members. There is a desire for E-SOH to be as flexible as possible when consuming data, but there is also an expectation that data producers provide data in a consistent and easily interpretable format.

*Acceptance criteria:*

*Consequences and decisions:*

### F16 - data quality above an agreed level or to be clearly indicated

"As a current, or new, data consumer of land surface observations, I want the data I receive to be above an agreed quality, or for the quality of the data to be clearly indicated. So, I can improve the services (including forecasting of fog and convective events) I provide to my users."

*Priority:*
- primary

*Clarifications:*
- There is no expectation for E-SOH to provide any data quality control capability. If data are received in a corrupt format, the data should be rejected, and no attempt should be made to recover the data. If, however, "poor" quality observations are provided to E-SOH, then E-SOH will publish the data as received. Where there are quality indicators provided by the data provider, these should be persisted and exposed to E-SOH data consumers.
- Future iterations of E-SOH, e.g., incorporating PWS data, will increase the need for EUMETNET, rather than relying on the data producer, to undertake real-time QC. This QC capability, possibly using machine learning techniques, falls outside of the current scope of E-SOH and will therefore need to be built separate too, but incorporate with, E-SOH.
- Will there be unified QC flagging scheme or is the "quality indicators persisted and exposed" also saying that there might be as many as flagging schemes as there are data providers? 

*Acceptance criteria:*

*Consequences and decisions*
- Conclusion: we will need some quality indicators

### F17 - reject corrupt data and record the event

"Given a data producer exposes data to E-SOH, when the data format is found to be corrupt. Then E-SOH should reject the data and record the event."

*Priority:*
 - primary

*Clarifications:*
 - There is no expectation for E-SOH to provide any data quality control capability. If data are received in a corrupt format, the data should be rejected, and no attempt should be made to recover the data. If, however, "poor" quality observations are provided to E-SOH, then E-SOH will publish the data as received. Where there are quality indicators provided by the data provider, these should be persisted and exposed to E-SOH data consumers.
 - Future iterations of E-SOH, e.g., incorporating PWS data, will increase the need for EUMETNET, rather than relying on the data producer, to undertake real-time QC. This QC capability, possibly using machine learning techniques, falls outside of the current scope of E-SOH and will therefore need to be built separate too, but incorporate with, E-SOH. 

*Acceptance criteria:*

*Consequences and decisions:*

### F18 - inform the data producer about corrupt format events

"Given E-SOH records a corrupt format events,when the number of events passes an agreed threshold, then E-SOH should inform the data producer through agreed channels."

*Priority:*
- primary

*Clarifications:*

*Acceptance criteria:*

*Consequences and decisions:*

### F19 - data providers to indicate the quality of the data they expose or only expose data above an agreed quality threshold

"As the E-SOH service manager, I want data providers of sub-hourly land surface observations to either indicate the quality of the data they expose or only expose data above an agreed quality threshold. So, I provide E-SOH data consumers with an expected service."

*Priority:*
 - primary

*Clarifications:*

*Acceptance criteria:*

*Consequences and decisions:*

### F20 - expose poor quality data with an indication of the data quality

"Given a data producer exposes observations data of poor quality, when those observations data are processed by E-SOH and a quality indicator is present,then the data should be exposed by E-SOH along with an indication of the data quality."

*Priority:*
- primary

*Clarifications:*

*Acceptance criteria:*

*Consequences and decisions:*

### F21 - indicate when data is of unknown quality

"Given a data producer exposes observations data (of any quality), when those observations data are processed by E-SOH and no quality indicator is present,then the data should be exposed by E-SOH along with an indication that the data are of unknown quality."

*Priority:*
- secondary

*Clarifications:*
- Should the default be to only return quality data, and an option to get all data + quality indicator)?
- The user must choose the level of quality control based on a controlled vocabulary in the discovery metadata. We may want to specify a default for use in the API search.

*Acceptance criteria:*

*Consequences and decisions:*

### F22 - convert data values and units to the expected E-SOH output

"Given a data producer exposes observations data, when those observations data are expressed in units not matching the expected E-SOH output, then E-SOH should convert the data values to match those required by E-SOH data consumers."

*Priority:*
- primary

*Clarifications:*
- Do we store the values in the original units, or in the expected E-SOH units?
- Expect users to provide values in SI units but if users provide non-SI units, we need to define where to do the conversion.
- Does WMO already describe which units should be used in BUFR? Yes. There are a lot of WMO documents, and finding what you want can be difficult, but there are a lot of definitions. For example https://www.nco.ncep.noaa.gov/sib/jeff/bufrtab_tableb.html
- What is the source of information or the specification to rely on? E.g. if there is some pressure data in mbar, should we convert in into hPa?
- We must start by following WMO rules. For example https://www.nco.ncep.noaa.gov/sib/jeff/bufrtab_tableb.html. We definitely need to do this for BUFR encoding
- Consequence / Requirement on the data producer: units must be defined using an openly available controlled vocabulary - if not, e-soh must just forward the data. Also, we expect SI units
- Implementation of the conversion ability is not first priority
- How to handle possible quality reduction caused by the conversion also needs to be considered

*Acceptance criteria:*

*Consequences and decisions:*

### F23 - near real-time access to sub-hourly observations delivered in the same format (i.e., BUFR) used by NMHSs today

"As a current data consumer of land surface observations, I want near real-time access to sub-hourly observations delivered in the same format (i.e., BUFR) used by NMHSs today. So, I can minimise development of my existing downstream systems."

*Priority:*
- primary

*Clarifications:*

*Acceptance criteria:*

*Consequences and decisions:*

### F24 - access to sub-hourly observations delivered in an Open Standard format (e.g., GeoJSON)

"As a data consumer of land surface observations, I want near real-time access to sub-hourly observations delivered in an Open Standard format (e.g., GeoJSON, CoverageJSON) following agreed and structured naming convention standards (e.g., CF and ACDD). So, I can minimize the development of new applications and reduce the need to learn domain specific formats."

*Priority:*
- primary

*Clarifications:*
- At the time of gathering requirements, GeoJSON was suggested - the consensus is now moving to CoverageJSON

*Acceptance criteria:*

*Consequences and decisions:*

### F25 - parameter naming convention standards, where not established, to be developed and followed

"As a Service Manager, I want parameter naming convention standards, where not established, to be developed and followed. So, I can efficiently maintain and lifecycle the E-SOH service."

*Priority:*
- primary

*Clarifications:*

*Acceptance criteria:*

*Consequences and decisions*

### F26 - near real-time sub-hourly observations delivered via the same method (i.e., push via GTS) used by NMHSs today

"As a current data consumer of land surface observations, I want near real-time sub-hourly observations delivered via the same method (i.e., push via GTS) used by NMHSs today. So, I can minimise development of my existing downstream systems."

*Priority:*
- tertiary

*Clarifications:*
- At the kick-off meeting on 3rd March, Jeremy Tandy mentioned that we could rely on WIS2.0 to take care of this delivery
- Jeremy also noted that there are limitations within the current GTS systems (e.g., the use for bulletin headers TTAAii) that might mean not all additional data produced via the E-SOH project can be shared via GTS. Therefore there is no requirement for E-SOH to develop additional GTS capability to enable additional observations to be shared on the GTS.

*Acceptance criteria:*

*Consequences and decisions:*

### F27 - near real-time access to sub-hourly observations via a publish-subscribe message pattern

"As a data consumer of land surface observations, I want near real-time access to sub-hourly observations via a publish-subscribe message pattern. So, I can minimise the development of new applications and reduce the need to rely on domain specific delivery methods."

*Priority:*
- primary

*Clarifications:*

*Acceptance criteria:*

*Consequences and decisions:*

### F28 - E-SOH to scale to user demands for data

"As a system manager, I want E-SOH to scale to user demands for data, especially those users requesting data via the E-SOH API and pub/sub message pattern. So, I can deliver the service expected by data consumers."

*Priority:*
- primary

*Clarifications:*

*Acceptance criteria:*

*Consequences and decisions:*

### F29 - query based on location, time, and parameter

"As a data consumer using API access, I want to query the data based on location, time, and parameter. So I can access exactly the data I require and minimised the amount of data retrieved and local post processing."

*Priority:*
 - primary

*Clarifications:*

*Acceptance criteria:*

*Consequences and decisions:*
- At this stage we expect to use EDR as the standard for the API so we should use the EDR standards for location and time. To start with, we will focus on simple radius and 2D polygon queries, and not worry about trajectories, etc.  There is still the open question about parameters but for location and time hopefully we can state EDR.
- If there is a Z axis, it needs to be defined what kind of support is required: Can one query data based on, e.g., pressure levels or height from ground level or sea level? How to use the Z axis when data is, e.g., sea temperature profiles or so?
- EDR API needs to support that, and the data storage also has to be such that we can store and query the data efficiently. Maybe the simplest form is to support the Z axis that data happens to have and the user needs to know what it is (e.g., based on metadata) and queries are possible only using that axis. Conversions etc are left to user.
- Should be defined whether the location can be in 3D (not just lat/lon) or not
- Decision: height is specified in parameter name and/or discovery metadata. We do not expect to implement vertical layer query in EDR (we will implement 2d bounding box, not 3d, at least as a start).

### F30 - pub-sub message pattern to be compliant with the requirements of WIS 2.0

"As a EUMETNET Member, I want the method of delivery via a pub-sub message pattern to be compliant with the requirements of WIS 2.0. So, I can efficiently meet my obligations as a WMO Member."

*Priority:*
 - primary

*Clarifications:*

*Acceptance criteria:*

*Consequences and decisions:*

### F31 - E-SOH software to meet agreed quality assurance standards

"As a System Manager, I want E-SOH software to meet agreed quality assurance standards. So, I can efficiently maintain and lifecycle the E-SOH service."

*Priority:*
- primary

*Clarifications:*
- What is the definition of "agreed software quality assurance standards"? We interpret this as something the e-soh project team needs to agree on.

*Acceptance criteria:*

*Consequences and decisions:*

### F32 - contributions to the E-SOH code base to be open to all EUMETNET members

"As a EUMETNET Member, I want contributions to the E-SOH code base to be Open to all Members. So, I can efficiently deliver my national and EUMETNET Strategy."

*Priority:*
- primary

*Clarifications:*

*Acceptance criteria:*

*Consequences and decisions:*

### F33 - security to be considered as a high priority

"As a System Manager, I want security to be considered as a high priority and all aspects of the system to meet IT security best practice and includes, for example, identity and access management, role- based access controls, access tokens and data encryption at rest and in transit. So, I can deliver a robust and secure system."

*Priority:*
- primary

*Clarifications:*
- In the tender, we have said the following, regarding this:
   * For F33 (security), we expect to implement encryption using secure protocols such as, e.g.HTTPS. Stored observation data will not be encrypted. Identity and Access Management (IAM) will depend on infrastructure implementations of which restrictions may apply, e.g., at EWC.
- Access control
   * Broken access control is the top top issue in the link:https://owasp.org/Top10/A01_2021-Broken_Access_Control/[OWASP/Top 10 list of the most critical security risks facing organizations].
   * It seems there is a need three separate systems for authentication and authorization:

- Data ingestion
   * There must be control of who are allowed to upload data to the system. Also, there may be several systems for uploading data. Sftp may be one of them, while others may depend on http post requests. This means that each system for ingesting data may need its own mechanisms for authentication, and possibly also authorization. If possible, it would be useful to have a common "source of truth" regarding authorization, regardless of authentication mechanism.

- Administration and monitoring
   * Access to administration and statistics about the system should not be freely available to anyone. Some system must be set up to allow access to relevant users only.
- Data delivery
   * In the first version of e-soh, there will be no restricted data, so from that perspective there is no need for authentication or authorization.
   * If, at a later stage, we will introduce access control here, there seems to be some limitations in FEMDI regarding this: The use of a message queue implies that anyone will be able to know about the *existence* of restricted data. We can only provide access control on the actual data itself. *This may or may not be acceptable at a later stage.*
   * Even if we want to only serve freely available data, we may still want to have some kind of access control here, to have some protection against servers becoming overloaded.
- Security monitoring
   * Some system must be in place to allow admins to monitor the system with regards to security incidents.
- Data encryption
   * All traffic to and from the system will use encryption. No usage of http, only https. The same applies to ftp - we will only provides sftp.

*Acceptance criteria:*

*Consequences and decisions:*

### F34 - sufficient compute resources

"As a System Manager, I want sufficient compute resource to be available. So, I can deliver a resilient and sustainable service to my users."

*Priority:*
- primary

*Clarifications:*
- The required compute resource for E-SOH is thought to be relatively low, especially compared with the requirements of NWP, Satellites and even Radar.
- The storage requirements are modest given only 24 hours of storage is required.
- Consideration also needs to be given to the requirements for resilience and for development environments. Depending on the resilience architecture and the need for development environments there might be several instances of E-SOH running in parallel to the operational system. On the other hand, depending on the service of the Cloud provider chosen, resilience might not need to be running in parallel and development environments may only exist when actively being used rather than being “always on”.
- As more observations network are added to E-SOH the resource requirements will increase accordingly. For the observations expected for E-SOH the amount of compute resource is likely to be proportional to the number of observations. As a very rough estimate, based on a traditional observations station with several observed parameters, the following compute resource is required for 5000 stations (i.e., an estimate of the number of observing stations in Europe)...
- CPU ~8 CPU Core, Memory ~8GB RAM, Storage ~1TB
- The estimate above is for a single instance of E-SOH running.
- For other networks the number of parameters per station might be less. E.g., rain-gauges might only record a single meteorological value.
- In addition to the resources required for the observations processing chain, additional resources will be required for the input and output to the systems. The number of “PUT” and “GET” request are likely to be significant given the number of  mall messages/files delivered to and disseminated by E-SOH. The Scoping study estimated between 0.25 and 1.7 Billion PUT requests per month.
- The ‘periphery’ components of E-SOH (e.g., monitoring and reporting) will also require compute resources, but these are believed to be significantly less than the core of E-SOH.
- The estimates above will need to be clarified during the design phase (WP1).
- Antoher crucial part is to estimate the load coming from open data requests. FMI open data gets about 20 req/s for observations (latest numbers should be confirmed with FMI). Scaling that up with number of countries would lead to 200-300 req/s and with number of users much more. FEMDI API gateway can hopefully cope with major part of the load, but probably not all. From that point of view, it's also important to check if, e.g., wis2box supports multiple nodes well (scaling).

*Acceptance criteria:*

*Consequences and decisions:*

### F35 - Data Enrichment and Processing

There is no requirement for E-SOH to perform any significant data enrichment or processing. However, where data received from a data producer does not contain sufficient metadata to meet the standards required of E-SOH products, these additional metadata will be added where possible.

In the case of WIGOS Station IDs (WSI) it will be the responsibility of the data producer to publish the WSI for each station exposed via E-SOH. The WSI may be expressed with the observations data provided or through an agreed metadata store (e.g., OSCAR).

*Priority:*
- primary

*Clarifications:*
- We need to state some principles before defining the standards:
   * A minimum set of (required and recommended) use and discovery metadata must follow the data, i.e., as part of the data files
   * This metadata must follow agreed standards
   * It must be possible to translate from the agreed data-following standards to other standards, such as DCAT and ISO19115 and related profiles of these
   * Based on discussion in https://app.zenhub.com/workspaces/e-soh-63fc8658faa10d2e7d262c3c/issues/zh/40 we only treat open datasets without restrictions in the first stage. This implies that a license is required on all data, and that e-soh only takes in the data if it has an open license or a release statement.

*Acceptance criteria:*

*Consequences and decisions:*


## Business requirements

### B01 - RODEO WP6 OPERA to be a flexible pathway to exposing weather radar data observations

“As a EUMETNET Member, I want RODEO to be flexible and be a pathway to exposing radar data from a single point of contact. So, I can deliver a consistent solution and reduce development activity.”

*Priority:*
- secondary

*Clarifications:*
- Documentation and education for members and other user groups are required to provide such pathway
 
*Acceptance criteria:*

*Consequences and decisions:*
- Documentation and education for members and other user groups are required to provide such pathway.

### B02 - adoption of a "build and share" approach to software development

“As a EUMETNET Member, I want the adoption of a "build and share" approach to software development. So, Members can efficiently and consistently develop national capability related to RODEO and beyond.”

*Priority:*
- primary

*Clarifications:*
- The project description says that all software should be open-source.
- OPERA is committed to share OPERA software under the GPL3.0 license with descision of EUMETNET PFAC. 

*Acceptance criteria:*
- Software in RODEO is licensed with an open license

*Consequences and decisions:*
- We will use Apache 2.0 as default?

### B03 - homogeneous data interoperability between EUMETNET Members and the wider community

“As a EUMETNET Member, I want the exchange of data, and data interoperability between EUMETNET Members and the wider community to be as homogenous as possible. So, I can meet part of my “Observations and Prediction Data” and “Science Technology and Infrastructure” Vision within the European NMHSs 2021-25 Strategy?.”

*Priority:*
- primary

*Clarifications:*
This is from E-SOH:
- It needs to be clarified what kinds of observations there will be in E-SOH, do we need separate means of exchange for 3rd party data etc. (i.e., data from stations not registered in WIGOS)?
- From the reqs (U03, U05, U06, ), it is clear that E-SOH should support distribution of non-WIGOS observations, and it should try to "normalize" those data so they can be consumed in a similar way as the WIGOS observations (e.g., by requiring transformations before sending to e-soh, or by doing the transformation in e-soh). We need to figure out in the design process how to do that, and which types of "other" observations we should support.
- We need to define use and discovery metadata that supports interoperability. Some station metadata (following a controlled vocabulary) should be required but we cannot require a WIGOS ID.
- Ignore restricted data in the beginning (i.e., data without a standard open license or release statement)

*Acceptance criteria:*

*Consequences and decisions*

### B04 - sustainable service

“As a EUMETNET Member, I want RODEO WP6 radar data supply to be a sustainable service that considers the whole lifecycle of a system from design, development, operations to retirement. So, I understand the total cost of ownership of the RODEO service.”

*Priority:*
- primary

*Clarifications:*
- It is understood that estimating the full operational costs, at the tender stage, is extremely difficult. Therefore, as well as an initial estimate during the tender phase, there is a requirement for a more accurate estimate to be produced during the initial operational phase. The fully costed estimate of the operational costs should include, for example, system life-cycling cost and reacting to emerging user needs.
- Is this just sustainable in the meaning of operating cost, not in the meaning of green computing etc?
- There is a general requirement for all EUMETNET Programmes to "ensure that the environmental footprint of the Programme is minimised where possible." So, this should be considered also in the meaning of green computing.

*Acceptance criteria:*

*Consequences and decisions:*

### B05 - continuity of service

“As a EUMETNET Member, I want continuity of service in the event of the Service Provider changing. So, I have a sustainable service delivering my obligations.”

*Priority:*
- primary

*Clarifications:*
- There is an expectation that the tender will outline how the RODEO service will be maintained in the event of a Service Provider not wishing to extend a support contract period or wishes to terminate the operational support contract after an agreed notice period.

*Acceptance criteria:*

*Consequences and decisions:*

### B06 - existing Members’ capability considered for incorporation within RODEO/OPERA?

“As a EUMETNET Member, I want, wherever possible, existing Members’ (including ECMWF, EUMETSAT) capability (e.g., EWC) considered for incorporation within E-SOH. So, previous investment is exploited to its full potential.”

*Priority:*
- secondary

*Clarifications:*

*Acceptance criteria:*

*Consequences and decisions:*

### B07 - make observations available

“As a data owner of public sector information, I want to make my observations available. So, I can meet my legal requirements, e.g., European Union Open Data Directive (HVD) obligations.”

*Priority:*
- primary

*Clarifications:*

*Acceptance criteria:*

*Consequences and decisions:*

### B08 - FAIR principles

“As a data owner, I want my data exposed following FAIR principles. So, I can meet my legal and user requirements.”

*Priority:*
- primary

*Clarifications:*
- Which of the FAIR principles we actually can fulfill in WP radar data - e.g. DOI for OPERA composite. For national data, the DOI or PID should be applied by the NMSs? 
- Findability
  * F1. (meta)data are assigned a globally unique and persistent identifier
  * F2. data are described with rich metadata
  * F3. metadata clearly and explicitly include the identifier of the data it 
describes
  * F4. (meta)data are registered or indexed in a searchable resource
 - Accessibility
   * A1. (meta)data are retrievable by their identifier using a standardized 
communications protocol
   * A1.1 the protocol is open, free, and universally implementable
   * A1.2 the protocol allows for an authentication and authorization procedure, where necessary
   * A2. metadata are accessible, even when the data are no longer available
- Interoperability
   * I1. (meta)data use a formal, accessible, shared, and broadly applicable language for knowledge representation.
   * I2. (meta)data use vocabularies that follow FAIR principles
   * I3. (meta)data include qualified references to other (meta)data
- Reusability
    * R1. meta(data) are richly described with a plurality of accurate and relevant attributes
    * R1.1. (meta)data are released with a clear and accessible data usage license
    * R1.2. (meta)data are associated with detailed provenance?
    * R1.3. (meta)data meet domain-relevant community standards

- Can FAIR, HVD and WIS2 requirements be contradictory?
- The requirements are not contradictory, but strict follow-up of the FAIR principles requires at least unique persistent id's on the dataset level (see definition elsewhere). Keeping metadata for indefinite time may be too challenging, since observation datasets are small and only live in E-SOH for 24 hours.

*Acceptance criteria:*

*Consequences and decisions:*

### B09 - data exposed in a way that’s consistent with data exchange initiatives within EUMETNET, WMO and the wider data community

“As a data owner, I want my data exposed in a way that’s consistent with data exchange initiatives within EUMETNET, WMO and the wider data community. For example, WIS 2.0, INSPIRE, HVD, and FDCM. So, I can meet my international commitments and obligations within the Meteorological and wider user community.”

*Priority:*
 - primary

*Clarifications:*

*Acceptance criteria:*

*Consequences and decisions:*

### B10 - secure mechanism to share data according to data policy

“As a data owner, I want a secure mechanism to share data according to my data policy. So, I can use RODEO to expose my data.”

*Priority:*
- primary

*Clarifications:*
- radar data belongs to the data providor, e.g. UKMO doesn't need to follow the HVD, and most likely is not willing to share the volume data through RODEO. Hence, somewhere, either in OPERA side or in RODEO, there needs to be block preventing data to be shared.
- Discussions on sharing all the OPERA data inside the composite must be agreed

*Acceptance criteria:*

*Consequences and decisions:*

### B11 - observation station metadata

“As a data owner, I want observations station metadata to be efficiently held and maintained within RODEO; synchronised with national and international metadata stores (e.g., WMO OSCAR); respecting the metadata agreed Single Source of Truth. So, I am assured my data are represented correctly to E-SOH users and costs of metadata maintenance are minimised. Correct this for OPERA data - OPERA radar database, WMO WRD radar database, various WSI shared. ”

*Priority:*
- primary

*Clarifications:*

*Acceptance criteria:*

*Consequences and decisions:*

### B12 - minimise the required changes in production systems

“As a data producer, I want to minimise the required changes in my systems prior to making data available to RODEO/OPERA. So, the value of RODEO, over developing bespoke capability, is realised.”

*Priority:*
- secondary

*Clarifications:*

*Acceptance criteria:*

*Consequences and decisions:*
- We need to establish principles for when RODEO requirements on, e.g., input data formats or interfaces can be changed to meet producer needs.

### B13 - unified approach to the supply of supplementary observations

“As a data producer, I want a unified approach to the supply of supplementary observations developed and supported. So, I can remove the need to develop bespoke solutions and the need to establish multiple bilateral agreements.”

*Priority:*
- secondary

*Clarifications:*

*Acceptance criteria:*

*Consequences and decisions:*

### B14 - radar observations delivered in the same format and exchange protocols as used today

“As a current data consumer of radar data, I want near radar observations delivered in the same format and exchange protocols as used today (i.e., HDF5 ODIM). So, I can minimise development of my systems downstream of RODEO.”

*Priority:*
- secondary

*Clarifications:*

*Acceptance criteria:*

*Consequences and decisions:*

### B15 - RODEO to handle transmission on GTS

“As a data producer, I want to rely on RODEO to handle the transmission of new, late or subsequently corrected observations on GTS, so I can replace my old systems for message generation. Applicable for radar data?”

*Priority:*
- secondary

*Clarifications:*
- The shared infrastructure of WIS2.0 will most likely be able to support this

*Acceptance criteria:*

*Consequences and decisions:*





## Dependencies

This chapter is meant to capture any relationships or interdependencies between different requirements. This information can be important for understanding how the system works as a whole, and for ensuring that each requirement is considered in the context of the broader system.

### Relationship between 

## Constraints and assumptions

The purpose of this sub-section is to document any limitations or assumptions that could impact the development of the system in order to ensure that the final product meets the users' needs and expectations. These constraints could include factors such as budget or time constraints, technical limitations, or any other factors that could affect the functionality or usability of the system. By identifying and addressing these constraints and assumptions early in the development process, we can minimize the risk of delays, misunderstandings, or unsatisfactory outcomes.

## Risks

This section should identify any risks specific to the requirements.

## Conclusion

In conclusion, the requirements document outlines the specific needs and objectives of the RODEO WP6 radar data supply, including functional and non-functional requirements. It should serve as a guide for the development team to ensure
that the final product meets the expectations and requirements Eumetnet and its associates. The document should be regularly reviewed and updated throughout the project lifecycle to ensure that any changes or additions are properly
documented and addressed. It is essential for the success of the project that all stakeholders agree on the requirements outlined in this document and use it as a reference throughout the development process.
