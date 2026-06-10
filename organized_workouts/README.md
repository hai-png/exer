# Organized Workout Matrix

## Overview

606 workout HTML files from Muscle & Strength, classified into a 6-dimensional matrix and filtered to **510 workouts** across **184 nonzero combinations**. Only genuinely problematic entries were removed — duplicates, fragments, and content that doesn't qualify as a workout program.

## Dimensions (3×4×3×3×3×7 = 2,268 total combos)

| Dimension | Values |
|-----------|--------|
| Equipment | fully equipped gym, body weight, home / small gym |
| Fitness Goal | fat loss, muscle building, general fitness, strength |
| Workout Type | full body, split, single muscle group |
| Gender | men, women, both |
| Training Level | beginner, intermediate, advanced |
| Days Per Week | 1–7 |

## Pipeline (`parse_and_organize.py`)

### Step 1 — Parse & Classify
Reads all 606 HTML files, extracts metadata, classifies into 6 dimensions.
→ **574** classifiable, **32** unclassifiable (index/listing pages with missing fields)

### Step 2 — Manual Content Filter
Applies `keep_out_filenames.json` (52 entries). Removes:
- Celebrity / movie character novelty workouts
- Military / tactical themed workouts
- Sport-specific (basketball, football, baseball, MMA)
- Gimmick workouts (100-rep shocker, fitness challenges)
- Planet Fitness–specific workouts
- Calisthenics programs
- Warm-up lists, exercise lists (not programs)
- Versioned coaching series (Core Strength Blueprint v1.1–v1.4)
- Historical figure novelty workouts
→ **52** removed, **522** remain

### Step 3 — Multi-Combo Review
Reviewed all 77 combinations with multiple workouts. **Only 12 removed** — all are genuine problems:
- **5** Cut Like Cutler cycles 2–6 (keep Cycle 1 only)
- **2** Conjugate System phases 2–3 (keep Phase 1 only)
- **4** MPP day-1/2/4/5 single-day fragments (not standalone programs)
- **1** Start from Scratch Phase 3 (keep Phase 2)
→ **12** removed, **510** final

### Final Count

| Category | Count |
|----------|-------|
| Total HTML files | 606 |
| Parse audit (unclassifiable) | 32 |
| Content filtered (manual) | 52 |
| Duplicates/fragments removed | 12 |
| **Final classified** | **510** |
| Nonzero combinations | 184 / 2,268 (8.11%) |
| Multi-workout combos | 77 |

## Output Files

```
organized_workouts/
├── workouts_classified.csv     # 510 classified workouts
├── content_filtered.csv        # 52 removed by manual review
├── duplicate_filtered.csv      # 12 duplicate/fragment removals
├── parse_audit.csv             # 32 unclassifiable pages
├── matrix_coverage.json        # 2,268 keys → workout count per combo
├── summary.json                # Aggregated stats
├── by_dimension/               # 23 CSVs (one per dimension-value)
├── by_combination/             # 184 CSVs (one per nonzero combo)
└── README.md
```

## Source Files

```
/home/user/
├── exer/                       # 606 HTML source files
├── parse_and_organize.py       # Complete pipeline (single script)
├── keep_out_filenames.json     # 52 manual filter entries
├── manual_review.json          # 119 original review decisions
└── organized_workouts/         # All outputs
```
