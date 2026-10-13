# fai-drawing-balloon

Standalone Paperclip skill: find inspection facts on a mechanical drawing or spec sheet, then circle them.

Extracted from this project's `fai-tech-data` skill and KEEP/DROP rules. Independent of PyMuPDF, DeepSeek, and `annonation`. Copy this folder; do not import `.grok/skills/fai-tech-data` into Paperclip (that copy is the live classifier prompt for this engine).

## Folder

```
fai-drawing-balloon/
├── SKILL.md
├── README.md
└── references/
    ├── examples.md
    ├── locate.md
    ├── patterns.md
    └── report-columns.md
```

## Install in Paperclip

1. Copy this folder into a workspace Paperclip can see, or import it from **Skills → Add** (local path or GitHub tree URL pointing at this directory).
2. Assign it to the balloon / drawing agent (`desiredSkills`: `fai-drawing-balloon`).
3. Task that agent with a drawing PDF. Routing is the `description` on `SKILL.md`.

This engine's DeepSeek classifier still loads `.grok/skills/fai-tech-data`. Leave that path alone.
