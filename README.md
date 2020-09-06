# Songplay analytics for Sparkify

A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app.
In order to enable analysis especially of what songs users are listening to a Postgres database and ETL pipeline were created with a star schema optimized for queries on song play analysis. 
This document details how to run the scripts and provides explanation of the files in the repository. 

## Schema
The schema for this database follows star model consisting of one fact table, songplays, and four dimension tables users, artists, time and songs.

## How it works

sql_queries.py contains the queries for creating and dropping tables in database and for inserting data into database for all our tables. These queries are called by etl.py that contains the ETL processes. The data for the tables is in JSON format and resides in log files and in songs database.
etl.py opens the datafile and inserting the data into database by calling SQL queries. etl.py also processes the log file data by disecting time data from the timestamp.
Songpplay table, the fact table, is created last by elt.py as it has to contain also primary keys from dimension tables.

For running first create tables by running create_tables.py. This creates tables based on queries in sql_queries.py. Then run etl.py to load the data into database. Finally check that contents of the database are correct by running test.ipynb.

## Description of files in repository

**sql_queries.py** 
- This file contains queries for dropping and creation of database tables. 
- Also contains queries for inserting data. 
- The file also has a query for selecting artist id and song id that are used when creating fact table
- The queries in this file are inputs for etl.py and create_tables.py

**create_tables.py**
- This file creates and drops databases.
- This file should be run before running etl.py

**etl.py**
- This file contains the ETL process for extracting data, transforming it and loading it into the different database tables.

**test.ipynb**
- With this file it is possible to see the contents of the created tables in the database.

**data**
- This folder contains the data used in this project
