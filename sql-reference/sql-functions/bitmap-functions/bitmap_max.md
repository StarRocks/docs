# bitmap_max

## description

### Syntax

```Haskell
BITMAP BITMAP_MAX(BITMAP bitmap)
```

Get the maximum value in bitmap. if bitmap is null, return null. if bitmap is empty, return 0 by default.

## example

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

## keyword

BITMAP_MAX,BITMAP
