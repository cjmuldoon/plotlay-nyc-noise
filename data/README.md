# Data

- `reports/noise_reports_2025.csv.gz`: every 2025 noise report to 311 after cleaning (see the main README): `request` (311's unique key), `date`, `time` (New York clock time), `how` (hour of the week, Mon 00:00 to Sun 23:00), `per_week` (1 over the times that hour came round in 2025: add them up for an average week), `type`, `descriptor`, `borough`, `cd` (community district code, by position), `lat`, `lng`.
- `tables/average_week.csv`: the city's reports in each hour of an average week, in all and by complaint type.
- `tables/hexagons_by_hour.csv`: each 1 km hexagon (`key`, as in `geometry/hexagons.*`) in each hour of the week: `places` (positions with a report) and `reports_a_week`.
- `tables/community_districts.csv`: each district's reports in an average week, in 2025, the share between 10 pm and 7 am, and its busiest hour.
- `tables/types.csv`, `tables/days.csv` (each day of 2025 against the median of the same weekday in the three weeks either side), `tables/cleaning.json` (the counts at each cleaning step).
- `geometry/`: the hexagons (GeoJSON, TopoJSON for the Power BI Shape Map) and the community districts (GeoJSON).
