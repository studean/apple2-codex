---
topic: "READ, DATA, RESTORE"
category: "data_storage"
statements: ["READ", "DATA", "RESTORE"]
related: ["INPUT", "GOTO"]
keywords: ["sequential data", "data pointer", "restore pointer", "constant data", "sentinel value"]
basic_variant: "applesoft"
---

# READ, DATA, and RESTORE

Use READ and DATA together when your program needs fixed values that don't
change at runtime but should be easy to update. DATA statements act as an
internal data source — READ pulls values from them sequentially, exactly as
INPUT would pull values from the keyboard. Unlike INPUT, DATA values are
embedded in the program itself and require no user interaction at runtime.

A hidden pointer tracks the current position in the DATA list. Each READ
advances the pointer by one item. RESTORE resets the pointer back to the
first item in the first DATA statement, allowing the same data to be read
multiple times.

DATA statements may appear anywhere in the program. They are ignored during
normal execution flow and only consumed by READ. Multiple DATA statements
are treated as one continuous list, read sequentially from the lowest line
number to the highest.

If READ is called when no more DATA items remain, an OUT OF DATA error
occurs. A common pattern to avoid this is to use a sentinel value — a
special marker value at the end of the DATA list that the program checks for
explicitly, signaling that all data has been consumed.

## Example: Number Guessing Game

The player tries to guess one of the numbers hidden in the DATA statements.
READ steps through each value looking for a match. If the sentinel value
-999999 is returned, all data has been exhausted and the player must try
a different number. RESTORE resets the pointer so the full list is available
for the next guess.

```applesoft
10  PRINT "GUESS A NUMBER";
20  INPUT G
30  READ D
40  IF D = -999999 THEN GOTO 90
50  IF D <> G THEN GOTO 30
60  PRINT "YOU ARE CORRECT"
70  END
90  PRINT "BAD GUESS, TRY AGAIN."
95  RESTORE
100 GOTO 10
110 DATA 1,393,-39,28,391,-8,0,3.14,90
120 DATA 89,5,10,15,-34,-999999
```

**Pattern demonstrated:** Sentinel-terminated DATA list with RESTORE-based
retry loop. The value -999999 is chosen because it is unlikely to appear as
a legitimate data value. Any value outside the expected range of your data
can serve as a sentinel.

## Key Rules

READ and DATA must be type-compatible — a numeric READ variable cannot read
a string DATA item and vice versa. String data does not require quotes in a
DATA statement unless the value contains a comma, colon, or leading/trailing
spaces.

RESTORE always resets to the very beginning of all DATA, regardless of which
DATA statement the pointer was in when RESTORE was called. There is no way in
Applesoft to restore to a specific DATA statement by address — only to the
beginning of the entire list.

DATA statements are tokenized at program entry time, not at runtime, so
spacing and capitalization in DATA values behaves differently than in other
statements. In particular, leading spaces in unquoted DATA items are ignored,
but trailing spaces are preserved.