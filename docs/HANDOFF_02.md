# HANDOFF_02 — Content swap, Other UI adoption, seven-section schema surfacing

**Project:** AMCIS 2026 Workshop — Teaching Inside the Thread
**Spec reference:** `docs/AMCIS_SPEC.md` v0.3
**Workshop date:** 2026-08-20
**Cut:** Substantial — replaces the Companion's placeholder content with the full AMCIS content tree, adopts the Pamplin Other-UI patterns directly, and surfaces the seven-section output schema in the Bridge screen

---

## Goal of this iteration

Take The Companion from a working skeleton with placeholder content to a fully content-loaded, professionally interactive triage interface. Three coordinated changes:

1. **Replace `companion/config.json`** with the full AMCIS content tree (7 categories, 42 Step 2 items, 42 Step 4 materials trees, revised Step 3 schema, locked copy strings, updated prompt template).

2. **Adopt the Pamplin Other-UI patterns** by lifting the working code directly from the reference file `docs/reference/pamplin_index.html`. Two distinct patterns:
   - **Step 1 Other:** always-visible textarea inside an amber-tinted panel that sits in the grid as a peer to the category cards. Live character counter. Type-to-select interaction.
   - **Step 2 and Step 4 Other:** reveal-on-select pattern. Other is one of the radio choices; selecting it reveals a "Describe in your own words" textarea below.

3. **Surface the seven-section output schema** in the Bridge screen so faculty see what response shape they're requesting before pasting into the GPT.

Plus a small update to the prompt template that names the seven sections explicitly.

---

## Current state of the repository

After HANDOFF_01 and HANDOFF_01_PATCH:

```
/index.html                              (homepage with three doors)
/assets/shared.css                       (design system)
/assets/slide1.png, slide2.png, slide3.png
/framework/index.html                    (three-slide flow)
/companion/index.html                    (state machine, placeholder content)
/companion/config.json                   (placeholder content)
/under-the-hood/index.html               (stub)
/docs/AMCIS_SPEC.md                      (will be v0.3 after this handoff)
/docs/HANDOFF_01.md                      (executed)
/docs/HANDOFF_01_PATCH.md                (executed)
/docs/CC_PROMPT_HANDOFF_01.md            (executed)
/docs/CC_PROMPT_HANDOFF_01_PATCH.md      (executed)
```

For this handoff, two new reference files arrive in `docs/reference/`:

```
/docs/reference/pamplin_index.html       (the Pamplin Companion's working code)
/docs/reference/pamplin_config.json      (the Pamplin config for structural reference)
```

These reference files are inputs CC will read but not modify. They are recorded in git for traceability.

---

## Inputs

**The new `companion/config.json` content** is provided pre-built as `docs/reference/amcis_config.json`. CC copies this file to `companion/config.json` rather than reconstructing it. This eliminates the risk of CC making errors in a ~1500-line content file.

**The Pamplin reference implementation** lives at `docs/reference/pamplin_index.html`. CC reads this file to understand the Other-UI patterns and lifts the relevant code into `companion/index.html`.

**SPEC v0.3** (`docs/AMCIS_SPEC.md`) is the architectural authority. §7 specifies the content design that the new config encodes.

---

## Deliverables

### Part 1 — Reference files placed in repo

**D1.1** Place the new reference files in `docs/reference/`:

```
docs/reference/
├── pamplin_index.html              (the Pamplin Companion's working code, for reference)
├── pamplin_config.json             (the Pamplin config, for structural reference)
└── amcis_config.json               (the new AMCIS content tree, ready to be copied to companion/config.json)
```

These files are placed by Onur before CC runs. CC does not author them; CC only reads them.

A short `docs/reference/README.md` explains what these files are:

```markdown
# Reference files

These files are working artifacts from a related project and the pre-built AMCIS content config. They are read by Claude Code during handoff execution and preserved in git for traceability.

- `pamplin_index.html` — the tested Companion interface from a related project; reference for Other-UI patterns
- `pamplin_config.json` — the corresponding config; reference for structure
- `amcis_config.json` — the pre-built content tree for AMCIS; copied to `companion/config.json` during HANDOFF_02

These files are not part of the deployed site.
```

### Part 2 — Replace companion/config.json

**D2.1** Copy `docs/reference/amcis_config.json` to `companion/config.json`. Overwrite the existing placeholder.

The new file is structurally compatible with the existing state machine's config-loading logic, with these extensions:

- **`step1.items`** is now an object keyed by category id, with `label` and `description` fields per category
- **`step1.order`** is an array preserving display order
- **`step1.boundary_statements`** is an object mapping certain category ids to "Best for..." strings; the three categories without a statement (`course_design`, `teaching_is_concepts`, `engagement_protocols`, `assessment_integrity`) have no entry and render no boundary statement
- **`step2`** is an object keyed by Step 1 category id, with arrays of items; each items array ends with an `other` entry
- **`step3.fields`** is an array of field definitions with types and options (replacing the previous flat `departments`/`student_levels`/etc. arrays)
- **`step4`** is keyed by Step 1 category id, with sub-keys per Step 2 item id; each leaf is an array of materials items
- **`step4.default`** provides a fallback materials list for the Step 1 Other path
- **`step4_other`** at top level provides max_chars for the Step 4 Other textarea
- **`reflection`** contains the textarea config plus the Q and O block content
- **`output_schema`** is a new array listing the seven output sections (used by the Bridge screen UI)
- **`prompt_template`** uses Handlebars-style conditional blocks (`{{#if field}}...{{/if}}`) and slot substitutions (`{slot_name}`); the assemblePrompt logic must handle both forms

**D2.2** Verify the existing state machine in `companion/index.html` still loads and renders correctly against the new config structure. The state machine inherits patterns from HANDOFF_01; this handoff modifies it as described in Parts 3–6 below to match the new config.

### Part 3 — Adopt Pamplin Step 1 Other-UI pattern

**D3.1** Read `docs/reference/pamplin_index.html` to understand the existing pattern. Key elements:

- CSS classes: `.tri-group`, `.tri-group-other`, `.tri-group-label`, `.plib-textarea`, `.plib-counter`
- Color tokens: `--c-r-bg`, `--c-r-border`, `--c-r-id` (the amber/warm-tan tint that distinguishes the Other panel)
- Step 1 rendering logic at approximately lines 460-518 of `pamplin_index.html`
- The textarea is **always visible inside the Other panel** from first load
- A live character counter ticks up as the user types
- Clicking anywhere in the Other panel focuses the textarea
- Typing in the textarea automatically selects Other (transferring selection from any previously-selected card)
- Selecting a different card deselects Other but does not clear the textarea content
- Continue is disabled when Other is selected and the textarea is empty or whitespace-only

**D3.2** Implement this pattern in `companion/index.html` for Step 1. The grid layout: Step 1 renders 7 category cards plus the Other panel as the 8th cell. On wide viewports, the grid is 4 columns × 2 rows. On narrower viewports it collapses gracefully.

Lift the CSS for `.tri-group-other`, `.plib-textarea`, and `.plib-counter` from `pamplin_index.html` into `assets/shared.css` (or the embedded `<style>` block of `companion/index.html`, whichever is more appropriate based on whether the styles are Companion-specific or genuinely shared).

Use the color tokens from the Pamplin reference, adapted to AMCIS's existing palette if there's a conflict. The amber-tan tint should land approximately as it does in the Pamplin reference: a subtle warm background with a slightly more saturated border, clearly distinguishable from the neutral category cards without being jarring.

### Part 4 — Adopt Pamplin Step 2 and Step 4 Other reveal pattern

**D4.1** For Steps 2 and 4, Other is one of the radio-style choices in the vertical list. The pattern in `pamplin_index.html` at approximately lines 575-625 (Step 2) and 790-810 (Step 4):

- Other appears as the last choice in the list, with the same radio button styling as the other options
- Selecting Other reveals a labeled textarea below the list: "Describe in your own words"
- Selecting any other option hides the textarea and clears its content
- The textarea uses `plib-textarea` with `maxlength` set per the config's `max_chars` field
- Continue is disabled when Other is selected and the textarea is empty

**D4.2** Implement this pattern in `companion/index.html` for Steps 2 and 4. Use the `.tri-other-input-wrap` and `.tri-other-input-wrap.hidden` classes from the Pamplin reference for the reveal/hide behavior.

The Step 2 and Step 4 Other interactions are visually distinct from Step 1's Other (Step 1 uses a peer panel; Steps 2 and 4 use a radio + reveal). This asymmetry is intentional — both patterns are adapted to their parent layout's interaction model. Do not unify them.

### Part 5 — Update the assemblePrompt logic

**D5.1** Adapt the prompt-assembly logic to match the new template structure.

The new template (in `config.prompt_template`) uses:
- **Slot substitutions:** `{course_topic}`, `{student_level}`, `{class_size}`, `{class_format}`, `{teaching_context}`, `{step1_goal}`, `{step2_focus}`, `{materials_list}`, `{materials_other}`
- **Handlebars-style conditional blocks:** `{{#if teaching_context}}...{{/if}}` and `{{#if materials_other}}...{{/if}}`

Conditional blocks should be processed first (removing the block entirely when the conditional value is empty/whitespace), then slot substitutions are performed on the remaining template.

The Pamplin reference's `assemblePrompt` function (approximately lines 951-1008 of `pamplin_index.html`) implements exactly this pattern. Lift the conditional-processing regex and the slot-substitution loop directly.

**D5.2** Slot value mapping:

- `student_level` ← Step 3 `student_level` field value, or "instructor" (with the rest of the line adjusted) if not provided
- `class_size` ← Step 3 `class_size` value, with appropriate plural/singular phrasing; if "Not applicable", the line should read "...teaching {class_format}" (omitting the class size phrase entirely) — this requires a small piece of conditional logic
- `class_format` ← Step 3 `class_format` value, lowercased and tweaked grammatically (e.g., "in-person", "in a synchronous online format", "in a hybrid format")
- `course_topic` ← Step 3 `course_topic` value
- `teaching_context` ← Step 3 `teaching_context` value (the new free-text field)
- `step1_goal` ← Step 1 selection label, OR Step 1 `other_text` if Other was selected
- `step2_focus` ← Step 2 selection label, OR Step 2 `other_text` if Step 2 Other was selected, OR a sensible fallback if Step 1 Other was selected (Step 2's rendering when Step 1 Other was selected may be a free-text elaboration screen — see D6)
- `materials_list` ← Step 4 selected materials, formatted as bulleted list; if empty, the no-materials text from config copy
- `materials_other` ← Step 4 `other_text` value

The exact grammatical handling for class size and format may require small string-massaging helpers. Keep them in the same JS block.

### Part 6 — Handle the Step 1 Other → Step 2 elaboration flow

**D6.1** When the user picks Other on Step 1 (with typed text), Step 2 does not have a category-specific tree to show. The Pamplin pattern (approximately lines 540-555 of `pamplin_index.html`) handles this with a dedicated Step 2 free-text elaboration screen: "Tell us a bit more about what version of this you have in mind."

Implement the same fallback. When Step 1 selection is Other, Step 2 renders a single textarea screen (no radio options, no Other reveal), with a label that elaborates on the user's typed text. The user's Step 2 free-text becomes `step2.other_text` for prompt assembly.

This branch should also affect Step 4: when Step 1 is Other, Step 4 uses the `default` fallback materials list (`config.step4.default`), since there's no category-specific Step 4 tree.

### Part 7 — Surface the seven-section output schema in the Bridge screen

**D7.1** The Bridge screen currently shows the assembled prompt in a read-only textarea. Below or beside this textarea, add a new section titled "What the agent will produce" that lists the seven output sections from `config.output_schema`:

```
What the agent will produce:
1. Recommended tool
2. How to access
3. Opening prompt
4. Follow-up prompts
5. What to expect
6. Estimated time
7. Reflection reminder
```

This makes the response shape visible to the faculty member before they paste into the GPT. The seven-section schema becomes part of the workshop's visible architecture rather than hidden machinery.

Visual treatment: subtle. A small bordered card or a clean list. The Bridge screen's primary action (the "I'm back, share a reflection" button) should remain the most prominent UI element on the screen.

### Part 8 — Update boundary statements rendering

**D8.1** Three Step 1 categories now have "Best for..." boundary statements that appear below the category title on the homepage door panel or on the Step 1 screen itself (CC decides which placement reads better):

- `cases_scenarios`: "Best for faculty who want to build cases, generate examples, or develop applied scenarios for classroom use."
- `research_methods`: "Best for teaching students how IS research is designed, evaluated, and interpreted."
- `doctoral_supervision`: "Best for mentoring doctoral students and supporting long-arc scholarly development."

The other four categories do not render a boundary statement (they are self-explanatory from their titles).

Implementation: read from `config.step1.boundary_statements` and render below the category description on Step 1 cards (recommended). If absent for a category, render nothing.

Visual treatment: italic or muted text, smaller than the description. Should read as helpful orientation, not as gatekeeping.

### Part 9 — Update the homepage door panel descriptions

**D9.1** The homepage's three door panels currently carry descriptions written during HANDOFF_01. The Companion door's description should be updated to reflect the locked content design:

Current (HANDOFF_01): "The hands-on artifact. A triage interface that takes your teaching goal, hands you a tailored prompt, opens a custom AI agent, and returns you to a structured reflection. Use it during the workshop and afterward."

New: same content, slightly tightened — verify the existing copy is still accurate after content lock. CC may keep verbatim if appropriate.

The other two door descriptions (The Framework, Under the Hood) should be checked for staleness against the SPEC v0.3 framings, but probably need no changes.

---

## Constraints

- **Do not modify the homepage's title, byline, or layout.** Only the door descriptions, if needed.
- **Do not modify the Framework spoke.** It's working correctly.
- **Do not modify the Under the Hood stub.** Content drafting for that spoke is a later handoff.
- **Do not modify the shared CSS palette tokens** unless adding new ones for the amber-tan Other panel. Existing tokens stay.
- **Do not introduce new dependencies.** No npm packages, no CDN imports.
- **Preserve all data-submission logic.** The Google Form integration is unchanged. The payload schema is also unchanged in structure (still type/session_id/timestamp/payload), but the payload's contents reflect the new Step 3 fields (class_size new; teaching_context replaces current_approach; institution_type removed; department removed) and the new prompt template output.
- **Preserve session_id semantics.** UUID v4 generated on page load, used across all submissions for the session, regenerated on "Start another path".
- **No em dashes** in any rendered HTML or config copy strings. Verify the new config.json copy strings have none. (The pre-built config has been checked; verify after copying.)
- **No contrastive constructions** in any user-facing copy.
- **Respect SPEC v0.3 verbatim.** If anything in this handoff conflicts with SPEC, SPEC wins. Surface the conflict.

---

## Expected outputs

**New:**
```
/docs/reference/                    (directory)
  README.md                         (placed by Onur, but verify present)
  pamplin_index.html                (placed by Onur)
  pamplin_config.json               (placed by Onur)
  amcis_config.json                 (placed by Onur)
```

**Modified:**
```
/companion/config.json              (replaced with full AMCIS content tree)
/companion/index.html               (Other-UI patterns, Step 1→Step 2 elaboration flow, output schema in Bridge, updated assemblePrompt)
/assets/shared.css                  (new Other-panel color tokens and primitives, if not already present)
/index.html                         (door descriptions verified, possibly minor tweaks)
```

**Unchanged:**
```
/framework/index.html
/under-the-hood/index.html
/assets/slide1.png, slide2.png, slide3.png
/README.md, /.gitignore
/docs/AMCIS_SPEC.md                 (Onur updates separately to v0.3)
```

---

## Done criteria

**Reference files:**
- [ ] `docs/reference/` directory contains the three reference files plus README
- [ ] None of the reference files were modified by CC

**Config replacement:**
- [ ] `companion/config.json` contains the full AMCIS content tree (verifiable by checking that 7 Step 1 categories load with their descriptions)
- [ ] `companion/config.json` validates as JSON
- [ ] Old placeholder content is fully gone

**Step 1 Other panel:**
- [ ] Step 1 renders 7 category cards + Other panel in a 4×2 grid (Other in the 8th cell)
- [ ] Other panel uses amber-tan tint distinct from the neutral category cards
- [ ] Textarea is visible from first load (no click-to-reveal)
- [ ] Live character counter beneath the textarea updates as user types
- [ ] Clicking anywhere in the Other panel focuses the textarea
- [ ] Typing in the textarea selects Other (transferring selection if needed)
- [ ] Selecting any other category deselects Other (textarea content preserved)
- [ ] Continue is disabled when Other selected with empty/whitespace textarea

**Step 2 and Step 4 Other reveal:**
- [ ] Step 2 Other is a radio choice; selecting it reveals a "Describe in your own words" textarea
- [ ] Selecting any other Step 2 choice hides the textarea and clears its content
- [ ] Step 4 follows the same pattern
- [ ] Character limits enforced per `max_chars` in config

**Step 1 Other → Step 2 elaboration:**
- [ ] When Step 1 Other is selected, Step 2 renders an elaboration-textarea screen (no category-specific Step 2 tree)
- [ ] Step 4 in this branch uses the `default` materials list from config
- [ ] The full triage flow works end-to-end when Step 1 Other is chosen

**Step 3:**
- [ ] All 5 fields render (course_topic, student_level, class_size, class_format, teaching_context)
- [ ] No department field present
- [ ] course_topic is the only required field
- [ ] class_size dropdown includes "Not applicable" as a valid option

**Step 4:**
- [ ] Materials list rendered for each Step 1 × Step 2 path matches the path's tree in config
- [ ] "I'm starting from scratch" appears at the end of every materials list
- [ ] Step 4 Other reveal works per Pamplin pattern

**Boundary statements:**
- [ ] `cases_scenarios`, `research_methods`, and `doctoral_supervision` render their "Best for..." statements
- [ ] The other four categories render no boundary statement
- [ ] Statements appear as muted/italic helper text, not bold gatekeeping

**Prompt assembly:**
- [ ] Conditional blocks (`{{#if teaching_context}}`, `{{#if materials_other}}`) are processed correctly
- [ ] All slots substitute correctly
- [ ] Class-size "Not applicable" produces a sensible omitted-class-size phrase
- [ ] Class format string is grammatically natural ("in-person", "online (synchronous)", etc.)
- [ ] The seven-section requirement appears at the end of the assembled prompt

**Bridge screen — seven-section schema:**
- [ ] Bridge screen displays the seven output sections in a "What the agent will produce" section
- [ ] Visual treatment is subtle (not competing with the primary action button)
- [ ] Layout reads cleanly on both wide and narrow viewports

**Homepage:**
- [ ] Door descriptions verified against SPEC v0.3
- [ ] No staleness from HANDOFF_01

**Data submission:**
- [ ] Triage submission payload includes the new Step 3 fields and the full assembled prompt
- [ ] Reflection submission payload structure is unchanged (still type/session_id/timestamp/payload), with Q and O responses inside the payload JSON
- [ ] Google Form endpoint and entry IDs unchanged
- [ ] Test submission lands in the connected sheet

**Hygiene:**
- [ ] No em dashes in any rendered HTML or config copy strings
- [ ] No contrastive constructions in any user-facing copy
- [ ] No new dependencies
- [ ] No build step required

**End-to-end smoke (suggested for Onur):**
- [ ] Complete a full triage from Step 1 through reflection with the standard happy path
- [ ] Complete a full triage with Step 1 Other selected (verify elaboration flow)
- [ ] Complete a triage with Step 2 Other selected (verify reveal pattern)
- [ ] Verify both rows land in the Google Sheet with matching session_id
- [ ] Verify the Bridge screen shows the seven output sections clearly
- [ ] Verify the assembled prompt names the seven sections at the end

---

## Notes for CC

- The Pamplin reference is **working tested code**. Lift patterns directly rather than reinventing. Lift CSS verbatim where it fits; lift JS handler patterns; lift the assemblePrompt logic. Do not improve on the Pamplin patterns — they are tested at scale and any "improvements" risk regressions.
- The new `amcis_config.json` is **pre-built and validated**. Copy it; do not reconstruct. If CC believes the config has errors, surface the error rather than silently editing.
- The Step 1 → Step 2 Other elaboration flow is the most easily-missed pattern. When the user types in Step 1's Other textarea, the next screen should be the elaboration textarea screen, not a category-specific Step 2 tree (which doesn't exist for Other).
- Class-size handling needs a small grammatical adjustment: most values produce "...teaching X in a class of Y students" while "Not applicable" should produce "...teaching X" without the class-size clause. This is a 5-line conditional.
- The output schema list in the Bridge screen is a small visual addition. It should land as helpful framing, not as another wall of text. A small card or muted list is fine.
- If anything in HANDOFF_02 conflicts with SPEC v0.3 §7 (the content design specification), SPEC wins. Surface the conflict; do not silently resolve.
- Do not attempt to run a local web server or simulate the workshop flow. Onur will smoke-test after the build.
