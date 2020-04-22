# Project: Data Modeling with Postgres

## Purpose of this database in the context of the startup, Sparkify, and their analytical goals:

Raw data is song and log datasets, which are in JSON format files and very hard to analyze quickly to answer questions like user's activities around songs.  The startup, Sparkify will run analytics on this data to find more insights on songs, artists, users. To accomplish this goal, the postgre database was developed with song and user data. This database will to optimize queries on song play analysis. 

### Example of song dataset:
artist_id	artist_latitude	artist_location	artist_longitude	artist_name	duration	num_songs	song_id	title	year
AR8IEZO1187B99055E	NaN		NaN	Marc Shaiman	149.86404	1	SOINLJW12A8C13314C	City Slickers	2008

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

## Example queries for song play analysis:

1. SELECT * FROM songplays LIMIT 5;

ongplay_id	start_time	user_id	level	song_id	artist_id	session_id	location	user_agent
1	1970-01-01 00:25:43.449658	73	paid	None	None	954	Tampa-St. Petersburg-Clearwater, FL	"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_4) AppleWebKit/537.78.2 (KHTML, like Gecko) Version/7.0.6 Safari/537.78.2"
2	1970-01-01 00:25:43.449691	24	paid	None	None	984	Lake Havasu City-Kingman, AZ	"Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1985.125 Safari/537.36"
3	1970-01-01 00:25:43.449842	24	paid	None	None	984	Lake Havasu City-Kingman, AZ	"Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1985.125 Safari/537.36"
4	1970-01-01 00:25:43.449896	73	paid	None	None	954	Tampa-St. Petersburg-Clearwater, FL	"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_4) AppleWebKit/537.78.2 (KHTML, like Gecko) Version/7.0.6 Safari/537.78.2"
5	1970-01-01 00:25:43.450034	24	paid	None	None	984	Lake Havasu City-Kingman, AZ	"Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1985.125 Safari/537.36"

2. SELECT * FROM songs LIMIT 5;

song_id	title	artist_id	year	duration
SOINLJW12A8C13314C	City Slickers	AR8IEZO1187B99055E	2008	149.86404
SOGDBUF12A8C140FAA	Intro	AR558FS1187FB45658	2003	75.67628
SORRZGD12A6310DBC3	Harajuku Girls	ARVBRGZ1187FB4675A	2004	290.55955
SONWXQJ12A8C134D94	The Ballad Of Sleeping Beauty	ARNF6401187FB57032	1994	305.162
SOFCHDR12AB01866EF	Living Hell	AREVWGE1187B9B890A	0	282.43546

## To run the Python Scripts:

1. Run the create_tables.py in the terminal - this connects tot he Sparkify database, drop/create tables as appropriate.
   root@ccdd6ebe27ae:/home/workspace# python create_tables.py 
2. Run the etl.py in the terminal - this will connect to the Sparkify database to extract/proceess datasets and load into five tables.
   root@ccdd6ebe27ae:/home/workspace# python etl.py

### Additional files in the repository
1. sql_queries.py - defines each five tables columns with data type and primary key identification
2. etl.ipynb - it was used to develop this database and debugging - those code blocks were used to make etl.py script
3. test.ipynb - to test the etl operations by running queries - to debug and later for analyzing the database
