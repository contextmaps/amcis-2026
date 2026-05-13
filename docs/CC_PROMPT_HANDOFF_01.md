# CC Prompt — HANDOFF_01

# EXECUTION MODE: AUTO-CONFIRM — STRONG

You are executing HANDOFF_01 for the AMCIS 2026 Workshop project. This is a substantial first-cycle build that establishes the full hub-and-spoke architecture for the workshop site.

**Default to YES on routine confirmations.** This includes: creating files, creating directories, writing content into files, overwriting empty placeholder files, running standard read/write file operations. Do not pause to ask "should I proceed?" for any of these. Proceed.

**Pause and ask before:**
- Deleting any file that already has substantive content
- Modifying anything inside `.git/`
- Touching files outside the project directory
- Resolving genuine ambiguity in the SPEC or HANDOFF that you cannot resolve by re-reading the documents
- Performing any action you cannot reverse with a single command

**Report style.** When you finish, produce a single CC report with these sections:
1. Files created (path + one-line description each)
2. Files modified (none expected, but list if any)
3. Decisions you made where the HANDOFF gave you latitude (e.g., specific copy wording, palette choices, layout details)
4. Anything you could not resolve and left as a question
5. Suggested smoke-test steps for the user to verify the build

Do not write a long preamble before starting. Read the inputs, plan briefly if needed, then execute.

---

## Inputs

Read both documents before doing anything else:

- `docs/AMCIS_SPEC.md` — the project specification, v0.2. The architectural authority.
- `docs/HANDOFF_01.md` — this iteration's unit of work. Lists all deliverables, constraints, and done criteria.

If anything in HANDOFF_01 conflicts with SPEC v0.2, **SPEC wins**. Surface the conflict in your report; do not silently resolve.

## Current state of the repository

The repository contains these files (placed by the user before you ran):

```
/.gitignore
/README.md
/assets/slide1.png       (the Old vs. New Framework slide)
/assets/slide2.png       (the Three-Phase Curricular Progression slide)
/assets/slide3.png       (the Human-AI Collaboration Loop slide)
/docs/AMCIS_SPEC.md
/docs/HANDOFF_01.md
/docs/CC_PROMPT_HANDOFF_01.md   (this file)
```

Do not modify `.gitignore`, `README.md`, the slide images, or any file in `docs/`. They are inputs and reference materials.

## Your job

Produce the six new files per HANDOFF_01 expected outputs:

```
/index.html                       (homepage)
/assets/shared.css                (design system)
/framework/index.html             (3-page slide flow)
/companion/index.html             (state machine)
/companion/config.json            (content + form + agent URL)
/under-the-hood/index.html        (stub)
```

Refer to HANDOFF_01 for the detailed deliverables. The handoff document is unambiguous about what each file contains; follow it.

## Critical reminders worth re-stating here

These are repeated from HANDOFF_01 because they are easy to miss in a long deliverable list:

1. **No em dashes in any rendered HTML content.** Buttons, descriptions, labels, status banners, panel text. None of these may contain em dashes. En dashes for date ranges are fine. Hyphens are fine. Em dashes are not. This applies only to user-visible HTML; markdown documents and code comments are unaffected.

2. **No contrastive constructions in user-facing copy.** No "not X, but Y" patterns. Direct positive claims only. Example: "The framework treats AI-era learning as occurring inside an immutable turn sequence" is correct. "The framework does not treat AI as an external tool, but as the environment" is incorrect (despite being arguably clearer). Reframe contrastive sentences as positive statements.

3. **Single HTML file per spoke.** Embed page-specific CSS and JS in the HTML file. Only `assets/shared.css` is external. No JS modules, no build step, no dependencies.

4. **The Companion state machine is the heart of this build.** It is the only spoke that has interactive logic. Spend the time on it. The other three pages are presentational.

5. **Under the Hood is a stub.** Do not draft real methodology content. The placeholder structure (six section headers, one-paragraph stubs each) is the deliverable. Anything more is out of scope for this handoff.

6. **No prior-project lineage on visible pages.** The artifact reads as freshly composed for AMCIS. No references to earlier workshops or "adapted from" framing on any rendered page. Internal comments in the HTML/JS can mention prior patterns if useful for future maintenance, but visible copy must be clean.

7. **Preserve the GPT URL and form credentials exactly.** These are in `companion/config.json`. They are operational credentials, not placeholders. Copy them verbatim from the HANDOFF document.

## Order of operations (suggested)

You can execute these in any sensible order, but this sequence minimizes risk of having to revisit completed work:

1. Read `docs/AMCIS_SPEC.md` and `docs/HANDOFF_01.md` end to end.
2. Author `assets/shared.css` (establishes the design tokens everything else depends on).
3. Author `index.html` (the homepage; exercises the shared CSS visually and locks down the header pattern).
4. Author `framework/index.html` (uses the shared CSS, the header pattern, and the slide images; relatively contained).
5. Author `companion/config.json` (defines all the content; get this right before the HTML that consumes it).
6. Author `companion/index.html` (the largest deliverable; state machine, block accents, data submission; reads from `config.json`).
7. Author `under-the-hood/index.html` (stub; quick).
8. Run any internal validation you can (syntax check, file existence, etc.).
9. Produce the report.

## When you finish

Stop and produce the report. Do not attempt to run a local web server or simulate the workshop flow yourself; the user will do end-to-end smoke testing after pushing the build to GitHub Pages.

Begin.
