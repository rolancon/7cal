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

In general, 7Cal follows the same principle: it is arranged so that the largest temporal term (the year) is placed to the left and each successively smaller term is placed to the right of the previous term. Any other term but the year is optional, the others terms are grouped into date, time, 'msecs' (milliseconds) and 'annot' (annotation) groups, and when left out the group of terms reverts to its preset default (the annot has no default, it is just the reflection of the 7Cal notation).

7Cal starts with the year. This is always a positive integer preceded by the plus '+' sign, indicating an offset from a start datetime that synchronizes it with the Gregorian calendar. 

7Cal at the datetime of the version of this write-up (see above) makes no specific demands with which datetime on the Gregorian the offset +0 synchronizes, except that it must be on a Sunday at midnight according to the UTC time zone. The author himself prefers to let 7Cal +0 start at 2017-01-01T00:00:00Z on the Gregorian calendar.

After the year are placed the date terms that signify one ore more full days. These are one or more terms, separated by a hyphen '-'.

After the days are placed the time terms that signify one ore more full seconds, which are separated from the date by an underscore '_' that mimics a space. The time terms are a separated by a colon ':'.

The terms in date and time groups are followed by the 'divider', shown as an integer number preceded by a slash '/', which divides the total number of days in a year (364) or total number of seconds in a day (86400). The term then signifies the total number of days or seconds within that division.

The number of digits in the term should always be the same as the number of digits in the divider. If needed the term must be padded with 0 or more zeroes '0' on its left side. Furthermore, there are a couple of predefined cases where the divider can be left out.

The date and time groups must always have a specific day or second at their lowest granularity, but as long as that holds the year or day can be divided multiple times, where one division follows the other and divides the remainder (the result from the previous division). So the terms are always expressed as a multiple of days or seconds.

The date group has another constraint: the year should not be divided beyond a week. Otherwise the week-based nature of the calendar would be compromised,

After the seconds is placed the term that signifies the number of milliseconds (msecs). They are separated from time in seconds with a dot '.'. The msecs are always expressed as 3 digits, ranging from 000 to 999. 

The 7Cal notation itself can be followed by an annotation (annot), which is separated from the actual 7Cal notation with the multiplication '*' sign. The annotation is the complete ISO 8601 notation in the UTC timezone (also known as Zulu time), where nothing but the msecs part is optional, only then showing when it is shown in the 7Cal notation.

(divided by a number that should always return another integer number)
The default date terms are the first day, second or msec in its specific period.

## Examples

The 'zeropoint' of 7Cal is notated as 1 term:

    +0

which is the start of the very first year on the calendar. The date, time and msecs terms are left out, so they revert to their defaults: the first day of the year, the first second of the first day and 0 msecs.

The next year on the 7Cal calendar is then:

    +1

The first day of the first year on the calendar can also be expressed more explicitly as follows, which contains a second term:

    +0-1/364

It contains a term (1) followed by a divider (/364), since there 364 days in the regular year (in the divider) and the 1st day in that period is 1 (the term).

The first day of the first week of the first year (whic is the same date again) is expressed as follows:

    +0-1/52-1/7
    
which contains 2 terms after the year: 



    +1-1-7_1/86400



    +1-1-7_1/86400.999

After the microseconds is placed the term that signifies the ISO 8601 equivalent to the full 7Cal notation.

    +1-1-7_1/86400.999*2016-31-12T00:00:01.999Z
