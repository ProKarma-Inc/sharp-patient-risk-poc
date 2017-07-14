# Pipeline

The pipeline builds the training dataset from the Cerner EMR system.

It is a Python script that runs a series of Impala queries to obtain the necessary data. The resulting data is processed and cleaned in Pandas before being output to either Hive or locally as a CSV file.

### Note: The medications

# Usage




# To Do

1. Add a way to accept a Hive schema as an input, rather than having the schema hard-coded into training_pipeline.py
2. Creating a more robust argument parser to ensure the command line arguments passed to training_pipeline.py are the correct ones.
