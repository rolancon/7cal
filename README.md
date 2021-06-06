# 7Cal
A week-based calendar

Version: 0.1

Datetime: 2016-03-13T21:07:45Z

## Rationale

7Cal is a new completely regular calendar week-based calendar where each year always consists of exactly 52 weeks of 7 days, with the week always starting on Sunday and ending on Saturday. As a result a year always consists of exactly 364 days (52 times 7 days), starts on a Sunday and ends on a Saturday.

The Gregorian calendar has 365 days, 1 day more than 7Cal, and every 4 years February has an extra leap day on February 29. This means that over a period of 4 years it has 5 more days than 7Cal.

To sync up 7Cal with the Gregorian calendar, but still retain a fully week-based calendar, 7Cal should add an extra leap week at the end of certain regular 52-week years. 5 extra days in 4 years amounts to 35 days (5 7-day weeks) in 28 years (7 periods of 4 years).

To accommodate this 7Cal employs a 28-year long cycle of 7 'superweek' blocks that each are 4 years long, where each superweek corresponds to a regular day. So the first block of 4 years in the 28-year cycle (years 1-4) is the Sunday superweek, the last block of 4 years (years 25 through 28) is the Saturday superweek.

At the end of every 'superweekday', meaning the Monday (years 5-8), Tuesday (years 9-12), Wednesday (years 13-16), Thursday (years 17-20) and Friday (years 21-24) superweeks, an extra 7-day leap week number 53 is inserted after the end of the regular 52-week year. This leap week is not counted as an extra week of the regular year, because the regular year always has 52 weeks, but instead a special leap year is envisioned that consists of the regular year plus the leap week.

This way the new 7Cal calendar is always a fully predictable week-based calendar with no exceptions. Even leap days are methodically added in such a way that they are combined to form a leap week occurring regularly after the 5 superweekdays (but not during the 'superweekend') during a 28-year superweek cycle.

## 7Cal Notation

7Cal comes with a standardized 'datetime' (date and time) notation that has been modeled on the international and Internet datetime notations [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and [RFC 3339](https://tools.ietf.org/html/rfc3339).

In general, 7Cal follows the same principle: it is arranged so that the largest temporal term (the year) is placed to the left and each successively smaller term is placed to the right of the previous term. Any other term but the year is optional, the others terms are grouped into date, time, 'msecs' (milliseconds) and 'annot' (annotation) groups, and when left out the group of terms reverts to its preset default. The default values for the 7Cal terms are the first day of the year for the date, the first second of the day for the time and the first millisecond of the second for the msecs. The annot(ation) has no default, it is just the reflection of the 7Cal notation.

7Cal starts with the year. This is always a positive integer preceded by the plus '+' sign, indicating an offset from a start datetime that synchronizes it with the Gregorian calendar. The datetime on the Gregorian calendar that synchronizes with the +0 start offset of 7Cal is 2000-01-02T00:00:00Z.

After the year are placed the date terms that signify one ore more full days. These are one or more terms, separated by a hyphen '-'. Dates are 1-index based, meaning the lowest value is 1.

After the days are placed the time terms that signify one ore more full seconds, which are separated from the date by an underscore '_' that mimics a space. The time terms are a separated by a colon ':'. Times are 0-index based, meaning the lowest value is 0.

The terms in date and time groups are followed by the 'divider', shown as an integer number preceded by a slash '/', which divides the total number of days in a year (364) or total number of seconds in a day (86400). The term then signifies the total number of days or seconds within that division. The division should always return another integer number.

The number of digits in the term should always be the same as the number of digits in the divider. If needed the term must be padded with 0 or more zeroes '0' on its left side. Furthermore, there are a couple of predefined cases where the divider can be left out.

The date and time groups must always have a specific day or second at their lowest granularity, but as long as that holds the year or day can be divided multiple times, where one division follows the other and divides the remainder (the result from the previous division). So the terms are always expressed as a multiple of days or seconds.

After the seconds is placed the term that signifies the number of milliseconds (msecs). They are separated from time in seconds with a dot '.'. The msecs are always expressed as 3 digits, ranging from 000 to 999.

The 7Cal notation itself can be followed by an annotation (annot), which is separated from the actual 7Cal notation with the multiplication '*' sign. The annotation is the complete ISO 8601 notation in the UTC timezone (also known as Zulu time), where nothing but the msecs part is optional, only then showing when it is shown in the 7Cal notation.

## Gregorian calendar

7Cal stays in synch with the Gregorian calendar, in which every 400 years 3 leap days are cancelled.

Every 2800 years (7 blocks of 400 years) the Gregorian calendar cancels 21 leap days (7 * 3). This amounts to 3 full weeks of 7 days, spread over 100 blocks of 28 years. 7Cal cancels these 3 weeks as follows: over the course of 5 blocks of 20 times 28 years (5 blocks of 560 years), which can be thought of as the workdays of the week (Monday thru Friday), on the first, third and fifth 'workday' (Monday = 560 years till Friday = 2800 years), one leap week is cancelled. The leap week which is cancelled is the one in the middle of the cycle of 28 years (the 'Wednesday' of that cycle), so the leap week after 16 years from the start of the cycle of 28 years, or 548 years into the cycle of 560 years.

## Examples

### Year and date notation

The notation of 7Cal's 'zero point' is 1 term:

    +0

which marks the start of the very first year on the calendar. The date, time and msecs terms are left out, so they revert to their defaults: the first day of the year, the first second of the first day plus 0 msecs.

The next year on the 7Cal calendar is then:

    +1

The first day of the first year on the calendar can also be expressed more explicitly as follows, which contains a second term:

    +0-001/364

It contains a term (001) followed by a divider (/364), since there are 364 days in the regular year (as shown in the divider), and the 1st day in that period is day 1 (as shown in the term). Not that the term is padded with zeroes so that it will have the same length as the divider.

The first day of the first week of the first year (which is the same date again) is expressed as follows:

    +0-01/52-1/7
 
which contains 2 terms after the year. The 1/52 indicates the first week (with 1 in the term) of the year (with 52 in the divider since are there 52 weeks in the year). This is followed by the subdivision 1/7: the first day (1) in the week (the 7 divides the week that results from the previous divider into seven days). Not again that the first term is padded with a zero so that it will have the same length as the divider.

Note that year is 0-based offset whereas the date is a 1-based index.

Because expressing weeks and weekdays is so natural to 7Cal the dividers can be left out and the terms will have implicit defaults:

    +0-01-1

There is no cause for ambiguity because weeks always 2 digits (01-52) and days always 1 digit (1-7).

If you would like to express any another division of the year, let's say to divide the years in 13 'months' of 4 weeks or 28 days each (it would probably be more correct to call them 'moons') the divider can never be left out. Therefore to express the first day of the first week of the first month it should always be:

    +0-01/13-1/4-7

In another example, let's divide the year in 4 quarters (or 'seasons'):

    +0-1/4-01/13-7

### Time, msecs and annot notation

The time is expressed in a similar manner as the date, although times are 0-index based. The time is a day divided up to a second. The first second of the (first) day is:

    +0-01-1_00000/86400

The part after the underscore '_' is the time. This one has 86400 in the divider (after the '/'), because 1 day has 24 hours times 60 minutes times 60 seconds is 86400 seconds, of which the (zero-padded) 1 in the term is the 1st second.

To show the first second of the first minute of the first hour on a 24-hour clock we write:

    +0-01-1_00/24:00/60:00/60

Because hours, minutes and seconds are so commonly used, and because the 24-hour clock is the standard with international Internet datetimes, the dividers can be left out and the time will then have an implicit default of 24 hours, 60 minutes and 60 seconds:

    +0-01-1_00:00:00

To write the same time on a 12-hour clock we have to insert another division at the front that first divides the day in an AM and a PM part:

    +0-01-1_0/2:00/12:00:00

Hours, minutes and seconds always have 2 digits, but since one always precedes the other in a preset order no ambiguity should arise.

After the time comes the msecs term. The msecs has no divider notation.
Since 000 is the default it can always be left out as shown above. To show the zero point datetime with explicit 000 msecs:

    +0-01-1_00:00:00.000

The upper range for msecs is 999:

    +0-01-1_00:00:00.999

After the microseconds is placed the annot term that signifies the ISO 8601 equivalent to the full 7Cal notation. The zero point notation once again:

    +0-01-1_00:00:00.000*2017-01-01T00:00:00.000Z

The ISO datetime should always be written out in full. Only the msecs part is optional, and only then when it is also missing from the 7Cal notation:

    +0-01-1_00:00:00*2017-01-01T00:00:00Z
