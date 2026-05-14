# CC Prompt — HANDOFF_02

# EXECUTION MODE: AUTO-CONFIRM — STRONG

You are executing HANDOFF_02 for the AMCIS 2026 Workshop project. This is a substantial cycle that replaces The Companion's placeholder content with the full AMCIS content tree, adopts working Other-UI patterns from a related project's reference code, and surfaces the seven-section output schema in the Bridge screen.

**Default to YES on routine confirmations.** This includes: copying files from `docs/reference/` to their target locations, modifying `companion/index.html`, modifying `assets/shared.css`, overwriting `companion/config.json` with the pre-built version. Do not pause for routine confirmations.

**Pause and ask before:**
- Modifying any file in `docs/reference/` (these are inputs, not deliverables)
- Modifying `docs/AMCIS_SPEC.md` (Onur maintains the SPEC separately)
- Modifying anything inside `.git/`
- Touching files outside the project directory
- Resolving any conflict between SPEC v0.3 and this handoff (SPEC wins, but surface the conflict before deciding)
- Improving on the Pamplin reference patterns (they are tested at scale; lift verbatim where they fit rather than reinventing)
- Reconstructing the new `amcis_config.json` from scratch (if you believe it has errors, surface them rather than silently editing)

**Report style.** When you finish, produce a single CC report with these sections:
1. Files created or moved (paths + one-line descriptions)
2. Files modified (paths + summary of changes)
3. Patterns lifted from `pamplin_index.html` (which CSS classes, which JS functions, where they landed)
4. Decisions you made where the HANDOFF gave latitude (visual treatment choices, copy adjustments, grammatical handling)
5. Anything you could not resolve and left as a question
6. Suggested smoke-test steps focused on what changed in this handoff

Do not write a long preamble before starting. Read the inputs, plan briefly if needed, then execute.

---

## Inputs

Read these documents before doing anything else:

- `docs/AMCIS_SPEC.md` — the project specification, v0.3. The architectural authority. Section 7 specifies the content design that this handoff encodes.
- `docs/HANDOFF_02.md` — this iteration's unit of work. Lists all deliverables, constraints, and done criteria.
- `docs/reference/pamplin_index.html` — the Pamplin Companion's working code. Reference for Other-UI patterns. Read carefully; you will be lifting CSS and JS from this file.

If anything in HANDOFF_02 conflicts with SPEC v0.3, **SPEC wins**. Surface the conflict in your report; do not silently resolve.

## Current state of the repository

After HANDOFF_01 and HANDOFF_01_PATCH executed, plus this handoff's reference files placed by Onur:

```
/index.html                              (homepage with three doors)
/assets/shared.css                       (design system)
/assets/slide1.png, slide2.png, slide3.png
/framework/index.html                    (three-slide flow)
/companion/index.html                    (state machine, placeholder content)
/companion/config.json                   (placeholder content, to be replaced)
/under-the-hood/index.html               (stub)
/docs/AMCIS_SPEC.md                      (v0.3)
/docs/HANDOFF_01.md, HANDOFF_01_PATCH.md
/docs/CC_PROMPT_HANDOFF_01.md, CC_PROMPT_HANDOFF_01_PATCH.md
/docs/HANDOFF_02.md                      (this iteration)
/docs/CC_PROMPT_HANDOFF_02.md            (this file)
/docs/reference/
  README.md
  pamplin_index.html
  pamplin_config.json
  amcis_config.json
```

The `docs/reference/` directory and all four files in it are placed by Onur before you run. Do not modify any of them. They are inputs and traceability artifacts.

## Your job

Per `docs/HANDOFF_02.md`, in nine parts:

1. **Part 1:** Verify the reference files in `docs/reference/` are present
2. **Part 2:** Copy `docs/reference/amcis_config.json` to `companion/config.json` (overwriting the placeholder)
3. **Part 3:** Adopt the Pamplin Step 1 Other panel pattern (always-visible textarea, amber tint, live counter, type-to-select) in `companion/index.html`
4. **Part 4:** Adopt the Pamplin Step 2/Step 4 Other reveal pattern (radio + reveal textarea) in `companion/index.html`
5. **Part 5:** Update the `assemblePrompt` logic to handle the new template's conditional blocks and slot substitutions
6. **Part 6:** Implement the Step 1 Other → Step 2 elaboration flow (when Step 1 Other is selected, Step 2 is a free-text elaboration screen)
7. **Part 7:** Surface the seven-section output schema in the Bridge screen
8. **Part 8:** Render boundary statements for the three categories that have them
9. **Part 9:** Verify homepage door descriptions are not stale (minor tweaks if needed)

Refer to HANDOFF_02 for the detailed deliverables. The handoff document is unambiguous about what each part contains.

## Critical reminders worth re-stating here

These are repeated from HANDOFF_02 because they are easy to miss in a long deliverable list:

1. **The new `amcis_config.json` is pre-built and validated.** Copy it directly to `companion/config.json`. Do not reconstruct it. If you believe it has errors, surface them in your report rather than silently editing.

2. **Lift Pamplin patterns verbatim where they fit.** The Pamplin reference is tested at scale. Do not improve on its patterns — improvements risk regressions. Specifically: lift CSS classes (`.tri-group-other`, `.plib-textarea`, `.plib-counter`, `.tri-other-input-wrap`), lift color tokens (`--c-r-bg`, `--c-r-border`, `--c-r-id`), lift the `assemblePrompt` regex and slot-substitution loop.

3. **Step 1 and Step 2/4 use different Other-UI patterns by design.** Step 1's Other is a peer panel with always-visible textarea (the layout is a grid). Step 2 and Step 4 Other is a radio + reveal (the layouts are vertical lists). Do not unify them. Both are appropriate to their parent layout.

4. **Step 1 Other → Step 2 elaboration flow is the most easily-missed pattern.** When the user picks Step 1 Other, Step 2 has no category-specific tree to show; instead, render a single textarea elaboration screen. Step 4 in this branch uses the `default` materials fallback.

5. **No em dashes in any rendered HTML content.** No contrastive constructions in any user-facing copy. Apply to all new code paths, including the boundary statements and the seven-section schema display.

6. **Preserve all existing data-submission logic.** Google Form endpoint and entry IDs unchanged. Payload format unchanged in structure (type/session_id/timestamp/payload); the payload's contents reflect the new Step 3 fields and prompt template output.

7. **Do not modify the Framework, Under the Hood, or homepage structure.** Only door descriptions on the homepage are in scope, and only if they need updates. The other spokes are stable from HANDOFF_01.

## Order of operations (suggested)

1. Read all three input documents end-to-end.
2. Verify reference files are present in `docs/reference/`.
3. Copy `amcis_config.json` to `companion/config.json` and validate it loads cleanly.
4. Modify `assets/shared.css` to add the Other-panel color tokens and `plib-*` primitives (if not already adequate from HANDOFF_01).
5. Modify `companion/index.html` for the Step 1 Other panel.
6. Modify `companion/index.html` for Steps 2 and 4 Other reveal.
7. Modify `companion/index.html` for the Step 1 Other → Step 2 elaboration branch.
8. Modify `companion/index.html` for the boundary statements.
9. Modify `companion/index.html` for the seven-section schema in the Bridge screen.
10. Modify `companion/index.html`'s `assemblePrompt` function for the new template structure.
11. Verify homepage door descriptions; tweak if needed.
12. Run any internal validation (JSON validity, CSS sanity, JS syntax).
13. Produce the report.

## When you finish

Stop and produce the report. Onur will smoke-test the build locally before pushing to GitHub Pages.

Begin.
