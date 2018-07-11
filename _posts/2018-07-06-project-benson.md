---
layout: post
title:

#### Identifying the Best NYC Subway Stations to Find Charitable Donors

![alt text](http://catholicandlovinit.com/wp-content/uploads/2018/05/Subwaymap-Htm-Alternative-Map-Of-Nyc-Subway-System.jpg "NYC Subway System")

I just finished my first week at Metis in San Francisco. We spent most of the week reviewing the basic Data Science toolkit which included review of Pandas and Visualization tools in Python, exploratory data analysis (EDA), presentation skills, and GitHub. For our first project we leveraged all of the tools we learned to help identify the optimal NYC subway stations to leaflet. In this article, I will walk you through my team's approach to framing the problem, designing the data pipeline, and ultimately implementing the analysis. You can find the project on GitHub, along with links to all the data.

### The Problem

WomenTechWomenYes (WTWY), a hypothetical non-profit organization in New York City, is raising money for their first girl’s summer coding bootcamp. In an attempt to provide underprivileged girls with financial assistance, WTWY is looking raise money at their annual summer gala.  To promote the event, street teams are being placed outside subway stations to register potential donors for the gala. WTWY would like some guidance in optimally deploying their street team members with the goal maximizing donations at the gala.

### The Approach

The goal of the project is to utilize MTA turnstile data to create a meaningful recommendation for WTWY on where and when they should deploy their street teams. Ultimately, we want to identify the stations with that have the most foot traffic  and are likely to have the highest density of individuals who fit the archetype of a strong donor to the cause.

After brainstorming and consulting existing academic studies, we believe that the target archetype is a high-income, female commuter who is employed in the tech industry.

![alt text](https://i1.rgstatic.net/publication/50205223_A_Literature_Review_of_Empirical_Studies_of_Philanthropy_Eight_Mechanisms_That_Drive_Charitable_Giving/links/0c96053613d45c5db7000000/largepreview.png "Charitable Giving Lit Review")


While, the MTA turnstile data will allow us to identify foot traffic at NYC subway stations, we needed to identify additional data sources to help identify which stations may have a high density of the targeted archetype commuters. We utilized data from *Zillow* that detailed median house prices by zip code (as a proxy for household income), a survey from *The Department of Youth and Community Development* that detailed gender density by zip code, and the *The 2016 NYC Tech Ecosystem Report​*, which helped us identify the tech hub zip codes. We were able to map these ancillary data sources to the MTA data by employing the Google Maps API to geocode the subway station locations.

This ensemble of data allowed us to zero in on subway stations which were likely to have large amounts of commuters that were women with high household income and worked in the tech industry.


![alt text](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRbfpn1xvhVG430yWYzABT9807mzAwo2ZZmHLcMN-gpc_c4H54P "NYC Tech Hubs")


### Analysis
Our team worked to munge all of the data sets so that we eventually arrived at a cross section of subway stations that detailed the average foot traffic during each day of the week (both in the morning and afternoon), the median house price associated with the station's zip code, the percent of the women in the station's zip code, and whether or not the station resided in a 'tech hub'.

Once the final data set was created, we applied a scoring algorithm based on a linear combination of the aforementioned variables. After calculating scores for each station, during each day of the week, and time of day (i.e. 'shift'); we then sorted the data set to identify the top ten 'shifts'.

### Recommendation