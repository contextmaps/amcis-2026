# CC Prompt: HANDOFF_03C

# EXECUTION MODE: AUTO-CONFIRM: STRONG

You are executing HANDOFF_03C for the AMCIS 2026 Workshop project. This is a small, CSS-only polish handoff: four visual fixes (one of which is a deliberate no-op) across the homepage and the Under the Hood spoke. This is the final cleanup before the draft site is shared with external reviewers.

**Default to YES on routine confirmations.** This includes modifying `index.html`, `under-the-hood/index.html`, and `assets/shared.css` for the CSS changes described in the handoff.

**Pause and ask before:**
- Making any HTML structure change (this handoff is CSS-only; if a fix seems to need HTML or JS changes, stop and surface it)
- Making any JavaScript change
- Modifying `framework/index.html`, `companion/index.html`, or `companion/config.json`
- Modifying anything in `docs/`
- Modifying image files
- Touching files inside `.git/` or outside the project directory
- Adding any dependency

**Report style.** When you finish, produce a single CC report with:
1. Files modified (paths + summary of CSS changes)
2. For each fix: what CSS changed and in which file
3. The Fix 4 max-height value chosen and the reasoning
4. Confirmation that the Framework spoke's slide sizing was not touched
5. Anything you could not resolve CSS-only
6. Suggested smoke-test steps

Do not write a long preamble. Read the inputs, execute, report.

---

## Inputs

Read these before doing anything else:

- `docs/AMCIS_SPEC.md`: the v0.3 specification, for project context.
- `docs/HANDOFF_03C.md`: this iteration's unit of work. Read it fully. It describes all four fixes precisely.
- `index.html`: the homepage. Fixes 1 and 2 apply here (or in shared.css).
- `framework/index.html`: read this to understand the current slide-viewer sizing, so Fix 4 can be made on the Under the Hood viewer without disturbing the Framework viewer.
- `under-the-hood/index.html`: Fix 4 applies here (or in shared.css).
- `assets/shared.css`: the shared design system; some of the relevant rules may live here.

## Your job

Per `docs/HANDOFF_03C.md`, four fixes:

- **Fix 1:** Center-align the homepage header block (title, conference line, byline) over the three door panels.
- **Fix 2:** Set the homepage description paragraph's container to the width of the three-panel row, keeping the paragraph text left-aligned within that centered container.
- **Fix 3:** No-op. The banner title stays short ("Teaching Inside the Thread"). No change. Listed only so fix-numbering matches the review notes.
- **Fix 4:** Constrain the Under the Hood slide images by height instead of width, so the image plus caption plus Previous/Next buttons all fit within a standard viewport. Does NOT apply to the Framework spoke.

The handoff document gives the precise target state, constraints, and done criteria for each fix. Follow it.

## Critical reminders

1. **CSS-only.** No HTML structure changes. No JavaScript changes. No content or config changes. If any fix appears to need an HTML or JS change, stop and surface it rather than proceeding.

2. **Fix 3 is a deliberate no-op.** Do not change the banner title. It stays "Teaching Inside the Thread" (short form). The handoff lists Fix 3 only so the numbering matches the review notes that prompted this work.

3. **Fix 4 is Under-the-Hood-only.** The Framework spoke's slide sizing must not change. The Framework slides have a wider aspect ratio and currently fit correctly. If the two viewers share CSS (HANDOFF_03B lifted the Framework pattern for Under the Hood), Fix 4 must be scoped with an Under-the-Hood-specific selector or wrapper class so the height constraint does not reach the Framework viewer.

4. **Fix 2 keeps the paragraph text left-aligned.** The paragraph's *container* is widened to the panel-row width and centered on the page, but the *text* inside stays left-aligned. Do not center-align the paragraph text.

5. **Tune Fix 4's max-height by testing.** Use a viewport-relative unit (vh) rather than a hardcoded pixel height. Pick a value where the image, caption, and nav buttons all fit at a standard 1080p viewport.

6. **Two files expected, possibly three.** `index.html` for Fixes 1 and 2, `under-the-hood/index.html` for Fix 4, or `assets/shared.css` if the relevant rules live there. Determine where the current rules are and edit accordingly.

## Order of operations (suggested)

1. Read the handoff and the four relevant files.
2. Locate where the homepage header and three-panel-row CSS lives (page file or shared.css). Note the panel-row container width.
3. Apply Fix 1 (center the header block) and Fix 2 (paragraph container width + left-aligned text).
4. Read the Framework viewer's slide-sizing CSS. Read the Under the Hood viewer's. Determine whether they share rules.
5. Apply Fix 4 to the Under the Hood viewer only, scoped so it does not affect the Framework viewer. Tune the max-height value.
6. Verify all changes are CSS-only.
7. Produce the report.

## When you finish

Stop and produce the report. Onur will smoke-test locally before pushing to GitHub Pages.

Begin.
