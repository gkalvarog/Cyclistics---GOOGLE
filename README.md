# Cyclistics---GOOGLE

# Data Analysis Process Documentation

## Steps
- Import all the CVS files
- Add the `ride_duration` , `weekday`  and `month` columns;
- Insert `PARSE_TIME('%T', FORMAT_TIMESTAMP('%H:%M:%S', TIMESTAMP_SECONDS(TIMESTAMP_DIFF(TIMESTAMP(ended_at), TIMESTAMP(started_at), SECOND))))` to get the `ride_duration`;
- Insert `EXTRACT(DAYOFWEEK FROM started_at)` to get the `weekday`;
- Insert `EXTRACT(MONTH FROM started_at)` to get the `month`;
- Insert `ROUND(CAST(TIMESTAMP_DIFF(ended_at, started_at, second) AS INT64) / 60, 2)` to get the `ride_minutes`;
- Insert ` ROUND(CAST(TIMESTAMP_DIFF(ended_at, started_at, second) AS INT64) / 3600, 2)` to get the `ride_hours`;
- Many rows contained duration longer than 24h. Since I have no criteria of how to clean and how valid is this information, I opted for not considering trips longer than 24h (filter 1);
- Many rows contained negative time, like:
    `started_at              ended_at
    2020-02-28 10:09:43 <-> 2020-02-28 10:09:42`
  and they were removed (filter 2);
- According to an [article](www.kensbikeski.com/articles/top-fitness-in-7-hours-a-week-pg211.htm#:~:text=Pro%20cyclists%20often%20ride%2020,if%20their%20events%20are%20short.) found on Google, pro cyclists usually ride an average of 20-30 hours per week. Dividing the maximum amount in this range by an average of 5 days per week, imagining that they do not ride 15 hours per day for two days, and then, rest the remaining time, it gives us an average of 6 hours per day. Imagining that regular people are not pro bicycle riders, I decided to filter out data that contais the ride_duration time not within the range of 5 minute up to 6 hours (filter 3).
- Look for blank and null values (filter 4);
- Open a new query, and run:
```
SELECT
  ride_id,
  rideable_type,
  member_casual,
  PARSE_TIME('%T', FORMAT_TIMESTAMP('%H:%M:%S', TIMESTAMP_SECONDS(TIMESTAMP_DIFF(TIMESTAMP(ended_at), TIMESTAMP(started_at), SECOND)))) AS ride_duration,
  ROUND(CAST(TIMESTAMP_DIFF(ended_at, started_at, second) AS INT64) / 60, 2) AS ride_minutes,
  ROUND(CAST(TIMESTAMP_DIFF(ended_at, started_at, second) AS INT64) / 3600, 2) AS ride_hours,
  EXTRACT(DAYOFWEEK FROM started_at) AS weekday,
  EXTRACT(MONTH FROM started_at) AS month,
  start_station_name,
  end_station_name,
  CONCAT(start_station_name, ' to ', end_station_name) as itinerary
FROM `2020.0103`
WHERE
  PARSE_TIME('%T', FORMAT_TIMESTAMP('%H:%M:%S', TIMESTAMP_SECONDS(TIMESTAMP_DIFF(TIMESTAMP(ended_at), TIMESTAMP(started_at), SECOND)))) BETWEEN '00:05:00' AND '06:00:00'
UNION ALL
SELECT
  ride_id,
  rideable_type,
  member_casual,
  PARSE_TIME('%T', FORMAT_TIMESTAMP('%H:%M:%S', TIMESTAMP_SECONDS(TIMESTAMP_DIFF(TIMESTAMP(ended_at), TIMESTAMP(started_at), SECOND)))) AS ride_duration,
  ROUND(CAST(TIMESTAMP_DIFF(ended_at, started_at, second) AS INT64) / 60, 2) AS ride_minutes,
  ROUND(CAST(TIMESTAMP_DIFF(ended_at, started_at, second) AS INT64) / 3600, 2) AS ride_hours,
  EXTRACT(DAYOFWEEK FROM started_at) AS weekday,
  EXTRACT(MONTH FROM started_at) AS month,
  start_station_name,
  end_station_name,
  CONCAT(start_station_name, ' to ', end_station_name) as itinerary
FROM `2020.04`
WHERE
  PARSE_TIME('%T', FORMAT_TIMESTAMP('%H:%M:%S', TIMESTAMP_SECONDS(TIMESTAMP_DIFF(TIMESTAMP(ended_at), TIMESTAMP(started_at), SECOND)))) BETWEEN '00:05:00' AND '06:00:00'
UNION ALL
SELECT
  ride_id,
  rideable_type,
  member_casual,
  PARSE_TIME('%T', FORMAT_TIMESTAMP('%H:%M:%S', TIMESTAMP_SECONDS(TIMESTAMP_DIFF(TIMESTAMP(ended_at), TIMESTAMP(started_at), SECOND)))) AS ride_duration,
  ROUND(CAST(TIMESTAMP_DIFF(ended_at, started_at, second) AS INT64) / 60, 2) AS ride_minutes,
  ROUND(CAST(TIMESTAMP_DIFF(ended_at, started_at, second) AS INT64) / 3600, 2) AS ride_hours,
  EXTRACT(DAYOFWEEK FROM started_at) AS weekday,
  EXTRACT(MONTH FROM started_at) AS month,
  start_station_name,
  end_station_name,
  CONCAT(start_station_name, ' to ', end_station_name) as itinerary
FROM `2020.05`
WHERE
  PARSE_TIME('%T', FORMAT_TIMESTAMP('%H:%M:%S', TIMESTAMP_SECONDS(TIMESTAMP_DIFF(TIMESTAMP(ended_at), TIMESTAMP(started_at), SECOND)))) BETWEEN '00:05:00' AND '06:00:00'
UNION ALL
SELECT
  ride_id,
  rideable_type,
  member_casual,
  PARSE_TIME('%T', FORMAT_TIMESTAMP('%H:%M:%S', TIMESTAMP_SECONDS(TIMESTAMP_DIFF(TIMESTAMP(ended_at), TIMESTAMP(started_at), SECOND)))) AS ride_duration,
  ROUND(CAST(TIMESTAMP_DIFF(ended_at, started_at, second) AS INT64) / 60, 2) AS ride_minutes,
  ROUND(CAST(TIMESTAMP_DIFF(ended_at, started_at, second) AS INT64) / 3600, 2) AS ride_hours,
  EXTRACT(DAYOFWEEK FROM started_at) AS weekday,
  EXTRACT(MONTH FROM started_at) AS month,
  start_station_name,
  end_station_name,
  CONCAT(start_station_name, ' to ', end_station_name) as itinerary
FROM `2020.06`
WHERE
  PARSE_TIME('%T', FORMAT_TIMESTAMP('%H:%M:%S', TIMESTAMP_SECONDS(TIMESTAMP_DIFF(TIMESTAMP(ended_at), TIMESTAMP(started_at), SECOND)))) BETWEEN '00:05:00' AND '06:00:00'
UNION ALL
SELECT
  ride_id,
  rideable_type,
  member_casual,
  PARSE_TIME('%T', FORMAT_TIMESTAMP('%H:%M:%S', TIMESTAMP_SECONDS(TIMESTAMP_DIFF(TIMESTAMP(ended_at), TIMESTAMP(started_at), SECOND)))) AS ride_duration,
  ROUND(CAST(TIMESTAMP_DIFF(ended_at, started_at, second) AS INT64) / 60, 2) AS ride_minutes,
  ROUND(CAST(TIMESTAMP_DIFF(ended_at, started_at, second) AS INT64) / 3600, 2) AS ride_hours,
  EXTRACT(DAYOFWEEK FROM started_at) AS weekday,
  EXTRACT(MONTH FROM started_at) AS month,
  start_station_name,
  end_station_name,
  CONCAT(start_station_name, ' to ', end_station_name) as itinerary
FROM `2020.07`
WHERE
  PARSE_TIME('%T', FORMAT_TIMESTAMP('%H:%M:%S', TIMESTAMP_SECONDS(TIMESTAMP_DIFF(TIMESTAMP(ended_at), TIMESTAMP(started_at), SECOND)))) BETWEEN '00:05:00' AND '06:00:00'
UNION ALL
SELECT
  ride_id,
  rideable_type,
  member_casual,
  PARSE_TIME('%T', FORMAT_TIMESTAMP('%H:%M:%S', TIMESTAMP_SECONDS(TIMESTAMP_DIFF(TIMESTAMP(ended_at), TIMESTAMP(started_at), SECOND)))) AS ride_duration,
  ROUND(CAST(TIMESTAMP_DIFF(ended_at, started_at, second) AS INT64) / 60, 2) AS ride_minutes,
  ROUND(CAST(TIMESTAMP_DIFF(ended_at, started_at, second) AS INT64) / 3600, 2) AS ride_hours,
  EXTRACT(DAYOFWEEK FROM started_at) AS weekday,
  EXTRACT(MONTH FROM started_at) AS month,
  start_station_name,
  end_station_name,
  CONCAT(start_station_name, ' to ', end_station_name) as itinerary
FROM `2020.08`
WHERE
  PARSE_TIME('%T', FORMAT_TIMESTAMP('%H:%M:%S', TIMESTAMP_SECONDS(TIMESTAMP_DIFF(TIMESTAMP(ended_at), TIMESTAMP(started_at), SECOND)))) BETWEEN '00:05:00' AND '06:00:00'
UNION ALL
SELECT
  ride_id,
  rideable_type,
  member_casual,
  PARSE_TIME('%T', FORMAT_TIMESTAMP('%H:%M:%S', TIMESTAMP_SECONDS(TIMESTAMP_DIFF(TIMESTAMP(ended_at), TIMESTAMP(started_at), SECOND)))) AS ride_duration,
  ROUND(CAST(TIMESTAMP_DIFF(ended_at, started_at, second) AS INT64) / 60, 2) AS ride_minutes,
  ROUND(CAST(TIMESTAMP_DIFF(ended_at, started_at, second) AS INT64) / 3600, 2) AS ride_hours,
  EXTRACT(DAYOFWEEK FROM started_at) AS weekday,
  EXTRACT(MONTH FROM started_at) AS month,
  start_station_name,
  end_station_name,
  CONCAT(start_station_name, ' to ', end_station_name) as itinerary
FROM `2020.09`
WHERE
  PARSE_TIME('%T', FORMAT_TIMESTAMP('%H:%M:%S', TIMESTAMP_SECONDS(TIMESTAMP_DIFF(TIMESTAMP(ended_at), TIMESTAMP(started_at), SECOND)))) BETWEEN '00:05:00' AND '06:00:00'
UNION ALL
SELECT
  ride_id,
  rideable_type,
  member_casual,
  PARSE_TIME('%T', FORMAT_TIMESTAMP('%H:%M:%S', TIMESTAMP_SECONDS(TIMESTAMP_DIFF(TIMESTAMP(ended_at), TIMESTAMP(started_at), SECOND)))) AS ride_duration,
  ROUND(CAST(TIMESTAMP_DIFF(ended_at, started_at, second) AS INT64) / 60, 2) AS ride_minutes,
  ROUND(CAST(TIMESTAMP_DIFF(ended_at, started_at, second) AS INT64) / 3600, 2) AS ride_hours,
  EXTRACT(DAYOFWEEK FROM started_at) AS weekday,
  EXTRACT(MONTH FROM started_at) AS month,
  start_station_name,
  end_station_name,
  CONCAT(start_station_name, ' to ', end_station_name) as itinerary
FROM `2020.10`
WHERE
  PARSE_TIME('%T', FORMAT_TIMESTAMP('%H:%M:%S', TIMESTAMP_SECONDS(TIMESTAMP_DIFF(TIMESTAMP(ended_at), TIMESTAMP(started_at), SECOND)))) BETWEEN '00:05:00' AND '06:00:00'
UNION ALL
SELECT
  ride_id,
  rideable_type,
  member_casual,
  PARSE_TIME('%T', FORMAT_TIMESTAMP('%H:%M:%S', TIMESTAMP_SECONDS(TIMESTAMP_DIFF(TIMESTAMP(ended_at), TIMESTAMP(started_at), SECOND)))) AS ride_duration,
  ROUND(CAST(TIMESTAMP_DIFF(ended_at, started_at, second) AS INT64) / 60, 2) AS ride_minutes,
  ROUND(CAST(TIMESTAMP_DIFF(ended_at, started_at, second) AS INT64) / 3600, 2) AS ride_hours,
  EXTRACT(DAYOFWEEK FROM started_at) AS weekday,
  EXTRACT(MONTH FROM started_at) AS month,
  start_station_name,
  end_station_name,
  CONCAT(start_station_name, ' to ', end_station_name) as itinerary
FROM `2020.11`
WHERE
  PARSE_TIME('%T', FORMAT_TIMESTAMP('%H:%M:%S', TIMESTAMP_SECONDS(TIMESTAMP_DIFF(TIMESTAMP(ended_at), TIMESTAMP(started_at), SECOND)))) BETWEEN '00:05:00' AND '06:00:00'
UNION ALL
SELECT
  ride_id,
  rideable_type,
  member_casual,
  PARSE_TIME('%T', FORMAT_TIMESTAMP('%H:%M:%S', TIMESTAMP_SECONDS(TIMESTAMP_DIFF(TIMESTAMP(ended_at), TIMESTAMP(started_at), SECOND)))) AS ride_duration,
  ROUND(CAST(TIMESTAMP_DIFF(ended_at, started_at, second) AS INT64) / 60, 2) AS ride_minutes,
  ROUND(CAST(TIMESTAMP_DIFF(ended_at, started_at, second) AS INT64) / 3600, 2) AS ride_hours,
  EXTRACT(DAYOFWEEK FROM started_at) AS weekday,
  EXTRACT(MONTH FROM started_at) AS month,
  start_station_name,
  end_station_name,
  CONCAT(start_station_name, ' to ', end_station_name) as itinerary
FROM `2020.12`
WHERE
  PARSE_TIME('%T', FORMAT_TIMESTAMP('%H:%M:%S', TIMESTAMP_SECONDS(TIMESTAMP_DIFF(TIMESTAMP(ended_at), TIMESTAMP(started_at), SECOND)))) BETWEEN '00:05:00' AND '06:00:00'
```

#### Explanation of a sample of the code:
```
### FILTERS 1 and 3
WHERE
  PARSE_TIME('%T', FORMAT_TIMESTAMP('%H:%M:%S', TIMESTAMP_SECONDS(TIMESTAMP_DIFF(TIMESTAMP(ended_at), TIMESTAMP(started_at), SECOND)))) BETWEEN '00:05:00' AND '06:00:00'
```

### Then, there were still negative time values, and I filtered the NULL and negative time values:
```
SELECT *
FROM `cyclistic-2020.2020.2020`
WHERE ride_minutes > 0 AND itinerary IS NOT NULL
```

#### Explanation of the code:

```
### FILTERS 2 AND 4
SELECT *
FROM `cyclistic-2020.2020.2020`
WHERE ride_minutes > 0 AND itinerary IS NOT NULL
```

## The result of the table is:

![Sneak peak of the table]("C:\Users\k-kal\Pictures\Screenshots\Captura de tela 2024-04-26 130252.png")

### Export the table to Google Sheets and Tableau to create visualizations.

- [Google Sheets](https://docs.google.com/spreadsheets/d/1TfEBOfRaP1pF28-qd507PZ_ggplefgw8Woh2MQEUKUI/edit?usp=sharing)
- [Tableau]( https://public.tableau.com/views/cyclisticvisualizations/CNTRidesperWeekdayineachMonth?:language=en-US&:sid=&:display_count=n&:origin=viz_share_link)


Personal note: I could have included the coordinates, so I could make a geolocation analysis as well, but I will leave it for a future work.


### Now, it is time to create the presentation, responding to the questions:
  - The success of the company depends on the maximization of the number of purchases of annual plans. True or False?
  - How to convert the Casual users into Members?
  - How do Casual and Annual members use the service?
  - Why would Casual users purchase the Annual Membership?
  - How can social media be used in terms of Marketing Strategy?

  #### And the result can he seen [here](https://slidesgo.com/editor/share/9beea77e-0b6c-4abe-97a5-99110ac3de05#rs=link).
