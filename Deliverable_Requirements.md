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
- [Datasets](#Dataset description)

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

## Dependencies

This chapter is meant to capture any relationships or interdependencies between different requirements. This information can be important for understanding how the system works as a whole, and for ensuring that each requirement is considered in the context of the broader system.

### Relationship between 

## Constraints and assumptions

The purpose of this sub-section is to document any limitations or assumptions that could impact the development of the system in order to ensure that the final product meets the users' needs and expectations. These constraints could include factors such as budget or time constraints, technical limitations, or any other factors that could affect the functionality or usability of the system. By identifying and addressing these constraints and assumptions early in the development process, we can minimize the risk of delays, misunderstandings, or unsatisfactory outcomes.

## User requirements

Description of use cases. Three of the use cases are stated also in the FEMDI documentation and four are related to E-SOH requirements. These are stated at each use case.  

### U01 A company or public institute, where a data scientist who wants to use radar data in their machine learning model (training and operational) environment. 

Related to use cases in FEMDI 2.4.

“As a big data consumer, I want a single unified view of available meteorological datasets in machine-readable formats and large-scale data usage / re-processing, dataset needed for training a Machine Learning (ML) model and then running it. This innovative use of met data, will help bring step-change advances to technological solutions for understanding and forecasting the weather and its impacts events.”  

*Requirements:* 

- Needs as long a history of data as possible, ideally in a cloud-optimised format
- Needs a suitable access mechanism for bulk consumption (rather than download), e.g. through S3 in cloud native formats, to download directly, so no need to download, store, etc.
- Corresponding real-time data to drive the models?
- The real-time data for execution needs to be consistent with the data used for model training (i.e., from the same source) 

*Priority:* 

*Clarifications:* 

*Acceptance criteria:* 

*Consequences and decisions:* 

### U02 A Small & Medium Enterprise (SME) application developer who wants to see what data sets are available and access them. 

Related to use cases in FEMDI 2.5 and E-SOH 4.3.

“As a new data consumer, I want a single unified view of available meteorological datasets which are updated on a regular basis, that is easily accessible and findable, is easily integrated into my systems and can be re-used (i.e., following FAIR principles). This will allow me to develop an application which makes best use of the available data to add value to the users and bring me in an income.”  

*Requirements:* 
- A software developer builds a mobile application that needs ....
- They identify a dataset via the FEMDI Shared Catalogue and determine that the API for that dataset is suitable for the application.
- The mobile application quickly becomes popular and is installed on over 10,000 devices. Each device makes a few requests a day as the user changes location, and this adds up to lots of requests on the Data Supply component’s API. 

*Priority:*  

*Clarifications:* 

- Can lead to a lot of requests and processing on the data source. 

*Acceptance criteria:* 

*Consequences and decisions:* 

### U03 A member of a public organisation who wants to see real time weather radar visualised on their mobile.  

4.4, and 4.5
“As a traffic officer manager, I want to use my smart phone to regularly check the rainfall amounts across my country and bordering countries in Europe, so I can be prepared for different driving conditions, and potential impacts on the traffic network and people’s safety.  

This will allow me to rapidly respond with appropriate resources and equipment to incidents.”   

 

[linked to E-SOH requirements 4.4, and 4.5] 

Priority: 

Clarifications 

Visualisation is out of scope of FMEID – another will provide the visualisation 

OPERA is EUMETNET’s radar programme; Also RODEO WP6. 

Potential additional use case to be considered 

Acceptance criteria 

Consequences and decisions 

=== U01 - sub-hourly resolution observations from stations operated by EUMETNET Members

As a current, or new, data consumer of land surface observations,

I want near real-time access to sub-hourly resolution observations from stations operated by EUMETNET Members that are normally only made available hourly (or less frequently),

So, I can improve the services (including forecasting of fog and convective events) I provide to my users.

==== Priority: primary

==== Clarifications

==== Acceptance criteria

==== Consequences and decisions

=== U02 - sub-hourly not normally made available

As a current, or new, data consumer of land surface observations,

I want near real-time access to sub-hourly resolution observations from stations operated by EUMETNET Members that are not normally made available,

So, I can improve the services (including forecasting of fog and convective events) I provide
to my users.

==== Priority: primary

==== Clarifications

==== Acceptance criteria

==== Consequences and decisions

=== U03 - single unified view of supplementary observations following FAIR principles

As a data consumer

I want a single unified view of supplementary observations, that is easily accessible and findable, is easily integrated into my systems and can be re-used (i.e., following FAIR principles).

So, I can access data easily, especially across national borders.

==== Priority: primary

==== Clarifications

==== Acceptance criteria

==== Consequences and decisions

=== U04 - near real-time access to rain-gauge observations that aren’t normally published

As a current, or new, data consumer of rain-gauge observations,

I want near real-time access to rain-gauge observations, from gauges operated by EUMETNET Members, that aren’t normally published,

So, I can improve the services (including forecasting of fog and convective events) I provide
to my users.

==== Priority: secondary

==== Clarifications

==== Acceptance criteria

==== Consequences and decisions

=== U05 - rain-gauge observations from 3rd parties

As a current, or new, data consumer of rain-gauge observations,

I want near real-time access to rain-gauge observations, from gauges operationally operated by 3rd parties who current make their data available to one or more EUMETNET Member, that aren’t normally published,

So, I can improve the services (including forecasting of fog and convective events) I provide to my users.

==== Priority: secondary

==== Clarifications

==== Acceptance criteria

==== Consequences and decisions

=== U06 - near real-time observations from personal weather stations

As a new data consumer of Personal Weather Station (PWS) observations,

I want access to near real-time observations from personal weather stations in a way that is consistent with other land surface observations made available via E-SOH,

So, I can improve the services (including forecasting of fog and convective events) I provide to my users and minimise development requirement in consuming data from a new observing network.

==== Priority: tertiary

==== Clarifications

==== Acceptance criteria

==== Consequences and decisions

=== U07 - first iteration and subsequent corrections

As a meteorologist in the weather forecasting services,

I need access to the first iteration of the observations data, as well as late or subsequently corrected observations,

so I can always base my forecasts on the most reliable observations.

==== Priority: primary

==== Clarifications

==== Acceptance criteria

==== Consequences and decisions

