# Homework1

## Overview

This repository contains answers to the first homework of the data engineering zoom camp 2024: [Homework Link](https://github.com/DataTalksClub/data-engineering-zoomcamp/blob/main/cohorts/2024/01-docker-terraform/homework.md)

## 1. Question 1. Knowing docker tags
```
docker --run -rm: Automatically remove the container when it exits
```

## 2. Question 2. Understanding docker first run
```
wheel - 0.42.0
```

## 3. Question 3. Count records

```sql
SELECT count(*) FROM public.green_taxi_trips
WHERE lpep_pickup_datetime BETWEEN '2019-09-18 00:00:00' AND  '2019-09-18 23:59:59'
AND lpep_dropoff_datetime BETWEEN '2019-09-18 00:00:00' AND  '2019-09-18 23:59:59';
```

Result: 15612

## 4. Question 4. Largest trip for each day

```sql
SELECT * FROM
(SELECT sum(trip_distance) as d1, date(lpep_pickup_datetime) as d2
FROM public.green_taxi_trips
GROUP BY date(lpep_pickup_datetime)) AS T
ORDER BY d1 DESC
```

Result: 6-09-2019

## 5. Question 5. Three biggest pick up Boroughs

```sql
SELECT Foo.d3
FROM
(SELECT sum(total_amount) as d1, "Borough" as d3
FROM green_taxi_trips JOIN zones
ON green_taxi_trips."PULocationID" = zones."LocationID"
WHERE lpep_pickup_datetime BETWEEN '2019-09-18 00:00:00' and  '2019-09-18 23:59:59'
AND "Borough" != 'Unknown'
GROUP BY "Borough") AS Foo
WHERE d1 > 50000
```

Result:
"Brooklyn"
"Manhattan"
"Queens"

## Question 6. Largest tip

```sql
ELECT "Zone" FROM zones WHERE "LocationID" = (SELECT d0 FROM
(SELECT "DOLocationID" as d0, max(tip_amount) as d1
FROM green_taxi_trips JOIN zones
ON green_taxi_trips."PULocationID" = zones."LocationID"
WHERE lpep_pickup_datetime BETWEEN '2019-09-01 00:00:00' and  '2019-09-30 23:59:59'
AND "PULocationID" = (SELECT "LocationID" FROM zones where "Zone" = 'Astoria')
GROUP BY "DOLocationID"
ORDER BY d1 DESC LIMIT 1) AS T)
```
Result: JFK Airport

## Question 7. Terraform
