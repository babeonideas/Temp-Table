# Temp-Table
Create Temp Table in SQL
## CREATING TEMPORARY TABLES

WITH 
longest_used_bike AS (
  SELECT
   bikeid,
   SUM(duration_minutes) AS trip_duration
  FROM
   bigquery-public-data.austin_bikeshare.bikeshare_trips
  GROUP BY
   bikeid
  ORDER BY
   trip_duration DESC
  LIMIT 1
)
## find station at which the longest-used bike leaves most often
SELECT
 trips.start_station_id,
 COUNT(*) AS trip_ct
FROM
 longest_used_bike AS longest
INNER JOIN
 `bigquery-public-data.austin_bikeshare.bikeshare_trips` AS trips
ON longest.bikeid = trips.bikeid
GROUP BY
 trips.start_station_id
ORDER BY
 trip_ct DESC
LIMIT 1
WITH 
longest_used_bike AS (
  SELECT
   bikeid,
   SUM(duration_minutes) AS trip_duration
  FROM
   bigquery-public-data.austin_bikeshare.bikeshare_trips
  GROUP BY
   bikeid
  ORDER BY
   trip_duration DESC
  LIMIT 1
)
## find station at which the longest-used bike leaves most often
SELECT
 trips.start_station_id,
 COUNT(*) AS trip_ct
FROM
 longest_used_bike AS longest
FULL JOIN
 `bigquery-public-data.austin_bikeshare.bikeshare_trips` AS trips
ON longest.bikeid = trips.bikeid
GROUP BY
 trips.start_station_id
ORDER BY
 trip_ct DESC
LIMIT 1
