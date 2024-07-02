# Project: Data Warehouse on_AWS
ETL pipeline that extracts their data from S3, stages them in Redshift, and transforms data into a set of dimensional tables for their analytics team to continue finding insights into what songs their users are listening to.

A music streaming startup, Sparkify, has grown their user base and song database and want to move their processes and data onto the cloud. Their data resides in S3, in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

**Staging**

- **1. staging_events**: stores data extracted from JSON logs on user activity. Columns: artist, auth, firstName, gender, itemInSession, lastName, length, level, location, method, page, registration, sessionId, song, status, ts, userAgent, userId*
- **2. staging_songs**: stores data extracted from JSON metadata on the songs in the app. Columns: *num_songs, artist_id, artist_latitude, artist_longitude, artist_location, artist_name, song_id, title, duration, year

**FACT And Dimensions**

- **Fact Table**
  - 1. **songplays**: records in event data associated with song plays i.e. records with page NextSong. Columns: songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent

- **Dimension Tables**
  - 1. **users**: all the users in the music streaming app.
  **Columns**: user_id, first_name, last_name, gender, level

  - 2. **songs**: all the songs in music database.
  **Columns**: song_id, title, artist_id, year, duration

  - 3. **artists**: all the artists in music database.
  **Columns**: artist_id, name, location, latitude, longitude

  - 4. **time**: timestamps of records in songplays broken down into specific units. 
  **Columns**: start_time, hour, day, week, month, year, weekday

## ETL pipeline

- 1. [create_tables.py](create_tables.py) will create and drop all existing tables as per the queries.[sql_queries.py](sql_queries.py).

- 2. [etl.py](etl.py) copying data from s3 to staging table and then populate fact table and dimension tables.
