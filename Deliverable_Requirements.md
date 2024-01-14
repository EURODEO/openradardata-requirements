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
- [System requirements](#System_requirements)
- [Business requirements](#Business_requirements)
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

## System requirements

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




