# Pipeline

The pipeline builds the training dataset from the Cerner EMR system.

It is a Python script that runs a series of Impala queries to obtain the necessary data. The resulting data is processed and cleaned in Pandas before being output to either Hive or locally as a CSV file.
