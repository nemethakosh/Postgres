# Postgres
In this repository I build an Postgres ETL pipeline using Python

The data is saved locally, not available here.

# Postgres ETL pipeline creation manual

My name is Akos Nemeth, Data Engineer, and I provide a solution to create a Postgres ETL pipeline to analyse data. The data is available as JSON logs on user activity, as well as JSON metadata on the songs.

As a data engineer I created a Postgres database with tables designed to optimize queries on song play analysis.
I created a Start schema as database schema and built ETL pipelines for the analysis.

I used the log_data and song_data and created the following tables :
- songplays as Fact table which contains : songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent . The primary key in this table is songplay_id
- users as Dimension table which contains user_id, first_name, last_name, gender, level . The primary key in this table is user_id
- songs as Dimension table which contains song_id, title, artist_id, year, duration. The primary key in this table is song_id
- artists as Dimension table which contains artist_id, name, location, latitude, longitude . The primary key in this table artist_id
- time as Dimension table which contains start_time, hour, day, week, month, year, weekday . The primary key in this table is start_time

There are cases where there are duplicate data. For the users table I managed duplicated differently :
The 'level' field is used for free and paid services for a user. If someone subscribes by paying a fee who happened to be a free user before, I update the level of the user to paid. In the users table creation, it can be found like this : 'ON CONFLICT (user_id) DO UPDATE SET level = EXCLUDED.level' .

In the material, I created, there are two py files. First, the create_table.py file has to be run, in order for the tables to be created. The py file can be run in the terminal by writing 'python create_tables.py'.
The second step is to run the 'etl.py' file, which runs the ETL pipelines I built :  'python etl.py' . It will load the log_data and song_data JSON files.

For testing, a Jupyter notebook file can be used too. 
