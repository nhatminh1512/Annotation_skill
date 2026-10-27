---
name: fai-drawing-balloon
slug: fai-drawing-balloon
description: Use when ballooning, circling, or highlighting inspection characteristics on a mechanical drawing, spec sheet, or tabulation, or when building an FAI balloon list from a page. Don't use for CAD drafting, generic PDF markup, or title-block admin filing.
---

# Balloon inspection facts on a drawing

Look at the page. A balloon is one fact an inspector must verify. If it would not be its own line on an FAI report, do not circle it.

This skill is KEEP/DROP, naming, and placement. It does not depend on a particular extractor, model, or stamper. Use the host's PDF or image tools. Never overwrite the source file — write a marked copy.

## Procedure

1. Look at the page (PDF or raster). Faint and light-gray print still count. Rotated text still counts.
2. Tag every block as one of the regions below.
3. In each region, list value-bearing cells and dimension groups.
4. Run the seven questions. Stop at the first DROP.
5. Dedup across regions.
6. Split packed strings into one KEEP per inspectable fact.
7. Load `references/patterns.md`. Map each KEEP to one closed `parameter` and one `specified_parameter`.
8. Load `references/locate.md`. Stamp one numbered circle per KEEP on a **copy** of the file.
9. If the page has geometry and Drawing is empty, look again (including faint and rotated text). If still none, leave Drawing empty and continue. Do not fail the packet.
10. If an inspection or FAI sheet template is in the task, load `references/report-columns.md` and fill only the characteristic columns (A–N for CCP; equivalent fields for OTS).

When headers do not match any sample, still do steps 2–8. Do not memorize a field list from a previous packet.

Worked samples (kind of fact, not a search list) — `references/examples.md`.

## Question for every candidate

Ask, in order. Stop at the first DROP.

1. Is this administrative chrome (doc number, rev letter, sheet size, signatures, dates, logo, photo, watermark, footer, disclaimer)? → DROP
2. Is this only a label or header that names a field, with the value in a neighbor cell? → DROP the label, consider the value
3. Is this empty or a negation (`N/A`, `None`, `No`, `Not Required`, `No additional…`, `No exceptions`, `NO SUBSTITUTES` with no replacement name)? → DROP
4. Is this a pointer to another place (`Refer Tabulation`, `SEE TABLE`, `SEE NOTE`, a lone word `LENGTH` next to a table-driven dim)? → DROP
5. Is this a fragment of a larger cell (`requirements`, `references`, one word of a sentence)? → DROP; use the whole cell instead
6. Is this the same fact already kept from a better place (see Dedup)? → DROP the weaker copy
7. Otherwise, if an inspector would measure or check this value → KEEP

A number is not automatically KEEP. An unseen row label is not automatically DROP.

## Page regions

Classify each block by role, then apply the tests above.

| Region | How you recognize it | What you look for |
|--------|----------------------|-------------------|
| Title block | Bottom or corner; TITLE, DOC NO, REV, SIZE, SHEET | KEEP the human part title / short name. DROP doc no, rev, size, sheet, names, dates |
| Identity | Manufacturer, vendor, part number, customer PN | KEEP filled names and part numbers. DROP empty alternate / no-substitute lines |
| Requirements list | Label + value rows or Parameter / Specification / Standard columns | KEEP each value that states a real requirement or a cited standard. DROP the label column and NA values |
| Notes / specs paragraph | `SPECIFICATIONS`, notes, flagged sentences | KEEP each distinct requirement line. One balloon per line, not per word |
| Drawing view | Geometry, leaders, dim numbers, GD&T, thread callouts | KEEP each dimension group. DROP captions that only point at a table |
| Tabulation | Grid of dash / size / description variants | KEEP one balloon per inspectable **column**. DROP repeated body rows |
| Revision record | REV / DESCRIPTION / DATE table | DROP the whole table |

Unknown layout — still tag each block as one of the rows above. Then run the seven questions. Never invent a location outside Title, Manufacturer, Manufacturer Part Number, Drawing, Notes.

Spec and tabulation pages are table-first. Do not hunt the view for sizes that exist only as repeated body rows.

## What a KEEP looks like

- A measurable size on a view — number, Ø/R/M/thread, angle, roughness, GD&T frame — plus its own tolerance
- A title string that identifies the part
- A manufacturer or manufacturer part number that is actually filled in
- A requirement value an inspector can check (material, finish, hardness, cleaning spec, packaging rule, cited standard, ROHS when it is affirmatively required)
- One representative cell of a variant column (dash series, tabulated length)

Group glyphs that belong to one fact (nominal + plus + minus, or every token inside one table cell). `raw_text` is the full fact, not a fragment. A printed range (`6.00-6.30`) is one item. `4X` / `6X` is `places` on that item, not a second balloon. A spec number stays whole (`202-065546-001`, not `202`).

## What a DROP looks like

Chrome, labels, NA language, pointers, fragments, legal precedence paragraphs, catalog disclaimers, row-index numerals (`1.` `2.` `3.`), redline commentary (`Change to …`) unless the user asked to treat markups as requirements.

Affirmative vs negative — `ROHS Required` / `Yes` is KEEP. `ROHS Not Required` / `No` is DROP. `ASME B18.3` as a stated requirement is KEEP. `No additional requirements` is DROP. Apply the same polarity test to any new compliance or exception row.

## Dedup (same fact, several places)

Priority, highest first:

1. Dimension printed on the view
2. Spec / requirements sentence
3. Tabulation body cell

Keep the highest. Put the tabulated number on the report line if needed; do not draw a second circle on the cell.

Exceptions:

- Title stays even if the description repeats the same code
- View thread (`M8`) and spec thread line may both stay when one is Drawing and one is Notes
- A governing-standard cell (`ASME …`, internal spec number) is its own fact, not a duplicate of the requirement sentence beside it

Normalize before compare (`Ø.50` = `.50` = `0.50`, `M8 Thread` = `M8`).

## Packed strings

If a title, part-description, or spec cell packs several inspectable facts, emit one KEEP per fact. Typical packed tokens: thread size, recess / drive type, end type, head type, shoulder diameter, thread length, `NN MM LG` / `N/N IN LG` as length.

Do not balloon the whole string as one Note when those tokens are present. Do not name the split-out facts `Part Description` or `Title`.

## Tabulation

If several rows only change dash / length / description and share the same columns, those rows are one family.

- One balloon for the identity column (dash / item) — first representative, family listed in `notes_datum`
- One balloon for a text description column
- One balloon for each numeric property column (length, thread length, hex, …)
- Place the circle on the header or the first data cell — not on every row

If the view already shows that property, skip the matching numeric column (Dedup).

## Views

Every printed dimension is a candidate. Merge a number with stacked `+` / `−` / `±` next to it. Letter callouts (`"D"`) count when they stand in for a size (the number may live only in a table — still balloon the view callout, not the cell).

Captions that are only the name of a tabulated variable (`LENGTH`, `THREAD LENGTH`, `SEE TABLE`) are pointers → DROP.

## Closed enums (updated for OQA-73965)

**Parameter** (match template dropdown as closely as possible; use `Others` only when no match):

Angle, Average, Chamfer, Chemical Composition, Circularity, Concentration, Concentricity, Conductance, Conductivity, Coplanarity, Count, Counterbore, Countersink, Current, Current Density, Current Ratio, Density, Depth, Diameter, Dielectric Constant, Dielectric Loss, Dielectric Thickness, Distance, Elastic Modulus, Energy Density, Flatness, Flow Accuracy Percentage, Force, Frequency, Hardness, Height, Impedance, Inductance, Leak Rate, Line Profile, Linear Dimension, Linearity, Loss Tangent, Magnification, Mean, Median, Notes from Drawing, Parallelism, Particle Count, Perpendicularity, Planarity, Porosity, Position, Position Diametric, Position Spherical, Power, Power Density, Pressure, Purity, Radius, Resistivity Volume, Resistance, Resistivity, Standard Deviation, Surface Finish, Surface Profile, Surface Roughness, Temperature, Thermal Uniformity, Thickness, Time, Total Runout, Thread, Voltage, Weight, Width, Straightness, Cylindricity, Angularity, Symmetry, Circular runout, Spherical Diameter, Spherical Radius, Slot Length, Slot Width, Others (See Notes/Datum)

**Location**: Title, Manufacturer, Manufacturer Part Number, Drawing, Notes

**Material Condition**: RFS (default), MMC Hole, MMC Shaft, LMC Hole, LMC Shaft

Unknown parameter → `Others`. Unknown location → `Drawing`. Do not invent labels.

`specified_parameter` is the inspector-facing name (Specified Parameter cell), not the closed `parameter` enum. Vocabulary and naming rules live in `references/patterns.md`.

## Output

Return one JSON object per page, then stamp the marked copy. `bbox` is `[x0, y0, x1, y1]` tight on this fact's glyphs, origin top-left, y downward, in the same space as the page you were shown (PDF points, or 0–1 fractions of a raster). Do not invent text ids. If the host already extracted boxes with ids that match the glyphs, include those ids; otherwise omit them.

```json
{
  "page": 1,
  "items": [
    {
      "balloon": 1,
      "bbox": [0.61, 0.22, 0.68, 0.26],
      "balloon_side": "right",
      "location": "Drawing",
      "parameter": "Diameter",
      "specified_parameter": "Head diameter",
      "notes_datum": null,
      "material_condition": "RFS",
      "unit": "mm",
      "stat": null,
      "nominal": "6.3",
      "lower_tol": null,
      "upper_tol": "0.3",
      "places": null,
      "raw_text": "6.3 +0.3"
    }
  ]
}
