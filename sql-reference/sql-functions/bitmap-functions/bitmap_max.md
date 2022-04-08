# BITMAP_MAX

## Description

Get the maximum value in the bitmap. If the bitmap is null, the return value is null. If the bitmap is empty, the default return value is 0.

## Syntax

`BITMAP_MAX(bitmap)`

## Parameter

`bitmap`: a bitmap, which can be constructed by functions, such as [BITMAP_FROM_STRING](./bitmap_from_string.md).

## Return value

Returns a BIGINT value.

## Example

```Plain Text
MySQL > select bitmap_max(bitmap_from_string("0, 1, 2, 3"));
+-------------------------------------------------+
|    bitmap_max(bitmap_from_string("0, 1, 2, 3")) |
+-------------------------------------------------+
|                                               3 |
+-------------------------------------------------+
MySQL > select bitmap_max(bitmap_from_string("-1, 0, 1, 2"));
+-------------------------------------------------+
|   bitmap_max(bitmap_from_string("-1, 0, 1, 2")) |
+-------------------------------------------------+
|                                            NULL |
+-------------------------------------------------+
MySQL > select bitmap_max(bitmap_empty());
+----------------------------------+
|       bitmap_max(bitmap_empty()) |
+----------------------------------+
|                                0 |
+----------------------------------+
```

## Keywords

BITMAP_MAX,BITMAP
