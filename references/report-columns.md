# Inspection report columns

Fill only when a template is in the task. Never write the cover sheet. Leave actuals, tooling, and conformance columns blank.

## Inspection sheet (Balloon No / Location / Parameter / …)

| Col | Field | Write |
|---|---|---|
| A | Balloon No | Sequential; same number as the PDF circle |
| B | Page | PDF page |
| C | Location | Closed enum, or the sheet's dropdown. On a sheet with a Parameter dropdown, write MFG / MPN / Specifications / Dimensions |
| D | Tool Code | Blank |
| E | Parameter/Dimension | Closed-enum name, or an allowed dropdown value. If the name is not in the list, write the Others option and put the value in Notes/Datum |
| F | Notes/Datum | Printed note / spec / datum. For a letter callout, include the size and unit (`B: 0.50"`), not the letter alone |
| G | Material Condition | MMC / LMC / RFS if shown |
| H | Specify Balloon for Size Dimensions | Blank |
| I | Unit | mm / in / deg / Ra if printed. “Unit of Measurement …” headers map here. If the column has a dropdown, write the matching token |
| J | STAT | Only if marked |
| K | Nominal | Printed at that balloon only |
| L | Lower Tolerance/Min | At that location |
| M | Upper Tolerance/Max | At that location |
| N | Places | Decimal places or `4X` / `6X` |
| O–V | LAIR, actuals, OOS, conformance, comments, internal | Blank |

## FAI data sheet (Item No / Specified Parameter / Specification)

- **Item No** — same number as the circle.
- **Specified Parameter** — `specified_parameter` from the page (printed row label, column header, or the feature seen on the view). One fact, one name. A joined `Thread / Length` label is split or dropped. Prefer `Thread size` / `End type` over `Part Description`. Map a long governing-standard heading to `Standard requirement`. Singularize `requirements`; sentence-case `Surface Finish`. Do not invent a `type`/`requirement` suffix when the page already named the fact. A Title balloon writes `Product description` here; the printed title string stays in Specification.
- **Specification** — the inspectable value. Compact a long requirement sentence to its document id. Do not glue `Thread` onto the size. Do not dump a variant list.
