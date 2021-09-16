

## Before you Begin

Dont give up! In this test we want to see how you will perform when given a problem. If you dont know how to do everything it is not a problem! Try to do as much as you can. 

Be creative. If you think there is a better way to do something, go ahead.

You don't have to send anything to us after you finish. We will ask you to present it to us during your interview.

## Problem Definition

Create an Airflow DAG using Python that reads launch data from the SpaceX API and loads it to a PostgresSQL database.
The API can be acessed here: https://api.spacexdata.com/v3/launches

The DAG should be scheduled on the first day of each month and only extract data of the previous month on each run. 
We want to be able to do backfilling and rerun the DAG to re-extract data from a past month if necessary.
TIP: You should use the execution_date here to control what month to extract.

You should control the access to the API by limiting the request throughput as well as the amount of records returned by each request. 

## Setup

We recommend running everything using Docker containers. You can load the data to the Airflow Postgres database if it is easier.

Some Links that might help:

https://airflow.apache.org/docs/apache-airflow/stable/start/docker.html

https://airflow.apache.org/docs/apache-airflow/stable/start/local.html