## Purpose

Sparkify would like to perform some analysis on songs and user activity and currently does not have an easy way to do so. The Sparkify database we have created in this project now allows for much easier analysis using PostgreSQL, with the song and user data now able to be queried from our Postgres database. The Sparkify analytics team can easily perform analysis of their user's activity using SQL.

## Schema

The Sparkify database has 5 tables in a star schema that we create by running the [create_tables.py](create_tables.py) Python script. The main fact table, `songplays` contains data related to user activity. There are 4 dimension tables, `users`, `artists`, `songs`, and `time` with foreign keys in the `songplays` table. The data included in the `songplays` table is `start_time`, `user id`, `level`, `song id`, `artist id`, `session_id`, `location`, and `user_agent`. This schema is conducive to analysis because the `songplays` table contains all of the user's activity data, the data is not fully normalized so to allow for faster queries, and you can easily perform aggregations and joins.

## ETL

The ETL pipeline is executed by running the [etl.py](etl.py) file. The pipeline takes the data contained in each file and adds it to the database after some preprocessing. The song data contained in the `song_data` folder in JSON files is gathered and loaded into two pandas DataFrames containing song data and artist data and then inserted into their respective dimension tables. The log data is similarly processed into pandas DataFrames after extracting time data and user data. Adding songplays data is the last step as it requires querying the song and artist tables in order to attempt to match artist and song data with each log entry using the song's title, artist name, and song length. 

## Building the database

