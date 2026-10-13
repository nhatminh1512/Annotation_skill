# Where to put the circle

Stamp on a **copy** of the drawing. Never overwrite the source. Use the host's PDF annotation tools. If you cannot stamp, still return the JSON with `bbox` and `balloon_side`.

## Circle

- One numbered circle per KEEP. Numbers continue 1…N across pages.
- Hollow (thin stroke), high-contrast — typically red/maroon — with the balloon number inside.
- Large enough for the number, small enough not to cover nearby dimensions.

## Side and gap

`balloon_side` is `right`, `left`, `above`, or `below`. Default `right`.

Sit in **empty paper** beside the value, never on the digits.

1. Offset about 6 pt from the glyph box along the preferred side.
2. If that hits text, another balloon, or the page edge, try the other three sides at the **same** gap before moving farther.
3. Then increase the gap (about 12, 20, 32, 44 pt) and retry sides.

Close first. Far only when the neighborhood is crowded.

## Leader line

If the circle center is more than about 20 pt from the data box, draw a thin leader:

- Start at the circle edge, aimed at the data.
- End at the data-box edge. Do not run through the digits.
- Skip the leader when the circle is already close.
- Moving a circle later does not grow a leader back to the old spot.

## What the circle attaches to

- View size — the dimension group (nominal plus stacked tolerance).
- Spec row — the **value** cell, not the label.
- Tabulation — the column header or the first data cell, not every body row.
- Letter callout that stands in for a size — the callout on the view.

## Do not

- Circle chrome, NA, pointers, fragments, or every tabulated body cell.
- Draw two circles for one size.
- Place the circle on top of the glyphs it represents.
- Stamp the source file.
