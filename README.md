# Udacity Data Engineering Project 05

# Data Pipeline with Airflow

## Overview

We need more automation to Sparkify data warehouse ETL pipelines through Apache Airflow.

1. The source data resides in **S3** and consist of JSON logs that tell about user activity in the application

2. Processed in Sparkify's data warehouse in **Amazon Redshift**

3. Pipeline runs tests against Sparkify's datasets after the ETL steps to catch any discrepancies in the datasets.

## Structure

- `create_tables.sql`: SQL create table statements provided with template.

`dags` directory contains:
- `sparkify_etl_dag.py`: Defines main DAG, tasks and link the tasks in required order.

`plugins/operators` directory contains:
- `stage_redshift.py`: Defines `StageToRedshiftOperator` to copy JSON data from S3 to staging tables in the Redshift via `copy` command.
- `load_dimension.py`: Defines `LoadDimensionOperator` to load a dimension table from staging table(s).
- `load_fact.py`: Defines `LoadFactOperator` to load fact table from staging table(s).
- `data_quality.py`: Defines `DataQualityOperator` to run data quality checks on all tables passed as parameter.
- `sql_queries.py`: Contains SQL queries for the ETL pipeline (provided in template).

## Config

This code uses `python 3` and assumes that Apache Airflow is installed and configured.

- Create a Redshift cluster and run `create_tables.sql` there for once only.
- Make sure to add following two Airflow connections:
    - AWS credentials, named `aws_credentials`
    - Connection to Redshift, named `redshift`