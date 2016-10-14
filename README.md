# sharp-patient-risk-poc

## Overview
### Below is the file structure of the tech-transfer

# Overview

### Below is the file structure of the tech-transfer

```
tech-transfer
│   OVERVIEW.ipynb    
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

modeling_base.ipynb
The main notebook for modeling.

modeling_diff_algorithms.ipynb
Exploring different modeling algorithms -- for reference only

modeling_sparseCO2.ipynb; modeling_sparseGCS.ipynb
These use the subset of available data which include CO2 or Glasgow Coma Score (GCS). To show that these two (particularly CO2) have predictive potential.

RunModelOnExamplePatients.ipynb
Extracts a small subset of patients, collects their statistics into a modeling tables based on different timeframes, loads the saved model, uses model to generate risk scores, then writes the scores and modeling tables to 

gbc_base.compressed
The saved model file, in sklearn's [joblib](http://scikit-learn.org/stable/modules/model_persistence.html) format.

NonRRT_modeling_table_13hr_raw.p
A pickled pandas dataframe of the modeling table for a subset of patients without RRT events.

RRT_modeling_table_13hr_raw.p
A picked pandas dataframe of the modeling table for patients with RRT events.



EDA (subfolder)
Contains notebooks which cover Exploratory Data Analysis of the data.
encounter_durations[EDA].ipynb
Explores encounter durations for patients with and without RRT events. 
Explores subselection of patients without RRT events who have similar encounter durations to patients with RRT events.

explore_vitals_by_encounter[EDA].ipynb
Creates time series of vitals signs for RRT patients which indicate time of RRT.

medications[EDA].ipynb
Explores the number of patients taking different kinds of medications, and how that breaks down for patients with and without RRT events

multi_rrts[EDA].ipynb
Explores patients with multiple RRT events. Only text output.

probe_encounter_types_classes[EDA].ipynb
Examine breakdowns of different patient/encounter types. Only text output.

rrt_reasons[EDA].ipynb
Explore the reasons for RRT events & their frequencies

vitals_avg_over_visit[EDA].ipynb
Compare if patients with RRTs have different average vitals than patients without RRTs, visually.
ETL-queries
We used the Impala Editor via Cloudera Hue to run queries on and explore the data. Queries which were not included in the notebooks are saved in this folder.
Queries are saved as .txt so files will open on jupyter.
