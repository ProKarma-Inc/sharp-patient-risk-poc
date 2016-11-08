# sharp-patient-risk-poc

# Overview

### Below is the file structure of the tech-transfer

```
tech-transfer
|   README.md
│   OVERVIEW.ipynb
|   Sharp-Intel-Technology-Transfer-Workshop.pdf
|   sharppatientrisk.yml
│
└───notebooks
│   └───modeling
|   │   │   create_modeling_table.ipynb
|   │   │   fix_modeling_table.ipynb
|   │   │   modeling_base.ipynb
|   |   |   modeling_diff_algorithms.ipynb
|   |   |   modeling_sparseCO2.ipynb
|   |   |   modeling_sparseGCS.ipynb
|   |   |   RunModelOnExamplePatients.ipynb
|   |   |   gbc_base.compressed
|   |   |   NonRRT_modeling_table_13hr_raw.p
|   |   |   RRT_modeling_table_13hr_raw.p
│   │
│   └───EDA
│       │   encounter_durations[EDA].ipynb
│       │   explore_vitals_by_encounter[EDA].ipynb
|       |   medications[EDA].ipynb
|       |   multi_rrts[EDA].ipynb
|       |   probe_encounter_types_classes[EDA].ipynb
|       |   rrt_reasons[EDA].ipynb
│       │   vitals_avg_over_visit[EDA].ipynb
│   
└───etl-queries
    │   Compare_arrival_depart_times.sql.txt
    │   Count_MedCategory.sql.txt
    |   demo_scores.sql.txt
    |   demo_scores_with_changes.sql.txt
    |   DrugCategories.sql.txt
    |   DrugName_to_DrugCategory.sql.txt
    |   encounter_location_history.sql.txt
    |   encounter_location_history_pairs.sql.txt
    |   med_hist_encntr_med_admin.sql.txt
    |   med_hist_encntr_med_admin_hr_cnt.sql.txt
    |   med_hist_RRT_event.sql.txt
    |   med_hist_RRT_event_distinct_med_hr_bucket.sql.txt
    |   med_hist_RRT_event_med_hr_bucket.sql.txt
    |   med_hist_RRT_non-event.sql.txt
    |   med_hist_RRT_non-event_distinct_med_hr_bucket.sql.txt
    |   med_hist_RRT_non-event_med_hr_bucket.sql.txt
    |   MostFrequentVitalsWLoc.sql.txt
    |   PersonQuery_KnownPersonID.sql.txt
```

## Approach to work
We typically explored the data using the Impala query editor in Hue. Once the data of interest were initially identified, we then ran such queries and worked with the results in jupyter notebooks.


# notebooks

### This section talks about what is in each of the notebooks and why we did what we did

## modeling (subfolder)
Contains notebooks which cover the creation of the predictive model and cross validation.

#### create_modeling_table.ipynb
Create modeling tables from the EMR, for patients with and without RRT events. Currently very time intensive to run (on the order of hours).
Modeling tables condensing data from 13 hours - 1 hour before the RRT event (or non-event) were saved for easy reference (see below).

#### fix_modeling_table.ipynb
In some cases, the create_modeling_table scripts would run but would not condense values for

#### modeling_base.ipynb
The main notebook for modeling.

#### modeling_diff_algorithms.ipynb
Exploring different modeling algorithms -- for reference only

#### modeling_sparseCO2.ipynb; modeling_sparseGCS.ipynb
These use the subset of available data which include CO2 or Glasgow Coma Score (GCS). To show that these two (particularly CO2) have predictive potential.

#### RunModelOnExamplePatients.ipynb
Extracts a small subset of patients, collects their statistics into a modeling tables based on different timeframes, loads the saved model, uses model to generate risk scores, then writes the scores and modeling tables to

#### gbc_base.compressed
The saved model file, in sklearn's [joblib](http://scikit-learn.org/stable/modules/model_persistence.html) format.

#### NonRRT_modeling_table_13hr_raw.p
A pickled pandas dataframe of the modeling table for a subset of patients without RRT events.

#### RRT_modeling_table_13hr_raw.p
A picked pandas dataframe of the modeling table for patients with RRT events.



## EDA (subfolder)
Contains notebooks which cover Exploratory Data Analysis of the data.

#### encounter_durations[EDA].ipynb
Explores encounter durations for patients with and without RRT events. Explores subselection of patients without RRT events who have similar encounter durations to patients with RRT events.

#### explore_vitals_by_encounter[EDA].ipynb
Creates time series of vitals signs for RRT patients which indicate time of RRT.

#### medications[EDA].ipynb
Explores the number of patients taking different kinds of medications, and how that breaks down for patients with and without RRT events

#### multi_rrts[EDA].ipynb
Explores patients with multiple RRT events. Only text output.

#### probe_encounter_types_classes[EDA].ipynb
Examine breakdowns of different patient/encounter types. Only text output.

#### rrt_reasons[EDA].ipynb
Explore the reasons for RRT events & their frequencies

#### vitals_avg_over_visit[EDA].ipynb
Compare if patients with RRTs have different average vitals than patients without RRTs, visually.

## ETL-queries

### We used the Impala Editor via Cloudera Hue to run queries on and explore the data. Queries which were not included in the notebooks are saved in this folder.
#### Queries are saved as .txt so files will open on jupyter.

### Saved Queries

| Query (file) name  | Description | Subject |
|-------------|-------------|-------------------------|
||||
| <b>encounter_location_history</b> | Show history of changes to patient location or level of care. | location_history |
| <b>encounter_location_history_pairs</b> | Show the distinct pairings of [from > to] locations. | location_history |
||||
| <b>med_hist_encntr_med_admin</b> | Associate medication with ordinal hour of administration within an encounter. | med_history |
| <b>med_hist_encntr_med_admin_hr_cnt</b> | Count number of medication administrations in each ordinal hour of encounter. | med_history |
|<b>med_hist_encntr_distinct_med_admin_hr_cnt</b>|Count number of distinct medications administered in each ordinal hour of encounter.| med_history|
| <b>med_hist_RRT_event</b> | Associate RRT event with ordinal hour of occurrence within an encounter. |med_history|
| <b>med_hist_RRT_non-event</b> | Associate non-RRT-event with ordinal hour of occurrence within an encounter. | med_history|
| <b>med_hist_RRT_event_med_hr_bucket</b> | Count number of medication administrations in 10 hourly buckets leading up to event| med_history |
|<b>med_hist_RRT_non-event_med_hr_bucket</b> | Count number of medication administrations in 10 hourly buckets leading up to non-event. | med_history|
| <b>med_hist_RRT_event_distinct_med_hr_bucket</b> | Count number of distinct medications administered in 10 hourly buckets leading up to event. | med_history |
| <b>med_hist_RRT_non-event_distinct_med_hr_bucket</b> |Count number of distinct medications administered in 10 hourly buckets leading up to non-event. | med_history |
||||
|<b>demo_scores</b> | Join rows in scoring table to associated encounter and patient. | demo |
| <b>demo_scores_with_changes</b> | Show changes in score and feature values across sequential rows in scoring table. | demo |
||||
|<b>MostFrequentVitalsWLoc</b> | Returns counts for potentially useful vitals signs | vitals |
|<b> DrugName_to_DrugCategory</b> | Return drug id and drug category given a partial drug name | drugs |
|<b> DrugCategories</b> | Show all the different drug categorizations | drugs |
|<b> Count_MedCategory</b> | Count the number of encounters where patients are taking various drug classes | drugs |
|<b> Compare_arrival_depart_times</b> | Output the different timestamps associated with an encounter | time |
|<b> PersonQuery_KnownPersonID</b> | Return info related to person, given a personid | person info |


### Environment and notes

##### Environment and install: We recommmend users install the [Anaconda scientific python distribution](https://www.continuum.io/downloads). We used python v2.7. We relied on the [impyla](https://github.com/cloudera/impyla/blob/master/README.md) and [ibis](http://www.ibis-project.org/) packages to pull data from HDFS to the jupyter notebook, and to write back to the tables. Other dependencies include: pandas, numpy, matplotlib, scikit-learn, cPickle, and seaborn. The dependencies are included in the "sharppatientrisk.yml" environment file. The environment can be loaded by the command:
```conda env create -f sharppatientrisk.yml```

##### - The times of RRT events (and all events from the clinical_event table) was recorded in the field "event_end_dt_tm" in the clinical_event table. This is an example where it is very important to have good relationships with your subject matter experts. This field records when the event took place, not the time of the end of the event.

##### - We discovered partway through the process that not all arrival time information was recorded consistently in the encounters table. Sometimes, "arrival_dt_tm" field in the encounters table was overwritten with the time a patient became an inpatient in the facility, rather than the true time of arrival. To get true time of arrival, we need to join to the tracking_item and tracking_checkin tables. Below is an example of querying for the encounter id and the true arrival time. The MIN in the subquery is to select only one timestamp, as some records contained duplicate entries. The difference in arrival time may or may not be relevant to the question at hand.

```
SELECT enc.encntr_id, COALESCE(tci.checkin_dt_tm, enc.arrive_dt_tm) AS check_in_time
FROM encounter enc
INNER JOIN clinical_event ce
ON ce.encntr_id = enc.encntr_id
LEFT OUTER JOIN  ( SELECT ti.encntr_id AS encntr_id, MIN(tc.checkin_dt_tm)  AS checkin_dt_tm
    FROM tracking_item ti
  JOIN tracking_checkin  tc ON  ti.tracking_id  = tc.tracking_id
GROUP BY ti.encntr_id ) tci
ON tci.encntr_id = enc.encntr_id```
