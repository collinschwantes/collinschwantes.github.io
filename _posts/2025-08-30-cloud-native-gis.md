---
layout: post
title: Course on Cloud Native GIS
date: 2025-08-30 17:39:00
tags: cloud-computing python COG geoparquet latency
description: Notes on cloud native gis
featured: true
mermaid:
  enabled: true
  zoomable: true
---


This course was produced and run by a group called thriveGEO for Yale University - it focused on the fundamentals of cloud-computing and specialized datastores/file formats for spatio-temporal data. 

One major challenge for any researcher is data discovery.
The [STAC specification](https://stacspec.org/en) provides a common and extensible way to describe geospatial information, improving discoverability. A STAC contains multiple levels of metadata that allow you to find a specific data product and query that product so that you receive just the data you need. 

This ability to query is critical for performant cloud-native geospatial analysis because data latency is the workflow killer. 
Moving the appropriate amount of data (potentially in parallel) instead of downloading a whole the dataset saves time and resources. 

In order for this all to work effectively, you need file formats like [COG](https://cogeo.org/) and [geoparquet](https://geoparquet.org/) that allow users to slice the data into small parts and libraries like DASK that improve parallelization. With appropriately sized chunks and well defined, parallel tasks, a research can to analyses over large swaths of space and time efficiently.  

Finally, the course talked about different analysis platforms that range from custom built cloud environments to plug-and-play systems. All of the plug-and-play platforms that were presented immediately raised concerns about vendor lock and reproducibility. 

The cloud-native geospatial space is still a developing area and will likely progress significantly in the coming years. 
The STAC ecosystem could benefit from better search funcitonality by surfacing lower level metadata for each catalog. 
From a FAIR research perspective, some aspects cloud native are wonderful - e.g. coding queries to access data and running analysis on "not your machine" - while others - lack of versioning and potential for vendors to dispappear - give me pause. 