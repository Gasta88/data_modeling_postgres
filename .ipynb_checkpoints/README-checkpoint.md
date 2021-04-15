# Data Modeling in Postgres - FGastaldello submission

## Purpose/Goals

This project is used as an exercise to verify the concepts learned in the first module of the Data Engineering Nanodegree on Udacity.

*Sparkify* is a music app with a Postgres database underneath to collect data related to songs listened and respective logs.
A data model for *sparkifydb* database has been implemented conceptually with the definition of fact and dimension tables. The ETL pipeline extracts the information from JSON file and prepare the data via Python before it is imported inside the database.

## Schema design

![image info](./imgs/EDR.png)

### Main design

The databse `sparkifydb` holds information about songs played and relative metadata. The Star schema is made of:

 - *fact table*: `songplays`
 - *dimension tables*: `songs`, `users`, `time` and `artists`
 
The creation/deletion of tables is done via the `create_tables.py`, based on the `sql_queries.py` script.
Along with `CREATE TABLE`, `DROP TABLE` and `INSERT` statements, the script has a `song_select` query that can retrieve the *song_id* and *artist_id* for the `songplays` table.

The ETL pipeline reads files inside the `/data` folder, which is organized to hold song data in `/data/song_data` and metadata in `/data/log_data`.
All files are in JSON format and these are manipulated via the `etl.py` script by using Pandas, a popular library for data manipulation for Python.

## How to run the project

1. On console run `python create_tables.py`. Database and empty tables should be ready.
2. After that run `python etl.py` to populate the tables with song and log data.
3. Use the `test.ipynb` to quickly inspect the database content.

## Query examples

Queries to check the number of user for each gender:

`SELECT COUNT(*) FROM users WHERE gender = 'M';`

`SELECT COUNT(*) FROM users WHERE gender = 'M';`

Query to check the weekday with highest number of songs played:

`SELECT weekday , COUNT(*) FROM time GROUP BY weekday ORDER BY 2;`

Query to retrieve the tile of all songs that last more than the avarage duration:

`SELECT title FROM songs WHERE duration >= (SELECT AVG(duration) FROM songs);`