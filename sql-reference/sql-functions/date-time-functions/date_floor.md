# date_floor

## Description

Floor a datetime to the specified period since `0001-01-01 00:00:00`

## Syntax

```sql
DATE_FLOOR(dt, INTERVAL N type)
```

## Parameters

- `dt` : the datatime to floor. DATETIME is supported.
- `INTERVAL N type` : is const value. `N` is positive value of period. `type` must be several fixed values: YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, WEEK, QUARTER.

## Return value

Returns a value of the DATETIME data type.

## Usage notes

Period start with A.D. `0001-01-01 00:00:00`

## Examples

Example 1: Floor a datetime to the start of the five-second period.

```Plain%20Text
mysql> select date_floor('2022-04-26 19:01:07', interval 5 second);
+------------------------------------------------------+
| date_floor('2022-04-26 19:01:07', INTERVAL 5 SECOND) |
+------------------------------------------------------+
| 2022-04-26 19:01:05                                  |
+------------------------------------------------------+                                                    
```

Example 2: Floor a datetime to the start of the five-day period.

```Plain%20Text
mysql> select date_floor('0001-01-07 19:01:07', interval 5 day);
+---------------------------------------------------+
| date_floor('0001-01-07 19:01:07', INTERVAL 5 DAY) |
+---------------------------------------------------+
| 0001-01-06 00:00:00                               |
+---------------------------------------------------+
```
