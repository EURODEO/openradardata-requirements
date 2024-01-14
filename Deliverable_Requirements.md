# RODEO WP6: OPERA Open Radar Data Sharing Requirements

### Annakaisa v. Lerber, Stuart J. Matthews, Gijsbert Kruithof, Mikko Rauhala, Roope Tervo, Vegar Kristiansen, Morten W. Hansen.


## Abstract

This is the Requirements Document for the the RODEO WP6 for sharing weather radar data. This document outlines the technical requirements and objectives for the development of radar data supply, which utilizes components developed in the the EUMETNET Federated European Meteorological Data Infrastructure (FEMDI) programme. The objective of work in WP6 is utilize the data sharing done in the EUMETNET OPERA programme already over a decase and, build on this collaboration a data supply for the third-party users in line with the World Meteorological Organization’s (WMO) Information System 2.0 (WIS 2.0) strategy and the European Union’s (EU) regulation on Meteorological High Value Data (HVD).

## Revision history
| Version | Date | Comment | Responsible
| :--- | :--- | :--- | :--- 
| 0.1 | 2024-01-14 | preliminary draft | Annakaisa v. Lerber
| | | |
| | | |
| | | |


## Table of Content
- [Introduction](#Introduction)
- [Dataset description](#Dataset_description)
- [User requirements](#User_requirements)
- [Dependencies](#Dependencies)
- [Constraints and assumptions](#Constraints_and_assumptions)

## Introduction
This is the Requirements Document for the RODEO WP6 for sharing weather radar data. This document outlines the technical requirements and objectives for the development of radar data supply, which utilizes components developed in the the EUMETNET Federated European Meteorological Data Infrastructure (FEMDI) programme. The objective of work in WP6 is utilize the data sharing done in the EUMETNET OPERA programme already over a decase and, build on this collaboration a data supply for the third-party users in line with the World Meteorological Organization’s (WMO) Information System 2.0 (WIS 2.0) strategy and the European Union’s (EU) regulation on Meteorological High Value Data (HVD).

This document is intended for the development team, stakeholders, and anyone interested in the technical specifications of WP6 weather radar data supply. It includes a detailed description of the system’s functional and non-functional requirements, acceptance criteria, and risks.

We hope that this document will serve as a clear guide for the development and implementation of work performed in WP6 for radar data supply and help ensure its successful integration with the FEMDI programme and within RODEO-project.

## Dataset description

### OPERA Composite Data

The composites cover the whole of Europe in a Lambert Equal Area projection. In ODYSSEY production (2011- 2023), they all are updated every 15 minutes, and issued ca. 15 minutes after data time.

- in BUFR and HDF5, possible GeoTiff
- production stable since 2012? Changes in production in 2024.

The composite corner coordinates, approximately: 70 N 30 W, 70N 50E, 32N 15W, and 32 N 30E.

There are three products on offer from the OPERA suite of products:
 
#### OPERA Instantaneous Maximum Reflectivity (in dBz)
- In the maximum reflectivity composite each composite pixel contains the maximum of all polar cell values of the contributing radars at that location.
- ODYSSEY production 2012-2023 with 
#### Instantaneous Surface Rain rate composite (in mm/h)
- In the  rain rate composite each composite pixel is a weighted average of the valid pixels of the contributing radars,      weighted by a quality index, the distance from center of the pixel and an exponential index related to inverse of the       beam altitude.
- Polar cells within a search radius of 2.5 km of the composite pixel are considered.
- Measured reflectivity values are converted to rainfall (mm/h) using the Marshall-Palmer equation.
#### OPERA One Hour rainfall Accumulation (in mm)
- Rainfall accumulation is the sum of the previous four 15-minute rain-rate products.

#### National composites
 - formats?
 - temporal and spatial resolution
 - included metadata

### National volume radar data
- DBZH, TH, VRADH
- can be sent as volumes, or scan-by-scan, radar variables can be in the same file or seprately
- two types of scans, reflectivity or velocity - optimized
- in VRADH aliasing is not always performed.
- ODIM Data format model vr. 2-2.4 not always reverse compatible
- archive in different national BUFR version, there are some manual how to encode these
- the newer files in HDF
- various national scanning strategies, definitions of scanning time, spatial and temporal resolution.
- different quality processing levels 

## User requirements

Description of use cases. Three of the use cases are stated also in the FEMDI documentation and four are related to E-SOH requirements. These are stated at each use case.  

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

## Dependencies

This chapter is meant to capture any relationships or interdependencies between different requirements. This information can be important for understanding how the system works as a whole, and for ensuring that each requirement is considered in the context of the broader system.

### Relationship between 

## Constraints and assumptions

The purpose of this sub-section is to document any limitations or assumptions that could impact the development of the system in order to ensure that the final product meets the users' needs and expectations. These constraints could include factors such as budget or time constraints, technical limitations, or any other factors that could affect the functionality or usability of the system. By identifying and addressing these constraints and assumptions early in the development process, we can minimize the risk of delays, misunderstandings, or unsatisfactory outcomes.




