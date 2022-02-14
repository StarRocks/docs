# bitmap_min

## description

### Syntax

```Haskell
BITMAP BITMAP_MIN(BITMAP bitmap)
```

Get the minimum value in bitmap. if bitmap is null, return null. if bitmap is empty, return -1 by default.

## example

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
