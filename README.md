## Seattle Terry Stops Final Project Submission

* Student name: Rebecca Mih
* Student pace: Part Time Online
* Scheduled project review date/time: 
* Instructor name: James Irving
* Blog post URL: 


* **Data Source:**  https://www.kaggle.com/city-of-seattle/seattle-terry-stops

    * Date of last update to the datasource: April 15, 2020


* **Key references:**
* https://assets.documentcloud.org/documents/6136893/SPDs-2019-Annual-Report-on-Stops-and-Detentions.pdf <br><br>

* https://www.seattletimes.com/seattle-news/crime/federal-monitor-finds-seattle-police-are-conducting-proper-stops-and-frisks/ <br> <br>
* https://catboost.ai/docs/concepts/python-reference_catboost_grid_search.html<br><br>
* https://towardsdatascience.com/catboost-vs-light-gbm-vs-xgboost-5f93620723db

<div>
<img src= "Seattle Police Dept.jpg"
           width=200"/>
</div


## Background

https://caselaw.findlaw.com/us-supreme-court/392/1.html

This data represents records of police reported stops under Terry v. Ohio, 392 U.S. 1 (1968). Each row represents a unique stop.

 A Terry stop is a seizure under both state and federal law. A Terry stop is
defined in policy as a brief, minimally intrusive seizure of a subject based upon
**articulable reasonable suspicion (ARS) in order to investigate possible criminal activity.**
The stop can apply to people as well as to vehicles. The subject of a Terry stop is
**not** free to leave.

Section 6.220 of the Seattle Police Department (SPD) Manual defines Reasonable Suspicion as:
Specific, objective, articulable facts which, taken together with rational inferences, would
create a  **well-founded suspicion that there is a substantial possibility that a subject has
engaged, is engaging or is about to engage in criminal conduct.**

- Each record contains perceived demographics of the subject, as reported by the officer making the stop and officer demographics as reported to the Seattle Police Department, for employment purposes.
- Where available, data elements from the associated Computer Aided Dispatch (CAD) event (e.g. Call Type, Initial Call Type, Final Call Type) are included.


## Notes on Concealed Weapons in the State of Washington

WHAT ARE WASHINGTON’S CONCEALED CARRY LAWS?
Open carry of a firearm is lawful without a permit in the state of Washington except, according to the law, “under circumstances, and at a time and place that either manifests an intent to intimidate another or that warrants alarm for the safety of other persons.”

**However, open carry of a loaded handgun in a vehicle is legal only with a concealed pistol license. Open carry of a loaded long gun in a vehicle is illegal.**

The criminal charge of “carrying a concealed firearm” happens in this state when someone carries a concealed firearm **without a concealed pistol license**. It does not matter if the weapon was discovered in the defendant’s home, vehicle, or on his or her person.

## Objectives
### Target:

   * Identify Terry Stops which lead to Arrest or Prosecution (Binary Classification)
    
### Features:
   * Location (Precinct)
   * Day of the Week (Date)
   * Shift (Time)
   * Initial Call Type
   * Final Call Type
   * Stop Resolution
   * Weapon type
   * Officer Squad
   * Age of officer
   * Age of detainee
    
    
### Optional Features:
   * Race of officer
   * Race of detainee
   * Gender of officer
   * Gender of detainee
    
   

## Definition of Features Provided

Column Names and descriptions provided in the SPD dataset  <br>
* **Subject Age Group**	
Subject Age Group (10 year increments) as reported by the officer. <br><br>

* **Subject ID**	
Key, generated daily, identifying unique subjects in the dataset using a character to character match of first name and last name. "Null" values indicate an "anonymous" or "unidentified" subject. Subjects of a Terry Stop are not required to present identification.  **Not Used** <br><br>

* **GO / SC Num**
General Offense or Street Check number, relating the Terry Stop to the parent report. This field may have a one to many relationship in the data. **Not Used** <br><br>

* **Terry Stop ID**
Key identifying unique Terry Stop reports.  **Not Used**
<br><br>

* **Stop Resolution**
Resolution of the stop**One hot encoding** <br><br>

* **Weapon Type**	
Type of weapon, if any, identified during a search or frisk of the subject. Indicates "None" if no weapons was found.  <br><br>

* **Officer ID**	
Key identifying unique officers in the dataset.
**Not Used** <br><br>

* **Officer YOB**	
Year of birth, as reported by the officer.  <br><br>

* **Officer Gender**	
Gender of the officer, as reported by the officer.
 <br><br>

* **Officer Race**	
Race of the officer, as reported by the officer. <br><br>

* **Subject Perceived Race**	
Perceived race of the subject, as reported by the officer. <br><br>

* **Subject Perceived Gender**	
Perceived gender of the subject, as reported by the officer. <br><br>

* **Reported Date**	
Date the report was filed in the Records Management System (RMS). Not necessarily the date the stop occurred but generally within 1 day.  <br><br>

* **Reported Time**	
Time the stop was reported in the Records Management System (RMS). Not the time the stop occurred but generally within 10 hours.  <br><br>

* **Initial Call Type**	
Initial classification of the call as assigned by 911.  <br><br>

* **Final Call Type**	
Final classification of the call as assigned by the primary officer closing the event.  <br><br>

* **Call Type**	
How the call was received by the communication center.

* **Officer Squad**	
Functional squad assignment (not budget) of the officer as reported by the Data Analytics Platform (DAP). <br><br>

* **Arrest Flag**	
Indicator of whether a "physical arrest" was made, of the subject, during the Terry Stop. Does not necessarily reflect a report of an arrest in the Records Management System (RMS). <br><br>

* **Frisk Flag**	
Indicator of whether a "frisk" was conducted, by the officer, of the subject, during the Terry Stop. <br><br>

* **Precinct**	
Precinct of the address associated with the underlying Computer Aided Dispatch (CAD) event. Not necessarily where the Terry Stop occurred. <br><br>

* **Sector**	
Sector of the address associated with the underlying Computer Aided Dispatch (CAD) event. Not necessarily where the Terry Stop occurred. <br><br>

* **Beat**	
Beat of the address associated with the underlying Computer Aided Dispatch (CAD) event. Not necessarily where the Terry Stop occurred. <br><br>

## Analysis Workflow (OSEMN)

1. **Obtain and Pre-process**
    - [x] Import data
    - [x] Remove unused columns
    - [x] Check data size, NaNs, and # of non-null values which are not valid data 
    - [x] Clean up missing values by imputing values or dropping
    - [x] Replace ? or other non-valid data by imputing values or dropping data
    - [x] Check for duplicates and remove if appropriate
    - [x] Change datatypes of columns as appropriate 
    - [x] Note which features are continuous and which are categorical<br><br>

2. **Data Scoping**
     - [x] Use value_counts() to identify dummy categories such as "-", or "?" for later re-mapping
     - [x] Identify most common word data
     - [x] Decide on which columns (features) to keep for further feature engineering
   
3. **Transformation of data (Feature Engineering)**
    - [x] Re-bin categories to reduce noise
    - [x] Re-map categories as needed
    - [x] Engineer text data to extract common word information
    - [x] Transform categoricals using 1-hot encoding or label encoding/
    - [x] Perform log transformations on continuous variables (if applicable)
    - [x] Normalize continuous variables
    - [x] Use re-sampling if needed to balance the dataset <br> <br>
    
4. **Further Feature Selection**
     - [x] Use .describe() and .hist() histograms
     - [x] Identify outliers (based on auto-scaling of plots) and remove or inpute as needed
     - [x] Perform visualizations on key features to understand  
     - [x] Inspect feature correlations (Pearson correlation) to identify co-linear features**<br><br>

5.  **Create a Vanilla Machine Learning Model**
    - [x] Split into train and test data 
    - [x] Run the model
    - [x] Review Quality indicators of the model <br><br>

6. **Run more advanced models**
    - [x] Compare the model quality
    - [x] Choose one or more models for grid searching <br><br>
    
7. **Revise data inputs if needed to improve quality indicators**
    - [x] By adding created features, and removing colinear features
    - [x] By improving unbalanced datasets through oversampling or undersampling
    - [x] by removing outliers through filters
    - [x] through use of subject matter knowledge <br><br>
    
8. **Write the Report**
    - [X] Explain key findings and recommended next steps

