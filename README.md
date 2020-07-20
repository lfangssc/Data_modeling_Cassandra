# Data_modeling_Cassandra
### Project Summary
The project was to build an Apache Casssandra database for storing the processed event data and for specific queries. There are two major parts:
1. Build an ETL pipeline to read the data from files to a csv
2. Design the schema of the tables and uplode the data accordingly

There are also query samples to verify the results at the end

### Step-by-step Coding
1. Walk through the event_data folders and find all the data files. 
2. Read every line of the data files and insert into a new table 'event_datafile_new.csv'
3. Create cluster and keyspace for the tables.
4. We know the three queries and need to create three tables accordingly. 
 - **Table one**: The query is to get the artist name, song name and song length based on session_id and item_in_session id. For this table, the session_id together with the item_in_session is unique to describle each songs. Therefore, the primary key is (sessionId, itemInSession). The query is "select artist, song, length from song_by_session_item where sessionId == * and itemInSession = * ". A sample query and results is given in the notebook.
 - **Table two**: The target is to query artist names, user names and song names using session_id, user_id. User_id is unique enough for user name but need to add item_in_session to be unique for the song and artist names. The primary key should be ((userId, sessionId), item_in_session). The query is "select artist, firstName,lastName, song from song_by_user_session where sessionId=* and userId=* ;" A sample query and results is given in the notebook.
 - **Table three**: The goal is to find which users lisented to a specific song. User Id is unique for user names. Song name also needs to be part of the primary key to allow the query and it should be the first in the primary key. Therefore, the primary key should be (song, userId). The query is "select firstName, lastName from user_by_song where song=* ;" A sample query and results is given in the notebook.
5. Finally drop the tables and close the session for the purpose of demo.
