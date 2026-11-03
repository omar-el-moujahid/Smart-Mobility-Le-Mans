# Reflections — Smart Mobility Le Mans

## 1. Easy vs. hard sub-questions
I expected the scheduled service per stop and the live delays to be easy, because the data is public. Comparing supply with demand looked harder because real ridership data is not published. Recurring patterns and prediction looked hardest because GTFS-RT has no archive.

## 2. Why the static feed does not refresh every 15 minutes
Timetables only change every few months, so most runs would give the same result.

## 3. Joining IDs with automatic types
If one file reads `stop_id` as numbers and another reads it as text, the values no longer match. The join can fail or lose rows. Reading every ID as text avoids this problem.

## 4. Per-stop vs. per-route logging
12 weeks is about 8,000 snapshots. Per-stop logging gives about 40 million rows, and per-route logging gives about 300,000 rows. I prefer per-stop data for analysis, because it shows where delays start, but the file would be huge. With per-route data, it is harder to find the stop or road section that causes a delay.

## 5. Alternative color rule
I propose three colors with fixed limits: blue for buses more than 60 seconds early, green from 60 seconds early to 180 seconds late, and red for buses more than 180 seconds late. A route that is often early would no longer look good, so the planner could review its schedule. If the whole network is late, the chart would show it clearly.

## 6. Static vs. real-time schedules
A 15-minute schedule for static GTFS is wasteful because timetables change every few months. It would mean about 2,880 runs a month with no new information. A monthly schedule for real-time data is useless because a delay loses its value within minutes, and GTFS-RT has no archive. The schedule should match how often the source changes and how long the data stays useful.

## 7. Checking one delayed route against reality

## 8. When population is a bad proxy for demand
A commune with few residents can have a large business park, so many workers travel there every day. The opposite is also possible: a commune can have many residents who mostly use cars.

## 9. My metric and a commune where it misleads
My metric is scheduled stop-visits per representative weekday, per 1,000 residents. Le Mans ranks only 10th with 153.8, while La-Chapelle-Saint-Aubin ranks 1st with 1,010.3. This looks wrong because Le Mans is the center of the network. A stop is assigned to the nearest commune center, so stops on the edge of Le Mans may be counted for smaller neighboring communes. TO COMPLETE: check one or two stops on a map and add what you found.

## 10. Aggregating stop-level delays
I would keep one row per stop, week, day type and time period, instead of one row per event. Each row would store the number of observations, the number of late observations, the total delay and the maximum delay. This gives about 216,000 rows at most instead of 40 million, and it can still show which stops have repeated delays.

## 11. Comparing my predictions with the results
TO COMPLETE AND ADJUST: Today, I could answer where scheduled service is concentrated and what the current delays are. The supply-versus-population ranking needed judgment calls because population is only a proxy and the choice of metric changes the result. Recurring delays and the best times to intervene need several weeks of history. This [matches / differs from] what I expected because [your reason].