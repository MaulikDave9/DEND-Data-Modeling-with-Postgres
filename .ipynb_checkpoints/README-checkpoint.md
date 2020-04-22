# Data Modeling with Postgres

## Purpose of this database 

The raw data is in JSON file format in song and log datasets.  It's very hard to analyze and answer questions like user's activities around songs.  The startup, Sparkify will run analytics on this data to find more insights on songs, artists, users. The postgre database was developed to optimize queries on song play analysis. 

### Example of song dataset:

{
   "num_songs": 1, 
   "artist_id": "ARD7TVE1187B99BFB1", 
   "artist_latitude": null, 
   "artist_longitude": null, 
   "artist_location": "California - LA", 
   "artist_name": "Casual", 
   "song_id": "SOMZWCG12A8C13C480", 
   "title": "I Didn't Mean To", 
   "duration": 218.93179, "year": 0
}

### Example of log dataset:

{
   "artist":null,
   "auth":"Logged In",
   "firstName":"Walter",
   "gender":"M",
   "itemInSession":0,
   "lastName":"Frye",
   "length":null,
   "level":"free",
   "location":"San Francisco-Oakland-Hayward,CA",
   "method":"GET",
   "page":"Home",
   "registration":1540919166796.0,
   "sessionId":38,
   "song":null,
   "status":200,
   "ts":1541105830796,
   "userAgent": "\"Mozilla\/5.0 (Macintosh; Intel Mac OS X 10_9_4) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/36.0.1985.143 Safari\/537.36\"",
   "userId":"39"
}

## Database schema design and ETL pipeline.

Star schma was created with five tables: songplays, users, songs, artists, time

ETL on the song_data dataset was done to create the songs and artists dimensional tables and ETL on the log_data dataset was done to create the time and users dimensional tables, and the songplays fact table.

1. songplays - records log associated with song plays. Following are the columns with Type.
 
        songplay_id SERIAL PRIMARY KEY
        start_time  TIMESTAMP 
        user_id     INT 
        level       TEXT 
        song_id     TEXT 
        artist_id   TEXT 
        session_id  INT 
        location    TEXT 
        user_agent  TEXT

2. users - users in the app

        user_id    INT PRIMARY KEY 
        first_name TEXT 
        last_name  TEXT 
        gender     TEXT 
        level      TEXT

3. songs - songs in music database
   
        song_id   TEXT PRIMARY KEY 
        title     TEXT 
        artist_id TEXT 
        year      INT 
        duration  FLOAT 

4. artists - artists in music database

        artist_id  TEXT PRIMARY KEY  
        name       TEXT
        location   TEXT 
        latitude   FLOAT 
        longitude  FLOAT   

5. time - timestamps of records in songplays broken into specific units

        start_time  TIMESTAMP PRIMARY KEY, 
        hour        INT, 
        day         INT, 
        week        INT, 
        month       INT, 
        year        INT, 
        weekday     TEXT 

## To run the Python Scripts:

1. Run the create_tables.py in the terminal - this connects tot he Sparkify database, drop/create tables as appropriate.
   >> python create_tables.py 
2. Run the etl.py in the terminal - this will connect to the Sparkify database to extract/proceess datasets and load into five tables.
   >> python etl.py

### Additional files in the repository
1. sql_queries.py - defines each five tables columns with data type and primary key identification
2. etl.ipynb - jupiter notebook was used to develop this database and debugging - those code blocks were used to make etl.py script
3. test.ipynb - jupiter notebook to test the etl operations by running queries - to debug and later for analyzing the database
