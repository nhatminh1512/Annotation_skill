# Recognition patterns

Hints for tokens, chrome, and inspector-facing names. Case-insensitive unless noted. These are not a field list to memorize.

## Dimension tokens (KEEP as Drawing)

```
diameter     ⌀|Ø|DIA\.?|DIAM
radius       R\s*\d|\br\s*\d
thread       \bM\d+(\.\d+)?(\s*x\s*\d+(\.\d+)?)?|\d+/\d+\s*-\s*\d+|#\s*\d+\s*-\s*\d+
inch         \.\d{2,4}\b
metric       \b\d+(\.\d+)?\s*(mm)?
plusminus    ±\s*\d|\+\s*0?\.\d+\s*/\s*-\s*0?\.\d+
stacked_tol  a sibling +\s*0?\.\d+  and  -\s*0?\.\d+  next to the nominal
repeat       \d+\s*X\b|4X|6X|8X
angle        \d+(\.\d+)?\s*°|\bDEG
rough        \bRa\b|\bRz\b|\bN\d+\b
chamfer      \d+\s*[xX]\s*\d+\s*°|C\s*\d
range        \d+(\.\d+)?\s*[-–]\s*\d+(\.\d+)?(\s*mm)?
length_in_desc  \d+(-\d+/\d+|\d+/\d+)?\s*(IN|MM)\s*LG
```

Group a number with sibling `+` / `-` / `±` within about 12 pt. A range is one fact.

## GD&T (KEEP as the matching GDT-* parameter)

```
position / true position     ⌖
perpendicularity             ⊥
parallelism                  ∥
angularity                   ∠
cylindricity                 ⌭
circularity / roundness      ○
flatness                     ▱ ⏥
straightness                 ⏤
concentricity                ◎
symmetry                     ≡ ⌯
circular runout / runout     ↗
total runout                 ⌰
profile of a surface         ⌓
profile of a line            ⌒
```

## Pointer captions (DROP)

```
refer tabulation
see table
see note
dimensions:\s*refer
^(length|thread length)$
```

`LENGTH` / `THREAD LENGTH` as standalone captions next to a leader — drop. A number under that leader is a separate KEEP.

## NA / empty spec values (DROP)

```
^(no additional( requirements| references)?|no exceptions|not required|n/?a|none)\.?$
```

## Title-block chrome (DROP)

Labels or values for

```
document no\.?|doc(?:ument)? number|dwg\.?\s*no
rev(?:ision)?$
size
sheet\s+\d+\s+of\s+\d+
drawn by|checked by|approved by|date
cage(?:\s+code)?
scale|weight|projection
software:
confidential|limited access
```

Do **not** drop the TITLE field (short all-caps part code such as `SCR,CPTV,SCH CAP,M8 THD,LG,SST`).

## Spec-row labels (not balloons; use to name the value)

```
part description
requirements
material
additional dimensional requirements
surface finish
requirements exceptions
cleaning requirements
packaging requirements
rohs compliance
additional requirements
reference information
```

Balloon the **value**, keep the label only as mapping context.

## Characteristic names (`specified_parameter`)

Name `specified_parameter` from this vocabulary, not a free string. This is the Specified Parameter cell on the FAI sheet — not the closed `parameter` enum, not a spec number, not a dumped list of variants.

### Feature / size (from the view geometry)

```
head diameter        head height         width across flat(s)
shank diameter       radius              length
thread size          thread length       recess type
end type             drive type          head type
shoulder length      shoulder diameter
```

A size may keep its value when the sheet prints it that way, e.g.
`Length, 1-1/2 inch`, `1/4 shoulder diameter`, `0.375 inch thread length`.

### Material / spec / requirement

```
material            surface finish      standard requirement
cleanliness         packaging           compliance required
hardness
```

Singular is canonical: `…Requirements` → `…requirement`. A long label such as
`Governing International Standard or Lam Specification` → `Standard requirement`.

### Title and tabulation

```
title                                → Title (report cell: Product description)
tabulation block / tabulation table  → Tabulation Block (Dash no.)
```

### Do not

- Merge two facts with `/` (`Thread / Length`, `Drive type / Head type`). One fact = one name.
- Use `Part Description` / `Title` as the name of a size/thread/end fact that sits inside the part-description string — name the feature (`Thread size`, `End type`).
- Leave it blank when the view shows the feature.

Prefer the shortest printed row label or column header that names **this one fact**. When the view shows a feature without a printed name, name that feature from the geometry.

## Tabulation

Headers that become column-level items

```
dash number
thread length
shoulder length
```

Do not balloon the Description column header. Parse `NNMM LG` / `N/NIN LG` out of description cells as Length.

Body dash token — emit once (first row), list the family in `notes_datum`.
Repeated identical numbers in a column — emit once.

## Normalize for dedup

```
strip Ø ⌀ DIA
.50     → 0.50
Ø.50    → 0.50
3/8-16  == 3/8-16
M8 Thread == M8
```
