# PROJECT KNOWLEDGE BASE

**Generated:** 2026-02-01
**GitHub:** FrankieeW/GroupAction-Slides
**Author:** Frankie F.-C. Wang

## OVERVIEW

Beamer slides for GroupAction mathematical project. Generates presentation slides for talks, seminars, and conferences.

## STRUCTURE

```
Slides/
├── main.tex            # Main presentation
├── frames/             # Individual frames (*.tex)
├── themes/             # Beamer theme customizations
├── images/             # Graphics and diagrams
└── output/             # Generated PDF slides
```

## WHERE TO LOOK

| Task | Location | Notes |
|------|----------|-------|
| Main slides | `main.tex` | Entry point |
| Frames | `frames/` | Modular slide content |
| Themes | `themes/` | Theme customizations |
| Images | `images/` | Include graphics here |
| Output | `output/` | Generated PDF |

## CONVENTIONS

- **Beamer theme**: Use `Singapore` or `Copenhagen`
- **Frame titles**: Descriptive, consistent style
- **References**: Use `\cite{}` for citations
- **Theorems**: Use `theorem`, `definition`, `proof` environments

## ANTI-PATTERNS (THIS PROJECT)

- **Too much text** → Keep slides concise (6x6 rule)
- **Small fonts** → Use default sizes
- **Missing transitions** → Use `\pause` sparingly
- **No backup slides** → Include supplementary material

## COMMANDS

```bash
# Compile slides
pdflatex main.tex

# Use latexmk
latexmk -pdf main.tex

# Open for presentation
open main.pdf
```

## NOTES

- Greenfield: No slides yet
- Coordinate with Report for content reuse
- Use `/scientific-slides` skill for structure
