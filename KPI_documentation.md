# RODEO WP6 Open Radar Data Key Performance Indicators


### Gijsbert Kruithof (KNMI), Annakaisa v. Lerber (FMI), Stuart J. Matthews (EUMETNET), Roope Tervo (EUMETSAT), Mikko Rauhala (FMI), Vegar Kristiansen (METNO) 


## Abstract

This document defines KPIs for the RODEO WP6 Open Radar Data (ORD) supply. The target of the KPIs is to provide guidance for system design and operations to ensure correct level of availability and usability of the system and data.

## Revision history
| Version | Date | Comment | Responsible
| :--- | :--- | :--- | :--- 
| 0.1 | 2024-01-14 | preliminary draft | Annakaisa v. Lerber
| 0.2 | 2024-02-05 | first concept | Gijsbert Kruithof
| 0.3 | 2024-05-03 | after discussion in RODEO RADAR Team meeting | Gijsbert Kruithof
| 1.0 | 2024-06-28 | Document reviewed for MS16 | Annakaisa von Lerber


## Table of Content
- [Introduction](#Introduction)
- [Service Level Definitions](#Service-Level-Definitions)
- [KPIs for Data Consumption](#KPIs-for-Data-Consumption)
- [KPIs for Data Provisioning](#KPIs-for-Data-Provisioning)

## Introduction

This document defines KPIs for RODEO WP6 Open Radar Data (ORD) supply. The target of the KPIs is to provide guidance for system design and operations to ensure correct level of availability and usability of the system and data.  ORD requirement F07 in the [Requirement documentation](#Deliverable_Requirements.md) states that the EUMETNET members want monthly, quarterly, and annual reports of the performance, against (to be confirmed) agreed KPIs.

The KPIs are measurable and aim to be as simple as possible, containing only few automatically collected metrics. KPIs should not be confused with requirements nor monitoring. Requirements defines clear lower/upper bounds while KPIs target a goal. Monitoring is used to ensure that the system is operating as expected, to detect anomalies and to
trace root cause of the potential problems.

In the process of establishing the KPIs the following sources and examples are taken into consideration:

* [OPERA Database](Annex/ANNEX2_OPERA_RADARS_DB_2024_02.csv) 
* [WIS 2.0 Technical requirements](https://community.wmo.int/en/WIS2_Technical_Specification_Guidance)
* [WIS Metadata Key Performance Indicators](https://community.wmo.int/en/activity-areas/wis/wis-metadata-kpis)
* [A Performance Benchmarking Methodology for MQTT Broker Implementations](https://qrs20.techconf.org/QRSC2020_FULL/pdfs/QRS-C2020-4QOuHkY3M10ZUl1MoEzYvg/891500a499/891500a499.pdf) 

## Service Level Definitions

The EU HVD Regulation, Article 3 defines: "Set out and publish the terms of use of the API and the quality of service criteria on its performance, capacity and availability". This section defines three service levels to use as reference in the KPI definitions:

1. **Reasonable endeavour – business hours:** Solution with support on reasonable endeavour basis, on business hours. The solution has a limited capacity to operate big and several parallel inquires. Error cases fixed within 2 weeks. Simple monitoring checks. Capabilities can be developed further, according to FAIR. 
2. **Immediate response – fixes in 24 hours:** Higher system performance with moderate service level. More advanced automatic monitoring checks and alerts, 24/7 first level support, and the ability to give human support in 24 hours. Error cases fixed within a week. Capabilities can be developed further, according to FAIR. 
3. **Time critical – fixes in an hour:** Operational international data exchange for model input. 24/7 first, second and third level support, efficient monitoring tools detecting any errors, high availability, and capacity to process data. Capabilities can be developed further, according to FAIR.

In OPERA, the Service Level Agreements (SLAs) for production are defined separately for each of the three production lines, as they are operated by different NMSs and the service levels offered can vary. The OPERA SLAs are detailed in [ANNEX1 OPERA SLA](./Annex/ANNEX1_OPERA_SLA_08032024.pdf).

Generally, the production lines are designed to serve operationally. Each production line has a secondary backup system, but switching to the backup is not automatic and can take several hours. Additionally, the service desks do not monitor production performance 24/7. For example, the goal at the OPERA hub is to provide an initial response to support inquiries in 75% of cases within three working days and to resolve 75% of inquiries within two weeks.

In the ORD supply, the targeted service levels are not yet defined. These will be established collaboratively in the RODEO project as part of the Quality of Service framework, following the preliminary implementation of the ORD API FEMDI Gateway. Additionally, the service desk correspondence will  be determined jointly within the RODEO project. The target of ORD supply is outlined in requirements F01-F05, aiming for a 24/7 service with an allowable yearly data disruption margin of 1%, and a maximum delay of one minute in data flow from the OPERA/national interface to making the datasets available in the S3. 

## KPIs for Data Consumption

The KPIs for Data Consumption define the target KPIs from the perspective of the data consumers of the ORD. This corresponds to the Search and Access APIs shown in Table 1., and the Notification Service in Table 2.

### Search and Access APIs

**Recommended Service Level:** "Reasonable endeavour – business hours", in the pre-operational phase.

Table 1. KPI for Search and Access API.
|*ID* |*KPI* |*Description* |*Target* |*Notes*
| :--- | :--- | :--- | :--- | :--- 
|KPI-1 |Availability |The check has to request for latest data and ensure that the returned data is in accordance with the expected one. |99% |Related to requirements F02, F04, F05
|KPI-2|Response time of the archived ORD|How fast the API starts the response.|TBD |
|KPI-3|Response time of the 24-hour cache of ORD|How fast the API starts the response.|TBD |
|KPI-4|Number of requests per hour |The number API requests reflect the usability of the service|TBD|The system should be able to scale up to 200 pull request per second (Revised FEMDI ET Estimation). 
|KPI-5|Amount of data downloaded |The amount of data downloaded indicates the usability of the data|TBD|National examples: KNMI radar data download = ca. 200 GB per day + FMI ca. 300 GB per day + DMI: 25 GB per day; average download size across all types 429 kB; number of downloads 58.627 per day
|KPI-6|Number of unique users |The number of unique users|TBD|Examples: KNMI has ca. 200 unique users per day for radar data

#### Discussion

KPI-1: The 99% is based on the target availability of the European Weather Cloud levels.

KPI-5 Number of unique API users: This metric can be tracked through user registration or by using a fingerprinting method (e.g., a combination of IP address, user-agent, operating system, and referrer). However, this approach will be determined after the start of operations. Currently, WP2 FEMDI does not plan to authenticate users, so if KPI-5 needs to be tracked per user, an alternative mechanism will be required. One possibility is to measure the number of subscribers to the notification service (KPI-8), which might be easier to track and could provide a similarly good indication.

KPI-4 and KPI-5: the number of requests and amount of data downloaded are not automatically monitored on EWC. So it needs an explicit effort to measure and report these.

### Notification Service

**Recommended Service Level:** "Reasonable endeavour – business hours", in the pre-operational phase.

Table 2. The KPIs of the Notification Service
|*ID* |*KPI* |*Description* |*Target* |*Notes*
| :--- | :--- | :--- | :---| :--- 
|KPI-8| Number of subscribers| |TBD|
|KPI-10|Publish delay|the time interval starts when a PUBLISH message is sent and ends when the corresponding PUBACK (QoS1) message has been received|TBD|

#### Discussion

Initially only the WIS2.0 Global brokers will subscribe to the notification service

## KPIs for Data Provisioning

The KPIs for Data Provisioning define the target KPIs for the data provisioning system, initially used by the NMHS'es. This corresponds to the Data Ingestion API(s) shown in Table 3.

### Data Ingestion API(s)
The main data source for ORD is OPERA, therefore the Data ingestion KPI's are only applicable to the national products D03.

**Recommended Service Level:** "Reasonable endeavour – business hours", in the pre-operational phase.

Table 3. KPIs for Data Ingestion API(s).
*ID*|*KPI*|*Description*|*Target*|*Notes*
|:---|:---|:---|:---|:---
|KPI-12|Number of data providers |(Mainly) NMHS'es providing data |33|
|KPI-13|Amount of data ingested|Gives an indication of the scale of the ingestion system|TBD|
|KPI-14|Ingestion system uptime|The uptime of the ingestion system|99%|Please note: this can be different than the uptime of the API for the end-user
|KPI-15|Ingestion success rate|The percentage of data succesfully ingested|99.95%|Please note: rejected files which do not comply to the input standards are not counted as an unsuccesfull ingest
|KPI-16|Ingestion timeliness|Processing time from "inserted in system" to "notification sent out to destination"|< 1 minute|See Requirement F03

#### Discussion

The KPI-12 target is derived from an assumption that all EUMETNET Member States will provide data.

Internal use of the NMHSs need to be reported as a special case as it is in special interest of the EUMETNET Member States and providing organisations. The KPIs and the target figures should be the same.

KPI-15: To be decided if this can be measured accurately.

