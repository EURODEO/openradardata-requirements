# RODEO WP 6 Opera open radar data Key Performance Indicators


### Annakaisa v. Lerber, Stuart J. Matthews, Roope Tervo, Gijsbert Kruithof, Mikko Rauhala, Vegar Kristiansen, DMI (Morten?), Lukas Tüchler (?), Christoph Müller, Daniel Heintze, Steffen Kremer 


## Abstract

This document defines KPIs for the RODEO WP6 weather radar supply. The target of the KPIs is to provide guidance for system design and operations to ensure correct level of availability and usability of the system and data.

## Revision history
| Version | Date | Comment | Responsible
| :--- | :--- | :--- | :--- 
| 0.1 | 2024-01-14 | preliminary draft | Annakaisa v. Lerber
| 0.2 | 2024-02-05 | first concept | Gijsbert Kruithof
| | | |
| | | |


## Table of Content
- [Introduction](#Introduction)
- [Service Level Definitions](#Service_Level_Definitions)
- [KPIs for Data Consumption](#KPIs_for_Data_Consumption)
- [KPIs for Data Provisioning](#KPIs_for_Data_Provisioning)
- [Conclusions](#Conclusions)

## Introduction

This document defines KPIs for RODEO WP6 open radar data system. The target of the KPIs is to provide guidance for system design and operations to ensure correct level of availability and usability of the system and data.  RODEO WP6 open radar data requirement F07 states that the EUMETNET members want monthly, quarterly, and annual reports of the performance, against (to be confirmed) agreed KPIs.

The KPIs are measurable and aim to be as simple as possible, containing only few automatically collected metrics.

KPIs should not be confused with requirements nor monitoring. Requirements defines clear lower/upper bounds while KPIs target a goal. Monitoring is used to ensure that the system is operating as expected, to detect anomalies and to
trace root cause of the potential problems.

In the process of establishing the KPIs the following sources and examples are taken into consideration:

* OPERA database? Check this with needed metadata.
* [WIS 2.0 Technical requirements:](https://community.wmo.int/en/WIS2_Technical_Specification_Guidance)
* [WIS Metadata Key Performance Indicators:](https://community.wmo.int/en/activity-areas/wis/wis-metadata-kpis)?
* DWD OPERA KPI's?
* KNMI KDP KPI's
* [A Performance Benchmarking Methodology for MQTT Broker Implementations:](https://qrs20.techconf.org/QRSC2020_FULL/pdfs/QRS-C2020-4QOuHkY3M10ZUl1MoEzYvg/891500a499/891500a499.pdf) - Technical 

## Service Level Definitions

The EU HVD Regulation, Article 3 defines: "Set out and publish the terms of use of the API and the quality of service criteria on its performance, capacity and availability". This section defines three service levels to use as reference in the KPI definitions:

1. **Best effort – business hours:** Solution with support on best effort basis, on business hours. The solution has a limited capacity to operate big and several parallel inquires. Error cases fixed within 2 weeks. Simple monitoring checks. Capabilities can be developed further, according to FAIR. 
2. **Immediate response – fixes in 24 hours:** Higher system performance with moderate service level. More advanced automatic monitoring checks and alerts, 24/7 first level support, and the ability to give human support in 24 hours. Error cases fixed within a week. Capabilities can be developed further, according to FAIR. 
3. **Time critical – fixes in an hour:** Operational international data exchange for model input. 24/7 first, second and third level support, efficient monitoring tools detecting any errors, high availability, and capacity to process data. Capabilities can be developed further, according to FAIR.
   

## KPIs for Data Consumption

The KPIs for Data Consumption define the target KPIs from the perspective of the data consumers of the open radar data. This corresponds to the Search and Access APIs, and the Notification Service.

### Search and Access APIs

**Recommended Service Level:** "Immediate response – fixes in 24 hours", in the pre-operational phase.


|*ID* |*KPI* |*Description* |*Target* |*Notes*
| :--- | :--- | :--- | :--- | :--- 
|KPI-1 |Availability |The check has to request for latest data and ensure that the returned data is in accordance with the expected one. |99% |Related to requirement F02
|KPI-2|Response time|How fast the API starts the response.|TBD |
|KPI-3|Number of requests per hour |The number API requests reflect the usability of the service|TBD|KNMI recieves ca. 2000 pull request per hour for radar data
|KPI-4|Amount of data downloaded |The amount of data downloaded indicates the usability of the data|TBD|KNMI radar data download = ca. 200 GB per day 
|KPI-5|Number of unique users |The number of unique users|TBD|KNMI has ca. 200 unique users per day for radar data
|KPI-6|Quality of WIS 2.0 metadata records |WIS metadata records KPIs score|TBD |Metadata quality can be quantified with tooling available at https://github.com/wmo-im/pywcmp. For more information, see: [WMO WIS metadata KPIs](https://community.wmo.int/en/activity-areas/wis/wis-metadata-kpis).
|KPI-7|Quality of HVD metadata records|HVD metadata records KPIs score |TBD |


#### Discussion

This section aims to provide the following:

* Justification of the service level suggestion
* Indication of any consequences for data providers
* Indication of cost expectations

Ideally, the target of KPI-target would support the global NWP model
simulations. They typically run every 6 hours, whereas local area models run
every 15-60 minutes.  For example, the IFS [continuous
assimilation model](https://www.ecmwf.int/en/newsletter/158/meteorology/continuous-data-assimilation-ifs) runs every 60 minutes. 

The NWP models can be run without the latest observations [Does the same apply for radar data???], but this has a
significant impact on the quality. Hence, less than 60 minutes of downtime is
desired. However, the WP6 Opera Radar System will initially only support 99% availability in order
to meet the "immediate response" service level. Higher availability would
require the "time critical" service level.

The KPI-2 and KPI-3 targets should be derived from time-critical applications
such as, e.g., thunderstorm monitoring or marine traffic control. Notably, open
data API is _not to provide_ QoS promise for the end user applications but to
exchange data. 

KPI-5 Number of unique API users. If this can be measured via registration or
using fingerprint (e.g. combination of IP address, user-agent, operating
system, and referrer). TBD after start of operations. Maybe the number of
subscribers to the notification service (KPI-8) is easier to measure and gives
an equally good indication.

KPIs 6 and 7 highlights the need for interoperability, and a consequential
requirement on data providers to deliver their data on agreed formats with a
minimum amount of metadata following an agreed format (currently the Attribute
Convention for Data Discovery [ACDD] with possible extensions, and the Climate
and Forecast (CF) variables).

### Notification Service

**Recommended Service Level:** Immediate response – fixes in 24 hours, in the pre-operational phase.


|*ID* |*KPI* |*Description* |*Target* |*Notes*
| :--- | :--- | :--- | :---| :--- 
|KPI-8|Number of subscribers to the Notification Service|Number of subscriptions to MQTT pub/sub notifications|TBD|
|KPI-9|Number of successfully processed PUBLISH messages|Succesfully processed MQTT notifications|TBD|
|KPI-10|Publish delay|the time interval starts when a PUBLISH message is sent and ends when the corresponding PUBACK (QoS1) message has been received|TBD|
|KPI-11|Quality of MQTT messages|MQTT KPIs score |TBD |


KPIs 8-10 on the MQTT pub/sub mechanism also depend on the overall FEMDI Architecture and especially RODEO Work Package 2.

#### Discussion

This section aims to provide the following:

* Justification of the service level suggestion
* Indication of any consequences for data providers
* Indication of cost expectations

## KPIs for Data Provisioning

The KPIs for Data Provisioning define the target KPIs for the data provisioning
system, initially used by the NMHS'es. This corresponds to the Data Ingestion API(s).

### Data Ingestion API(s)
Is this applicable to the radar data? Will there be an ingestion API?

**Recommended Service Level:** "Immediate response – fixes in 24 hours", in the pre-operational phase.

*ID*|*KPI*|*Description*|*Target*|*Notes*
|:---|:---|:---|:---|:---
|KPI-12|Number of data providers |(Mainly) NMHS'es providing data |31|
|KPI-13|Number of Radar sites |Combined with the providing organisations|No target value|
|KPI-14|Amount of data ingested|Gives an indication of the scale of the ingestion system|TBD|
|KPI-15|Ingestion system uptime|The uptime of the ingestion system|99%|Please note: this can be different than the uptime of the API for the end-user
|KPI-16|Ingestion success rate|The percentage of data succesfully ingested|99.95%|Please note: rejected files which do not comply to the input standards are not counted as an unsuccesfull ingest
|KPI-17|Ingestion timeliness|Processing time from "inserted in system" to "notification sent out to destination"|< 1 minute|See Requirement F03
|KPI-18|Data transformation success rate|The percentage of BUFR and CSV files that is succesfully transformed by the system|100%|
|=========================

#### Discussion

This section aims to provide the following:

* Justification of the service level suggestion
* Indication of any consequences for data providers
* Indication of cost expectations

Internal use of the NMHSs need to be reported as a special case as it is in special interest of the EUMETNET Member States and providing organisations. The KPIs and the target figures should be the same.

The KPI-12 target is derived from an assumption that all EUMETNET Member States will provide data.

Regarding KPI-13, there is an assumption that EUMETNET Members will provide data from all of their radar sites. Is the actual number of radar sites from each Member is known at present???? 


## Conclusions
