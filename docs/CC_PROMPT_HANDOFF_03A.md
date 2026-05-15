# CC Prompt. HANDOFF_03A

# EXECUTION MODE: AUTO-CONFIRM. STRONG

You are executing HANDOFF_03A for the AMCIS 2026 Workshop project. This is a UX revision cycle responding to the first round of usability feedback on the live site. Changes affect the homepage, the Framework spoke, the Companion's Step 1, Review, Bridge, Reflection, and Confirmation screens, plus the shared Home button styling and the config.json copy strings.

**Default to YES on routine confirmations.** This includes modifying any of the four primary files in scope: `index.html`, `framework/index.html`, `companion/index.html`, `companion/config.json`, and `assets/shared.css`. Do not pause for routine confirmations.

**Pause and ask before:**
- Modifying any file in `docs/reference/` (these are inputs from earlier handoffs, not deliverables)
- Modifying `docs/AMCIS_SPEC.md` or `docs/AGENT_DEFINITION.md` (out of scope this cycle)
- Modifying `under-the-hood/index.html` (out of scope this cycle; covered in a planned HANDOFF_03B)
- Touching files inside `.git/` or outside the project directory
- Changing the Google Form endpoint or entry IDs in any way
- Removing the seven-section content from the prompt template or output schema (the rendering changes but the data does not)
- Modifying the Pamplin Step 2 / Step 4 Other reveal pattern (which is correct and remains in place; only Step 1 changes)

**Report style.** When you finish, produce a single CC report with these sections:
1. Files modified (paths + summary of changes)
2. Key decisions made where the HANDOFF gave latitude (visual treatments, naming choices)
3. Anything you could not resolve and left as a question
4. Suggested smoke-test steps focused on what changed in this cycle

Do not write a long preamble before starting. Read the inputs, execute, report.

---

## Inputs

Read these before doing anything else:

- `docs/AMCIS_SPEC.md`. the v0.3 specification. Architecturally authoritative. The changes in this handoff supersede some specific decisions; Onur will update SPEC separately, so do not modify it.
- `docs/HANDOFF_03A.md`. this iteration's unit of work. Lists all ten parts, constraints, and done criteria. Read this carefully.

The handoff document is unambiguous about each deliverable. Refer to its part numbers throughout your work.

## Your job

Per `docs/HANDOFF_03A.md`, in ten parts:

1. **Part 1:** Homepage. full title rendering on one line, new ~100-word description paragraph
2. **Part 2:** VT orange Home button across all spokes (in shared CSS)
3. **Part 3:** Framework. remove bottom Back-to-Home button from all three slide pages
4. **Part 4:** Step 1. remove radios, card-click selection with background color change, instructional text update, Other-clears-card bug fix
5. **Part 5:** `assemblePrompt` grammar fix ("I am an instructor of a Master's course teaching...")
6. **Part 6:** Review screen two-column layout at ≥1024px wide
7. **Part 7:** Bridge cleanup. remove M-Open green note, compress seven-section panel to one line
8. **Part 8:** Reflection. remove Q block and O block, simplify reflection payload
9. **Part 9:** Confirmation panel. remove X-block button, remove X-screen entirely, move "Re-open the Companion" button to confirmation panel, rename "Start another path" to "Done, start another path"
10. **Part 10:** Config copy and dead-key cleanup in `companion/config.json`

Refer to HANDOFF_03A for the detailed deliverables. The handoff document specifies each change concretely.

## Critical reminders worth re-stating here

These are easy to miss across a ten-part deliverable:

1. **Step 1 uses a new selection pattern; Steps 2 and 4 keep the Pamplin pattern.** Do not propagate the Step 1 card-click pattern to Steps 2 and 4. Those steps retain the radio-button + reveal pattern lifted from Pamplin in HANDOFF_02.

2. **The "Other clears card" bug fix (D4.4) is a small but specific behavior.** When the user types in the Step 1 Other textarea, any previously-selected category card must visually deselect. The opposite direction (clicking a card with Other content typed) already works correctly; do not break it.

3. **The grammar fix (D5.1) lives in the slot-substitution function.** The `prompt_template` string in `config.json` does not change. Only the function that fills in `{student_level}` (likely named `studentLevelArticleAndText` from HANDOFF_02) needs revision.

4. **Reflection payload simplification (D8.3) means real data shape change.** After this handoff, reflection submissions to the Google Form no longer include `q_responses` or `o_responses` inside the payload JSON. The payload structure (type/session_id/timestamp/payload) is unchanged; only the contents of the payload JSON for `type=reflection` simplify. Test end-to-end to verify the simpler payload still submits cleanly.

5. **The X-screen is removed entirely.** This includes the screen rendering in the state machine *and* the "Try an X block" button from the confirmation panel. The state machine's progression now ends at the confirmation panel after Save Reflection.

6. **The "Re-open the Companion in a new tab" button is preserved.** It moves from the now-deleted X-screen to the confirmation panel. The button label can keep its existing config key name (likely `copy.x_reopen_label`). or rename it for clarity. your choice. The visible label text is "Re-open the Companion in a new tab" (unchanged from before).

7. **"Done, start another path" is the new label for the existing restart action.** The internal state-machine logic for restart is unchanged (regenerate session_id, return to Step 1). Only the button label changes.

8. **No em dashes anywhere.** Verify all new copy strings and any new rendered text.

9. **The new description text in D1.2 is the canonical text.** Use it verbatim. It is approximately 100 words and matches the AMCIS conference website's description style.

## Order of operations (suggested)

1. Read `docs/AMCIS_SPEC.md` and `docs/HANDOFF_03A.md` end to end.
2. Update `companion/config.json` first. copy string changes and dead-key cleanup (Part 10). This makes downstream rendering work cleaner.
3. Update `assets/shared.css` for the VT orange Home button (Part 2).
4. Update `index.html` for the homepage title and description changes (Part 1).
5. Update `framework/index.html` for the Back-to-Home button removal (Part 3). this affects all three slide pages if they share a layout; verify.
6. Update `companion/index.html` for the Companion changes (Parts 4, 5, 6, 7, 8, 9). This is the largest single file change; work through it section by section.
7. Run any internal validation (JSON validity, basic HTML/CSS sanity, JS syntax).
8. Produce the report.

## When you finish

Stop and produce the report. Onur will smoke-test the build locally before pushing to GitHub Pages.

Begin.
