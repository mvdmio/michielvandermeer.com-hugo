+++
title = "Ridder HortOS"
date = 2021-09-01
feature_image = "/images/projects/Ridder-HortOS.png"
author = "Michiel van der Meer"
+++

Developing a large-scale data ingestion and analysis tool for the horticultural sector.

I designed a platform that can ingest large amounts of data from all sorts of sensors and platforms in greenhouses, and transforms that data into information useful to the Managers and Growers in the Organizations of those greenhouses. I then led two development teams who developed the platform over the course of two years.

We had a development team in Romania (6 developers) and in the Netherlands (2 developers). We collaborated closely with the other development teams at Ridder (Climate & Water and Productive), who connected their respective systems to HortOS through an API I designed. I also collaborated with third parties who connected their applications to the HortOS data platform in order to calculate different pieces of information relevant to those 3rd parties.

More (commercial) information about the platform can be found [on the Ridder website](https://ridder.com/hortos/).

I worked with: C#, .NET Core (2, 3, 3.1), .NET 5, Entity Framework, Microsoft Azure (App Services, Azure SQL database, Servicebus, Application Gateway, ARM), Microsoft Active Directory, Microsoft Active Directory B2C, Microsoft Azure DevOps (Boards, Pipelines, Releases).

I had to solve some interesting challanges during this project:

-  Get SQL server to perform well with querying gigabytes of sensor data
-  Efficiently querying millions of rows of data from an ASP.NET application
-  Optimize throughput of Azure Functions so that we could handle tens-of-thousands of messages per hour
