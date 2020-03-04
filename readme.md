# nqm-social-care

[TOC]

## Available data

### Data relationships

![](./proposed-data-hierarchy.svg)

### Proposed schema

```protobuf
message ServiceUser {
    string id = 1;
    int32 dob = 2;
    Gender gender = 3;
    string nhsNumber = 4;
    repeated int32 safeguarding = 5;
    int32 createdOn = 6;
    repeated Location locationHistory = 7;
    repeated Referral referrals = 8;
    repeated Assessment assessments = 9;
    repeated CarePackage carePackages = 10;
}

enum Gender {
	UNKNOWN = 0;
	MALE = 1;
	FEMALE = 2;	
}

message Location {
	string address = 1;
	string lsoa = 2;
	int32 validFrom = 3;
}

message Referral {
	string id = 1;
	int32 opened = 2;
	int32 closed = 3;
	string reason = 4;
	repeated String tags = 5;
	string team = 6;
	string status = 7;
	string nfaReason = 8;	
}

message Assessment {
	string id = 1;
	int32 createdOn = 2;
	int32 autorisedOn = 3;
	int32 completedOn = 4;
	string reason = 5;
	repeated String tags = 6;
    string team = 7;
    string goal = 8;
    string note = 9;
}

message CarePackage {
	string id = 1;
	int32 createdOn = 2;
	int32 started = 3;
	int32 ended = 4;
	repeated String tags = 5;
	string psr = 6;
	float weeklyCost = 7;
	int32 weeklyVisits = 8;
	float weeklyContactHours = 9;
	string team = 10;
	string provider = 11;
	string note = 12;
}
```

## Getting started

### Service user map

This view displays the distribution of service users not only across the county borough, but across the "social care patch areas" and is categorised into their respective care package provider. 



### Service user status

Providing a live feed of visits, motion events, review data we are able to summarise and measure an individual's well-being at any particular point in time. Recording this data enables us to predict a service user's cost and which package they are likely to move on to  in the next "n" months.



### Service user timeline

#### 	Timeline view

Deconstructing social care into 3 primary sections (Referrals, Assessments &  Care packages), we can 	build a  historical timeline of an individual's care. This view gives insight into a client's history in the 		care system with the option to view details of each referral, assessment, and care package received.

#### 	Event view

Using a different strategy to the previous method, the event view merges these 3 sections into one timeline. Enabling us to view social care as a series of events from opening a referral to reviewing a care package.



### Care package analysis

#### 	Care package cost

Care package cost is an annual breakdown of the average weekly costs of a single care package sorted by the year it started. With this Bar chart you can see the most expensive costs for each of the care packages given the cohort selected. This page also gives information about how many clients we have sufficient data for that year and the total number of care packages that were administered.

#### 	Care package trends

Viewing a care package in a time-series graph assists in predicting the cost trajectory of a client on certain packages. Presenting normalised & complete timelines from the moment a service user began a particular care type, their total weekly cost is recorded until fully completed (or it exceeds 2 years). Each individual is then averaged with other clients to get this insight.



### Service user analysis

Viewing a cohort of service users in a time-series graph gives insight into lifetime trajectories & predictions. Presenting normalised & complete timelines from the moment a service user began social care, their total weekly cost is recorded until fully completed (or it exceeds 2 years). This view is categorised by the primary support reason (PSR) of the service user. If a client happens to have multiple PSRs through their social care lifetime, their respective costs are split into corresponding categories, representing the same point in time of their care.

Similar to the care package cost tab, it is possible to view the top 50 clients with the most expensive weekly,  annual or lifetime costs. Selecting a field takes you to the users timeline view.



### Cohort builder

Within most modules, a cohort can be set in order to view different aspects of the data. A cohort can be defined by age, gender, care type, psr, provider, etc. This builder selects (and saves) those users who remained in that cohort for 2 consecutive years. For example: selecting care package types X & Y, the users displayed will have 2 consecutive years of care packages X and Y running at the same time. 

The time-series chart displayed in this module shows the total costs of the cohort selected over a period of weeks in the service. The distribution can be inferred from the max, min and average trajectories displayed for each cohort.



### Cohort map

Displaying and clustering saved cohorts using a map of the county borough and machine learning, individuals can be grouped into colour coded groups based on their purchasing team. Sliders are used to determine how distance (in km) between points in a cluster, and the (minimal) number of points needed to create a single cluster. Identifying these clusters, the  distance travelled by social workers to their clients is minimised, saving time and money for walking social carers, but also giving the opportunity for walking social carers within each social care patch.



### Data integrity

An insightful view of the data we have received against the schema we have proposed for nqm social care. This module displays the data we have received, it's integrity and additional data which would provide useful insight. 

| Data visualisation | Description                                                  |
| :----------------- | :----------------------------------------------------------- |
| Radar chart        | Displaying data counts for each field in the schema.         |
| Population pyramid | Quick insight into the underlying social care population.    |
| Bar chart          | For fields with (potentially) infinite unique inputs, the total integrity of the field is encapsulated within a bar chart. |
| Pie chart          | Categorical breakdown of specific fields (along with its corresponding data count), the percentage below corresponds to the data integrity of that field. |



### Cluster analysis

The aim of the cluster analysis view is to allow the optimisation of existing patch boundaries and the delivery of care by different providers. It allows users to select a number of starting cohorts, defining them by PSR, Care Type, Provider, and Purchasing Team. The service users associated with these cohorts are then displayed on a map, with colour denoting the cohort to which they belong. Additionally circles are drawn on the map to show the area covered by the group, with smaller circles showing the distribution of the most centralised users.

This view also calculates an optimised geographic distribution for these users into a new set of cohorts, equal in number to those originally selected. This optimisation is based on geographical proximity, and a comparison of the efficiency of these groupings is shown in a table view on this screen.



### Cost summary

Using a tabular format, this module displays the most recent 52 weeks of data broken down by social care type & support reason.

