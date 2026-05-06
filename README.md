# Build-a-Belt

Single-file browser prototype for a 6-row conveyor belt assembly challenge. Built in partnership with Intralox for training and product education.

The main artifact is:
- Belt_v3-6.html (v3.6 with v22 visual enhancements)

## Purpose

This prototype simulates an operator workflow where a learner:
1. Builds six rows from module parts.
2. Verifies sequence and edge orientation.
3. Pulls adjacent correct rows together.
4. Inserts rods through joined boundaries.
5. Submits results via copy-to-clipboard.

It is designed for training-style practice with immediate feedback and a timed, scored run.

## Current Scope

Included:
- Full assembly interaction loop with optimized performance.
- Drag/drop module placement with validation.
- Edge rotation checks and sequence validation.
- Row merging and rod insertion with visual feedback.
- Timer, score, stars, and personal-best tracking (local storage).
- Copy-to-clipboard run submission text.
- Optional tutorial and name-gate UX.
- **Material system**: Module plastic presets, module colour, rod material selection.
- **Visual enhancements (v22)**: Shimmer sweep, chevron hints, grip handles, score pop badges, rod spark effects.
- **Sound effects**: Configurable WebAudio feedback with toggle control.
- **Desktop-only notice**: Recommendation message for optimal experience.
- **Intralox branding**: Company logo and header integration.
- **Practice tools mode**: Test-mode indicator and accessibility features.

Explicitly not included (currently purged):
- Prefilled form submission flow.
- Leaderboard modal and feed integration.

## Run Instructions

1. Open the HTML file in a modern desktop browser.
2. Enter a name/date if desired.
3. Build rows in target sequence.
4. Merge adjacent correct rows.
5. Insert rods until complete.
6. Click Submit time to copy result text.

No build system, package manager, or server is required.

## Tech Stack

- Plain HTML, CSS, and JavaScript in one file.
- No external runtime dependencies.
- SVG module art embedded as data URIs.
- Local persistence via localStorage.

## Gameplay and Validation Rules

### Visual Enhancement System (v22)

The prototype now includes a robust feature-flag system controlling all visual enhancements:
- **SHIMMER**: One-shot glint animation when a row is completed correctly.
- **CHEVRONS**: Animated ▲▲ nudge arrows displayed in gaps between adjacent complete rows.
- **SCORE_POPS**: Floating +/− badges that rise and fade from the cursor on score changes.
- **ROD_SPARK**: Radial burst effect when a rod is fully seated into a boundary.
- **SLIPPERY_DRIFT**: Optional side-to-side drift animation for incomplete rows (disabled by default).
- **SFX**: WebAudio-based feedback sounds with user-configurable toggle.

All features can be toggled via the `FEAT` object in the JavaScript section (search "FEAT FLAGS").

### Row rules
- Each row has a required pattern (E9, I9, E24 module combinations).
- Placement is validated in sequence order.
- Edge modules must face outward (rotation-dependent).

### Merge rules
- Only adjacent row groups can merge.
- Both groups must be fully correct before merge is accepted.
- Merge failures apply penalties and provide status feedback.

### Rod rules
- Rods can only be inserted into valid joined boundaries.
- Partial insertion applies a penalty.
- Full insertion marks boundary complete.
- Completion triggers result summary.

## Scoring Model

High-level model:
- Base score starts at a fixed value.
- Errors and rejected actions subtract points.
- Completion speed adds a bonus (within defined time window).
- Stars are assigned from run time + error count.
- Autocomplete/practice mode applies penalties and caps stars.

Primary score components are configured as constants in the script section.

## Data and Persistence

localStorage keys used by the prototype include:
- Personal best record
- SFX preference
- Belt color preference
- Rod color preference
- Module material preset (plastic type)
- Module colour choice
- Rod material preset
- Tutorial visibility preference
- Autocomplete unlock state

No network calls are required for the current run flow. All user preferences persist across sessions.

## File Structure (Single File)

The file is logically organized as:
1. CSS styles and animations.
2. App markup (header, controls, tray, rows, results, modals).
3. Main script IIFE with:
   - Constants and state
   - Feature/helper utilities
   - Row build/validation logic
   - Merge logic
   - Rod threading logic
   - Timer and scoring
   - Submit/copy behavior
   - Event wiring

## Maintenance Guide

### Safe edits
- Text copy, labels, and status messages.
- Color/theme defaults (CSS root variables).
- Scoring constants and star thresholds.
- Tutorial slide content.
- Visual enhancement feature flags (FEAT object).
- Sound effect tones and parameters.

### Higher-risk edits
- Drag/drop and merge flow logic.
- Rod insertion state machine.
- Timer/scoring side effects.
- Pattern rules and edge-orientation checks.
- Material selector configuration and conditional UI logic.
- Animation keyframe timing and effects integration.

When editing high-risk areas, test complete runs end-to-end. Visual enhancement changes should be tested both with features enabled and disabled.

## Suggested Test Checklist

1. Fresh load starts with clean board and disabled submit.
2. Correct row placement transitions to complete state.
3. Incorrect placement is rejected with penalty feedback.
4. Edge orientation errors are detected.
5. Adjacent correct rows merge; invalid merges fail safely.
6. Rod insertion supports both full and partial outcomes.
7. Completion opens results with valid time/score/stars.
8. Submit time copies share text successfully.
9. Personal best updates only on eligible runs.
10. Reload preserves preferences but not in-progress board state.

## Version Notes

### v3.6 (Current - v22 Visual Enhancements)
- Major visual upgrade with feature-flag-controlled animations and effects.
- Integrated Intralox branding and material system.
- Added sound effects with WebAudio and user toggle.
- Material presets for module plastic, module colour, and rod material.
- Enhanced UX with chevron hints, shimmer sweeps, score pop badges, and rod sparks.
- Desktop-only notice for optimal experience guidance.
- Practice tools indicator in header.

### Previous versions
This readme reflects the post-v22 enhancements state. Earlier versions (including v21) had the core assembly loop without the visual enhancement system, material selector, or integrated branding.

## Ownership Notes

If this file is moved into a dedicated GitHub repository, rename this document to README.md at the repository root for standard discoverability.
