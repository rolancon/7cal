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

## 7cal Notation

7cal comes with a standardized datetime notation that has been modelled on the international and Internet datetime notations [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and [RFC 3339](https://tools.ietf.org/html/rfc3339).

In general, 7cal follows the same principle: it is arranged so that the largest temporal term (the year) is placed to the left and each successively smaller term is placed to the right of the previous term. Any other term but the year is optional, and when left out the term reverts to its default.

7cal starts with the year. This is always a positive integer preceded with the plus '+' sign, indicating an offset from a start datetime that synchronizes it with the Gregorian calendar. So the start of 7cal is notated as:

    +0

7cal at the date and time of this version's write-up (see above) specifies no specific date and time on the Gregorian with which the year offset +0 synchronizes. The author himself prefers to let 7cal +0 start at 2017-01-01T00:00:00Z on the Gregorian calendar.

The next year on the 7cal calendar is then:

    +1

After the year are placed the terms that signify one ore more full days. There are one or more terms, separated by the a hyphen '-', and followed by the 'divider' shown as a slash '/' with an integer number, which signifies the number of days in that part of the year (364 divided by a number that should always return another integer number).

The first day of the next year on the calendar would thus be:

    +1-1/364
 
After the days are placed the terms that signify one ore more full seconds.

After the seconds is placed the term that signifies the number of microseconds.

After the microseconds is placed the term that signifies the ISO 8601 equivalent to the full 7cal notation.
