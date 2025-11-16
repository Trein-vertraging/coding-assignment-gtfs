# GTFS Departure Board - Code Assignment

## Overview

Welcome to the GTFS Departure Board coding assignment. Your task is to build a system that processes GTFS (General Transit Feed Specification) data and provides departure information for train stations.

This assignment tests your ability to:

- Parse and process structured CSV data
- Join data across multiple datasets
- Filter and sort results based on multiple criteria
- Write clean, maintainable, and well-structured code

## The Dataset

The `data/` directory contains a mini GTFS dataset representing train schedules across major European cities. The dataset includes:

### Files

#### 1. `stops.csv`

Contains information about train stations.

- `stop_id`: Unique identifier for the stop
- `stop_name`: Human-readable name of the station

#### 2. `routes.csv`

Describes the different train routes/lines.

- `route_id`: Unique identifier for the route
- `route_short_name`: Short name (e.g., "ICE 70")
- `route_long_name`: Descriptive long name (e.g., "Hamburg -> Basel")

#### 3. `trips.csv`

Represents individual trips/journeys on a route.

- `trip_id`: Unique identifier for the trip
- `route_id`: References the route this trip belongs to
- `service_id`: References when this trip operates (see calendar_dates.csv)

#### 4. `stop_times.csv`

The scheduled arrival/departure times for each stop on each trip.

- `trip_id`: References the trip
- `stop_id`: References the stop
- `departure_time`: Time the train departs from this stop (HH:MM:SS)

#### 5. `calendar_dates.csv`

Defines on which specific dates a service operates.

- `service_id`: Unique identifier for the service calendar
- `date`: Date in YYYYMMDD format
- `exception_type`: `1` means service runs on this date

**Important**: A trip only runs on a given date if there's a matching entry in `calendar_dates.csv` for its `service_id`.

### Dataset Characteristics

The dataset is designed with realistic complexity:

- **11 stations** across Germany, Netherlands, and Switzerland
- **6 routes** (ICE, IC, and RE trains)
- **10 trips** spread across two service periods:
  - `000001`: December 2024 dates
  - `000010`: Late April/Early May 2025 dates
- **Multiple stops are shared** across different trips (e.g., Köln Hbf appears in 7 different trips)
- **Overlapping schedules** to test time-based filtering

## Your Task

Create a function/class/module that can answer the following query:

**"What trains depart from station X between time Y and time Z on date D?"**

### Requirements

Your implementation should:

1. **Load and parse** all GTFS CSV files
2. **Accept parameters**:

   - `station_name` (string): Name of the station (e.g., "Köln Hbf")
   - `from_time` (string): Start of time window (e.g., "09:00:00")
   - `to_time` (string): End of time window (e.g., "20:00:00")
   - `date` (string): Date in YYYYMMDD format (e.g., "20241216")
3. **Return** a list of departures, where each departure includes:

   - Departure time
   - Route short name (e.g., "ICE 70")
   - Route long name/destination (e.g., "Hamburg -> Basel")
   - Trip ID (for debugging/reference)
4. **Filter correctly**:

   - Only include departures from the specified station
   - Only include departures within the time window (inclusive)
   - Only include trips that operate on the specified date
5. **Sort** results by departure time (earliest first)

## Deliverables

Please provide:

1. Your implementation (in your preferred language)
2. Instructions on how to run your code
3. Example output for at least 2 of the example queries above
4. Brief explanation of your design decisions (can be comments or a short doc)

## Reference: GTFS Specification

For more information about GTFS format, see: https://gtfs.org/schedule/reference/

Note: This is a simplified subset. We're not using all GTFS files (e.g., no calendar.txt, agency.txt, etc.)T7
