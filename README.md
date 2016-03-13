# 7cal
A week-based calendar

Version: 0.1
Datetime: 2016-03-13T21:07:45Z

## Rationale

7cal is a new completely regular calendar week-based calendar where each year always consists of exactly 52 weeks of 7 days, with the week always starting on Sunday and ending on Saturday. As a result a year always consists of exactly 364 days (52 times 7 days), starts on a Sunday and ends on a Saturday.

The Gregorian calendar has 365 days, 1 day more than 7cal, and every 4 years February has an extra leap day on February 29. This means that over a period of 4 years it has 5 more days than 7cal.

To sync up 7cal with the Gregorian calendar, but still retain a fully week-based calendar, 7cal should add an extra leap week at the end of certain regular 52-week years. 5 extra days in 4 years amounts to 35 days (5 7-day weeks) in 28 years (7 periods of 4 years).

To accommodate this 7cal employs a 28-year long cycle of 7 'superweek' blocks that each are 4 years long, where each superweek corresponds to a regular day. So the first block of 4 years in the 28-year cycle (years 1-4) is the Sunday superweek, the last block of 4 years (years 25 through 28) is the Saturday superweek.

At the end of every 'superweekday', meaning the Monday (years 5-8), Tuesday (years 9-12), Wednesday (years 13-16), Thursday (years 17-20) and Friday (years 21-24) superweeks, an extra 7-day leap week number 53 is inserted after the end of the regular 52-week year. This leap week is not counted as an extra week of the regular year, because the regular year always has 52 weeks, but instead a special leap year is envisioned that consists of the regular year plus the leap week.

This way the new 7cal calendar is always a fully predictable week-based calendar with no exceptions. Even leap days are methodically added in such a way that they are combined to form a leap week occurring regularly after the 5 superweekdays (but not during the 'superweekend') during a 28-year superweek cycle.
