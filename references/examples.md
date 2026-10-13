# Worked packets (not rules)

These packets show the *kind* of fact to keep. They are not a field list to memorize, and the numbers are not a search list for other drawings.

Redline text `Change to …` on source-control is human markup. Do not emit it as an item.

`specified_parameter` is the inspector-facing name, read from the page: `Recess type`, `Thread size`, `Cleaning requirement`, `Head diameter`, `Width across flats`. Not a spec number, not `-04|-06|…`.

## Source control — 752-109865-001 (1 page)

KEEP 10

1. Title `PIN,STOP,3/8-16`
2. Manufacturer `MASTERLINE DESIGN`
3. Manufacturer Part Number `HB-6-N`
4. Material `12L14 CRS`
5. Finish `Nickel Plate`
6. Thread `3/8-16`
7. Hardness `56-60 HRC`
8. View D (table `.50` is the report value; balloon the view callout, not the cell)
9. View C + `+.003 / -.000` (table `.250`)
10. View B (table `.50`)

DROP Refer Tabulation, D/B/C/T cells, T THREADS caption, G, DOC NO, rev table, NO SUBSTITUTES, catalog disclaimer.

## Spec 11-row — 21-041906-XX

Sheet 1 KEEP Title, Recess `Hex Socket Drive`, Thread `10-32`, Requirements `ASME B18.3`, Material, Finish, Cleaning, Packaging, ROHS `Required`.

DROP empty rows, DOC NO, and the Description column header.

Sheet 2 KEEP Dash column once and the tabulated length.

## OTS — 720-C07055-XXX

Sheet 1 KEEP Title plus every real Specification cell and every Governing cell that is not N/A (ASME / internal spec numbers).

DROP Additional / ROHS No / exceptions No / Precedence / N/A.

Sheet 2 KEEP Dash column, Shoulder Length column.

## Spec 11-row — 728-283558-XXX

Sheet 1 KEEP 6 — Title, Description, Material, Finish, Cleaning, Packaging.

DROP ROHS `Not Required` and every No-additional row. DROP DOC NO.

Sheet 2 KEEP Dash, length from the description (`16MM LG`), Thread Length `10`, view M8 / 6 / 13 / 8 / r0.3 / 6.3.

DROP the Description column header. DROP captions LENGTH and THREAD LENGTH. DROP extra dash rows.

The part-description string packed `M8 Thread` and `Flat End` — those are separate KEEP items (`Thread size`, `End type`), not `Part Description`.
