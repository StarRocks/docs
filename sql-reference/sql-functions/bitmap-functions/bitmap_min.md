# BITMAP_MIN

## Description

Get the minimum value in bitmap. If bitmap is null, return null. If bitmap is empty, return -1 by default.

## Syntax

`BITMAP_MIN(bitmap_expr)`

## Parameter

`bitmap_expr`: a Bitmap expression, which can be constructed by functions, such as [BITMAP_FROM_STRING](./bitmap_from_string.md).

## Return value

Returns a BIGINT value.

## Example

```Plain Text
MySQL > select bitmap_min(bitmap_from_string("0, 1, 2, 3"));
+-------------------------------------------------+
|    bitmap_min(bitmap_from_string('0, 1, 2, 3')) |
+-------------------------------------------------+
|                                               0 |
+-------------------------------------------------+

MySQL > select bitmap_min(bitmap_from_string("-1, 0, 1, 2"));
+-------------------------------------------------+
|   bitmap_min(bitmap_from_string('-1, 0, 1, 2')) |
+-------------------------------------------------+
|                                            NULL |
+-------------------------------------------------+

MySQL > select bitmap_min(bitmap_empty());
+----------------------------------+
|       bitmap_min(bitmap_empty()) |
+----------------------------------+
|                               -1 |
+----------------------------------+
```

## keyword

BITMAP_MIN,BITMAP
