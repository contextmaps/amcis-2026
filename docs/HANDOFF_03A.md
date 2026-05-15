# HANDOFF_03A. Platform UX fixes from workshop website feedback

**Project:** AMCIS 2026 Workshop. Teaching Inside the Thread
**Spec reference:** `docs/AMCIS_SPEC.md` v0.3 (with revisions tracked in this handoff)
**Workshop date:** 2026-08-20
**Cut:** Substantial UX revision affecting all three spokes (Homepage, Framework, Companion). Removes vocabulary-leakage of the underlying framework from user-facing surfaces. Fixes screen-fit issues on Companion's Step 1, Review, Bridge, and Reflection screens. Adopts visual identity refinements (full title rendering, VT orange accent on Home button, AMCIS-style description text).

---

## Goal of this iteration

The workshop site is functionally complete after HANDOFF_02. This handoff addresses the first round of usability feedback. The changes fall into three categories:

1. **Visual identity:** Full title rendering on homepage, new description text matching AMCIS conference style, VT orange accent on the shared Home navigation button.

2. **Framework-vocabulary removal:** The M-Open note on the Bridge screen, the Q-block and O-block screens on Reflection, the X-block confirmation button, and the standalone X-block (capstone) screen are removed. Faculty experience the framework through the structure of the experience, not through framework terminology bleeding into the UI. The Framework spoke remains the place where block vocabulary is named and explained for curious users.

3. **Screen-fit and interaction polish:** Step 1 card design refactored (radios removed, card-click selection, color highlight). Review screen relaid as two-column for vertical compression. Bridge screen's seven-section panel compressed to one line. Grammar fix in `assemblePrompt`. Confirmation panel after Save Reflection gains a "Re-open the Companion in a new tab" button.

This is a single coherent cycle even though the change list is long. Each change is mechanically simple; the volume comes from the breadth of surfaces touched.

---

## Current state of the repository

After HANDOFF_02 executed:

```
/index.html                              (homepage with three doors)
/assets/shared.css                       (design system + Pamplin-lifted Other-UI primitives)
/assets/slide1.png, slide2.png, slide3.png
/framework/index.html                    (three-slide flow with bottom Back-to-Home button)
/companion/index.html                    (full Companion state machine with all current screens)
/companion/config.json                   (full AMCIS content tree)
/under-the-hood/index.html               (stub, not modified in this cycle)
/docs/AMCIS_SPEC.md                      (v0.3)
/docs/HANDOFF_01.md, HANDOFF_01_PATCH.md, HANDOFF_02.md  (executed handoffs)
/docs/CC_PROMPT_HANDOFF_01.md, etc.      (executed CC prompts)
/docs/reference/                         (Pamplin reference files)
/docs/AGENT_DEFINITION.md                (v1.3, agent body for the GPT)
```

---

## Deliverables

### Part 1. Homepage (`index.html`)

**D1.1. Full title rendering.** Replace the split-title treatment with a single line.

Current state: "Teaching Inside the Thread" rendered as the main title (large), "An AI-Centered Pedagogy" rendered as a smaller subtitle below.

Target state: A single title line reading **"Teaching Inside the Thread: An AI-Centered Pedagogy"**. Font size reduced slightly from the current main-title size so the full title fits on one line at the standard viewport without wrapping. The conference name, location, date, and the author byline that currently sit below the subtitle move up to occupy the freed vertical space.

Visual treatment: same color, same weight, same font family as the current main title. Only the size and the content change.

**D1.2. Description paragraph.** Replace the current description text above the three door panels.

Current text:
> "A 90-minute workshop, structured as three doors. The framework, a working artifact you can use, and the methodology behind the build."

New text:
> "AI is reshaping how students engage with course material, but most faculty are working without a coherent framework for what that means pedagogically. This 90-minute workshop introduces an AI-Centered Pedagogy through a hands-on Companion Interface that attendees use live during the session. You'll work through a triage of your teaching goal, receive a tailored prompt, engage with a custom AI agent calibrated for IS audiences, and complete a structured reflection. The session closes with a walkthrough of the design and build process behind the artifact. Pre-requisites include a laptop and a ChatGPT account (free tier acceptable)."

The new paragraph is approximately 100 words. It mirrors the rhythm of the AMCIS conference website's description style. It serves two purposes: it appears above the three door panels on the homepage, and it is the description Onur will submit to AMCIS for the conference program.

Visual treatment: same styling as the current description paragraph (muted color, smaller than the title, comfortable line-height). Width-constrained per the existing design.

### Part 2. Shared Home button color (`assets/shared.css`)

**D2.1. VT orange accent on the Home button across all spokes.**

The top navigation banner currently displays "Home" in the top-right corner across the Framework, Companion, and Under the Hood spokes. The banner is VT maroon. Change the Home button's accent color to **VT orange** so it stands visually distinct from the maroon banner.

The Virginia Tech color palette uses Burnt Orange `#cf4520` as its complementary brand color to Maroon `#630031`. Use Burnt Orange (or a close visual match consistent with the existing palette tokens, if `assets/shared.css` already defines an orange token) for the Home button's background or its text-and-border treatment, whichever reads better against the maroon banner.

The "Teaching Inside the Thread" text in the top-left of the banner (also a link to home) stays in its current style; this change only affects the right-side Home button.

### Part 3. Framework spoke (`framework/index.html`)

**D3.1. Remove the bottom Back-to-Home button.**

The Framework slide pages currently have a "Back to Home" button at the bottom of each slide. Remove this button entirely from all three slide pages. The top-left "Teaching Inside the Thread" text-link and the top-right "Home" button both already navigate home; the bottom button is redundant and is partially cut off at standard viewports.

The "Previous" and "Next" navigation buttons at the bottom of each slide stay as they are.

### Part 4. Companion: Step 1 redesign (`companion/index.html`)

**D4.1. Remove the "Pick this area" radio button from each category card.**

The category cards on Step 1 currently render with a radio button labeled "Pick this area" at the bottom of each card. Remove these radio buttons entirely.

**D4.2. Card-click selection with background color change.**

Selection is now indicated by clicking anywhere on the card body (not on a specific control). When a card is selected, its background color changes to indicate the selection. Use a soft AMCIS-palette tint for the selected state (the existing `--accent-soft` token or its equivalent. a pale maroon-tinted background). The card border may also change to a stronger maroon to reinforce the selection. Unselected cards revert to their neutral background.

Only one card may be selected at a time across the seven category cards.

**D4.3. Update Step 1 instructional text.**

Current text (Step 1 subtext, `copy.step1_subtext` in config):
> "Pick the area that best matches what you want to work on. You can refine the focus on the next screen."

New text:
> "Click on the panel that best matches what you want to work on, or type it in the Other box. Then click Continue."

Update `companion/config.json` with the new copy string.

**D4.4. Bug fix: typing in the Other textarea must clear category card selection.**

Current bug: if the user selects a category card and then types in the Other panel's textarea, the card's selection visually persists. The Other panel correctly becomes selected, but the previously-selected category card stays highlighted, creating ambiguity.

Target behavior: typing in the Other textarea immediately clears any selected category card. Symmetrically (and this is already working): clicking a category card while text exists in the Other textarea deselects the Other panel (the textarea content is preserved per the existing Pamplin pattern, but the visual selection moves to the card).

**D4.5. Vertical compression.**

With the "Pick this area" radio removed, each card shrinks vertically. The Step 1 layout should reflow so the Continue button is visible without scrolling at a standard 1080p viewport. No new bottom padding or empty space.

### Part 5. Companion: grammar fix in `assemblePrompt` (`companion/index.html`)

**D5.1. Change instructor phrasing.**

Current prompt template renders the opening sentence as:
> "I am a Master's instructor teaching in-person in a class of 25 or fewer students."

Target rendering:
> "I am an instructor of a Master's course teaching in-person in a class of 25 or fewer students."

Apply this pattern across all student level options:
- Undergraduate → "I am an instructor of an undergraduate course teaching..."
- Master's → "I am an instructor of a Master's course teaching..."
- Doctoral → "I am an instructor of a doctoral course teaching..."
- Mixed → "I am an instructor of a mixed-level course teaching..."

When student level is blank or not selected, fall back to "I am an instructor teaching..." (drop the "of a X course" phrase entirely).

This change lives in the `studentLevelArticleAndText()` helper (or whatever the equivalent function is named in the current `companion/index.html`). The prompt template string in `config.json` does not change; only the slot-substitution logic does.

### Part 6. Companion: Review screen two-column layout (`companion/index.html`)

**D6.1. Two-column layout on the Review screen.**

The Review screen currently displays the four review sections (Goal, Specific focus, Context, Materials) stacked vertically, followed by a "Prompt to be copied" panel below them, followed by the "Copy prompt and open the Companion" button at the bottom. The bottom action button is currently below the fold at standard viewports.

Target layout: a two-column grid at viewports ≥1024px wide.

- **Left column:** The four review sections (Goal, Specific focus, Context, Materials) with their Edit links, stacked vertically as they are now.
- **Right column:** The "Prompt to be copied" panel with the assembled prompt visible inside it.
- **Below both columns (full width):** The "Copy prompt and open the Companion" primary action button.

At viewports < 1024px wide, the two columns stack (Left first, then Right, then the button below), preserving the current single-column experience for narrow screens.

This compresses the screen vertically and makes the primary action visible without scrolling on standard workshop-day displays.

The Edit links on the left-column sections continue to work as they currently do (clicking jumps back to the relevant step).

### Part 7. Companion: Bridge screen cleanup (`companion/index.html`)

**D7.1. Remove the green M-Open note.**

The Bridge screen currently renders a green-tinted note that reads approximately:
> "This prompt is your M-Open, the start of a multi-turn exchange. When you're done, you can paste an M-Close into the thread or simply close it."

Remove this entire note element. The vocabulary (M-Open, M-Close, multi-turn exchange) is framework-specific and is not part of the experience AMCIS attendees need or expect. The reasoning: faculty should not need to learn the framework's internal vocabulary to use the Companion successfully. The Framework spoke is the place where this vocabulary is named and explained for curious users.

The corresponding config copy string (`copy.bridge_m_open_note` in `companion/config.json`) may be deleted from the config, or kept as a dead key. CC's choice. The note element itself is the user-visible change.

**D7.2. Compress the "What the agent will produce" panel.**

The Bridge screen currently renders the seven-section schema as a numbered list inside a bordered card titled "What the agent will produce." This takes substantial vertical space and pushes the primary "I'm back, share a reflection" button below the fold.

Target rendering: a compact one-line description titled "What the agent will produce" followed by a single sentence:

> "A structured response with seven sections in one message: 1. Recommended tool, 2. How to access, 3. Opening prompt, 4. Follow-up prompts, 5. What to expect, 6. Estimated time, and 7. Reflection reminder."

Visual treatment: small, muted, single-line (the seven sections enumerated inline with comma separators or in a compact horizontal flow). The bordered card may stay (smaller now) or be removed; CC chooses based on what reads cleanly. The compressed panel must occupy substantially less vertical space than the current numbered-list version.

The seven-section content is unchanged. Only the rendering compresses.

**D7.3. Verify primary action is above the fold.**

After D7.1 and D7.2, the "I'm back, share a reflection" button should be visible without scrolling at a standard 1080p viewport.

### Part 8. Companion: Reflection screen. remove Q and O blocks (`companion/index.html`, `companion/config.json`)

**D8.1. Remove the Q block (checkbox question).**

The Reflection screen currently renders, below the main reflection textarea, a checkbox question labeled "Which of these AI-in-teaching practices feels most likely to change something about your teaching this fall?" with five options. Remove this entire block from the rendered screen.

The corresponding config content (`reflection.q_block` in `companion/config.json`) may be deleted from the config, or kept as a dead key. CC's choice. The user-visible Q block disappears.

**D8.2. Remove the O block (ranking question).**

Below the Q block, the Reflection screen currently renders a ranking question labeled "Rank these dimensions of AI-assisted teaching by how much they concern you." with six rankable items. Remove this entire block from the rendered screen.

The corresponding config content (`reflection.o_block` in `companion/config.json`) may be deleted from the config, or kept as a dead key. The user-visible O block disappears.

**D8.3. Reflection payload simplified.**

The data submitted to the Google Form when the user clicks "Save reflection" no longer includes `q_responses` or `o_responses`. The reflection payload is now: `reflection_text`, `optional_name`, plus the existing session_id and timestamp. The payload structure (type/session_id/timestamp/payload) remains the same; only the contents of the `payload` JSON are simplified.

This is a deliberate trade: structured Q/O data is lost, but the experience becomes cleaner and the Save Reflection button moves above the fold. The remaining data. the user's triage selections plus their free-text reflection. is still substantive evidence for post-workshop analysis.

**D8.4. Vertical compression.**

After D8.1 and D8.2, the "Save reflection" button should be visible without scrolling at a standard 1080p viewport.

### Part 9. Companion: Reflection confirmation panel restructure (`companion/index.html`, `companion/config.json`)

**D9.1. Remove the "Try an X block" button from the confirmation panel.**

After Save Reflection, the green confirmation panel currently shows two buttons:
- "Try an X block: open a free exploration"
- "Start another path"

Remove the "Try an X block" button entirely.

**D9.2. Remove the standalone X-block screen.**

The Companion state machine currently has an X-block screen (labeled "If you have time, try an X block.") that activates when the user clicks the now-removed Try-an-X-block button. Remove this entire screen from the state machine. The state machine's step ordering is now: triage steps → bridge → reflection → confirmation panel (no further screens beyond confirmation).

The X-screen's specific UI elements (the "Copy ### X prefix" button, the body copy describing X-blocks) disappear with the screen.

**D9.3. Move the "Re-open the Companion in a new tab" button to the confirmation panel.**

The "Re-open the Companion in a new tab" button currently lives on the now-removed X-screen. Move this button to the green confirmation panel that appears after Save Reflection.

**D9.4. Rename "Start another path" to "Done, start another path".**

In the confirmation panel, rename the "Start another path" button to "Done, start another path" (the wording from the now-removed X-screen, which Onur preferred). Update the corresponding config copy string.

**D9.5. Final confirmation panel layout.**

After D9.1 through D9.4, the green confirmation panel contains:
- A short confirmation message: "Thank you. Your reflection is saved." (existing copy, unchanged)
- Two buttons side by side:
  - "Re-open the Companion in a new tab" (secondary button styling)
  - "Done, start another path" (primary button styling)

No third button. No X-block reference.

### Part 10. Config copy and dead-key cleanup (`companion/config.json`)

**D10.1. Copy string updates.**

Apply these copy string changes in `companion/config.json`:

- `copy.step1_subtext`: Replace with the new instructional text from D4.3.
- `copy.bridge_m_open_note`: Delete from config (the rendering removal in D7.1 is the change; the config key can either be removed or kept as a dead key).
- `copy.try_x_label`: Delete from config (the X-block button is gone per D9.1).
- `copy.x_prompt`, `copy.x_subtext`, `copy.x_copy_prefix_label`, `copy.x_reopen_label`, `copy.x_done_label`: Delete from config (the X-screen is gone per D9.2).
- `copy.new_route_label`: Replace value with "Done, start another path" (D9.4).
- The "Re-open the Companion in a new tab" button label needs a config key. If `copy.x_reopen_label` was being used for this, keep that key and reuse its value ("Re-open the Companion in a new tab"). Otherwise, add a new key like `copy.reopen_companion_label` with the same value. CC chooses naming.

**D10.2. Dead reflection content.**

In `companion/config.json`:
- `reflection.q_block`: Delete from config (or keep as dead key).
- `reflection.o_block`: Delete from config (or keep as dead key).
- `reflection.textarea_max_chars`, `reflection.textarea_suggested_min_words`, `reflection.textarea_suggested_max_words`: All keep.

---

## Constraints

- **Do not modify `docs/AMCIS_SPEC.md`.** Onur will update the SPEC separately to reflect the changes in this handoff.
- **Do not modify `docs/AGENT_DEFINITION.md`.** Agent body is locked at v1.3.
- **Do not modify Under the Hood (`under-the-hood/index.html`).** That spoke is the subject of a separate planned handoff (HANDOFF_03B).
- **Do not touch the GPT configuration on ChatGPT.** Agent calibration is a separate work track.
- **Do not break the existing data submission logic.** The Google Form endpoint and entry IDs are unchanged. The payload structure (type/session_id/timestamp/payload) is unchanged. Only the contents of the payload JSON for reflection submissions simplify per D8.3.
- **Do not modify the existing Step 2 / Step 4 Other reveal patterns.** Those (the radio + reveal pattern on Steps 2 and 4) were lifted from Pamplin in HANDOFF_02 and remain correct for those steps. The Step 1 redesign in Part 4 is a deliberate departure from the Pamplin pattern for AMCIS. Step 1's card-click selection is *not* applied to Steps 2 and 4.
- **No em dashes** in any rendered HTML, copy strings, or new content. Verify after all edits.
- **No contrastive constructions** in user-facing copy.
- **Preserve session_id semantics.** Generated on page load, used across submissions within a session, regenerated on "Done, start another path."

---

## Expected outputs

**Modified files:**

```
/index.html                        (D1.1, D1.2)
/assets/shared.css                 (D2.1; possibly small CSS additions for Step 1 card-click selection if not handled in companion/index.html's embedded styles)
/framework/index.html              (D3.1. applies to all three slide pages)
/companion/index.html              (D4.1-D4.5, D5.1, D6.1, D7.1-D7.3, D8.1-D8.4, D9.1-D9.5)
/companion/config.json             (D8 dead-key cleanup, D10.1-D10.2)
```

**Unchanged files:**

```
/under-the-hood/index.html
/assets/slide1.png, slide2.png, slide3.png
/docs/AMCIS_SPEC.md
/docs/AGENT_DEFINITION.md
/docs/reference/                   (all reference files preserved)
```

---

## Done criteria

**Homepage (Part 1):**
- [ ] Title renders as a single line: "Teaching Inside the Thread: An AI-Centered Pedagogy"
- [ ] Title font size adjusted to fit on one line at standard viewport without wrapping
- [ ] Conference details + author byline moved up to occupy freed vertical space
- [ ] Description paragraph replaced with the new ~100-word AMCIS-style text
- [ ] Description reads cleanly above the three door panels

**Home button color (Part 2):**
- [ ] Home button in top-right banner uses VT orange (or close palette match) across all spokes
- [ ] Visual distinction from VT maroon banner is clear without being garish

**Framework (Part 3):**
- [ ] Bottom "Back to Home" button removed from all three slide pages
- [ ] Top-left text-link and top-right Home button both work as before
- [ ] Previous/Next slide navigation works as before

**Step 1 (Part 4):**
- [ ] "Pick this area" radios removed from all category cards
- [ ] Cards select on click anywhere on the card body
- [ ] Selected cards show distinct background color (palette-consistent soft maroon tint)
- [ ] Only one card may be selected at a time
- [ ] Step 1 instructional text updated per D4.3
- [ ] Typing in Other textarea clears any selected card
- [ ] Clicking a card while Other has content deselects Other (existing behavior preserved)
- [ ] Continue button visible without scrolling at 1080p

**Grammar (Part 5):**
- [ ] Assembled prompts read "I am an instructor of a Master's course teaching..." style
- [ ] All four student levels produce grammatical sentences
- [ ] Blank student level produces "I am an instructor teaching..." without orphan phrase

**Review screen (Part 6):**
- [ ] Two-column layout at viewports ≥1024px (review sections left, prompt panel right)
- [ ] Single-column stack at viewports <1024px
- [ ] "Copy prompt and open the Companion" button below both columns, visible without scroll at 1080p
- [ ] Edit links continue to work as before

**Bridge (Part 7):**
- [ ] Green M-Open note removed
- [ ] Seven-section schema compressed to a single-line description
- [ ] "I'm back, share a reflection" button visible without scroll at 1080p

**Reflection (Part 8):**
- [ ] Q block removed from screen
- [ ] O block removed from screen
- [ ] Reflection payload simplified (no q_responses, no o_responses)
- [ ] Save Reflection button visible without scroll at 1080p

**Confirmation panel (Part 9):**
- [ ] "Try an X block" button removed
- [ ] X-block screen removed from state machine
- [ ] "Re-open the Companion in a new tab" button moved to confirmation panel
- [ ] "Start another path" renamed to "Done, start another path"
- [ ] Confirmation panel layout has two buttons side by side, no third

**Config (Part 10):**
- [ ] `copy.step1_subtext` updated
- [ ] `copy.new_route_label` updated to "Done, start another path"
- [ ] X-screen-related copy keys removed or marked dead
- [ ] Q/O block reflection content removed or marked dead
- [ ] Config validates as JSON

**Hygiene:**
- [ ] No em dashes in any rendered HTML or config copy
- [ ] No contrastive constructions in user-facing copy
- [ ] Google Form endpoint and entry IDs unchanged
- [ ] Session_id semantics preserved

**End-to-end smoke (suggested for Onur):**
- [ ] Homepage renders with full title, new description, three doors
- [ ] Framework spoke navigates between slides; no bottom Back-to-Home button; top-right Home button is orange
- [ ] Step 1 cards click-to-select with color highlight; Other clears card selection
- [ ] Full triage completes; Review screen is two-column on wide viewport
- [ ] Bridge screen shows compressed schema; primary button above fold
- [ ] Reflection screen has no Q or O blocks; Save button above fold
- [ ] Confirmation panel shows two buttons: Re-open Companion + Done start another path
- [ ] Triage submission lands in Google Sheet with full prompt
- [ ] Reflection submission lands in Google Sheet without Q/O fields

---

## Notes for CC

- This is a UX revision cycle, not a content cycle. No new content tree work, no new categories, no new Step 2 items. The config.json content is largely preserved; only the metadata copy strings around the now-removed UI elements change.

- The Step 1 redesign in Part 4 is a deliberate departure from the Pamplin Other-UI pattern lifted in HANDOFF_02. Step 1 moves from radio-button-in-card to click-card-to-select. Steps 2 and 4 remain on the Pamplin radio + reveal pattern; do not change those.

- For D4.4 (Other textarea clears card selection): this is a bug fix, not a redesign. The Step 1 Other panel already deselects when a card is clicked (that pattern is preserved from HANDOFF_02). The reverse direction. clicking into the Other textarea → card deselects. is the missing piece. Add an event listener on the textarea's focus or first-input event that calls the same clear-selection function used by the Other panel's existing input handler.

- For D7.2 (compressed schema): the compact rendering can be a single paragraph with the seven sections enumerated inline, separated by commas. The exact visual treatment (whether the section names are bold, the numbers are stylized, etc.) is CC's choice as long as the result reads cleanly and occupies meaningfully less vertical space than the current bulleted list.

- For D9.5 (confirmation panel layout): two buttons side by side at standard viewports. At very narrow viewports (mobile), the buttons can stack. The "Done, start another path" button retains primary styling (the bold maroon background); the "Re-open the Companion in a new tab" button uses secondary styling (border-only, less visual weight).

- Submission to the Google Form must continue to work after the reflection payload simplifies. Test this end-to-end during smoke testing.
