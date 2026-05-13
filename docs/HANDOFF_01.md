# HANDOFF_01 — Hub-and-spoke skeleton, Companion working end-to-end

**Project:** AMCIS 2026 Workshop — Teaching Inside the Thread
**Spec reference:** `AMCIS_SPEC.md` v0.2
**Workshop date:** 2026-08-20 (~14 weeks from this handoff)
**Cut:** Substantial first cycle — establishes the full architecture with one spoke fully working and two spokes as informative stubs

---

## Goal of this iteration

Stand up the complete hub-and-spoke architecture for the workshop site, with The Companion working end-to-end and the other two spokes as informative skeletons. By the end of this handoff, the artifact at `contextmaps.github.io/amcis-2026/` is walkable in full: homepage with three doors, each door leading to a functional spoke, with The Companion executing a complete triage → bridge → reflection → optional X flow against the live AMCIS Teaching Companion GPT and submitting data to the live Google Form.

Four concrete builds:

1. **Hub (homepage).** Polished landing page with title, byline, and three door panels.
2. **The Framework spoke.** Three-page navigable slide flow using the existing PNG images.
3. **The Companion spoke.** Full platform state machine, IS-audience Step 1 content (with placeholder Step 2), expanded reflection with Q and O blocks, opt-in X capstone, wired to the GPT and the Google Form.
4. **Under the Hood spoke.** Informative stub page with title, byline, and a clear "in active drafting" framing.

Plus: **shared CSS design system** spanning all four pages.

---

## Current state

- Project is a new GitHub repo at `contextmaps/amcis-2026`, deploying to `contextmaps.github.io/amcis-2026/`.
- The repo is empty (or has only a default README). This handoff is the first substantive build.
- Onur has the three PNG slide images locally and will place them in `assets/` as `slide1.png`, `slide2.png`, `slide3.png` before CC runs (or CC can prompt for their placement if absent).
- The AMCIS Teaching Companion GPT is created and live at the URL below, with a placeholder instruction body sufficient for end-to-end testing.
- The Google Form is created, verified, and live (test submission confirmed 2026-05-13).

---

## Inputs

**GPT URL:**

```
https://chatgpt.com/g/g-6a04e57a41208191ac7ef63d967053f8-amcis-teaching-companion
```

**Google Form configuration:**

```
SUBMISSION_URL:   https://docs.google.com/forms/d/e/1FAIpQLSfr1k5pksXMujds0RpFEdpc8bTVxk5aWaZVyQANSuMn71j5GA/formResponse
ENTRY_TYPE:       entry.1850646152
ENTRY_SESSION_ID: entry.560367375
ENTRY_TIMESTAMP:  entry.1473660026
ENTRY_PAYLOAD:    entry.1114220693
```

**Workshop title:**

> Teaching Inside the Thread: An AI-Centered Pedagogy

**Byline (used on homepage and Under the Hood):**

> AMCIS 2026 Workshop · Reno, Nevada · August 20, 2026
> Onur Seref, Pamplin College of Business, Virginia Tech

---

## Deliverables

### Part 1 — File structure and shared CSS

**D1.1 Create the directory structure** at project root:

```
/index.html                       (homepage)
/assets/
  shared.css                      (design system for all pages)
  slide1.png                      (placed by Onur)
  slide2.png                      (placed by Onur)
  slide3.png                      (placed by Onur)
/framework/
  index.html                      (three-page slide flow)
/companion/
  index.html                      (platform state machine)
  config.json                     (content + form + agent URL)
/under-the-hood/
  index.html                      (stub for v1)
```

If `assets/slide1.png` etc. do not exist when CC runs, the framework pages should still render — they should display a placeholder caption "Slide image not yet placed" instead of breaking the layout. CC must not attempt to generate the slide images.

**D1.2 Author `assets/shared.css` as the design system across all four pages.**

The shared stylesheet defines:

- **CSS variables (`:root`):** color tokens (background, foreground, accent, muted, success, warning), typography (font family, base size, line height), spacing scale, border radius, shadow tokens.
- **Color palette:** Virginia Tech maroon (`#630031`) as the primary accent, with supporting neutrals (white background, near-black text, mid-gray for muted content). The maroon appears in the title strip on each page and the door panel borders/accents on the homepage. Restrained use — this is an academic artifact, not a marketing page.
- **Typography:** modern system font stack (`-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, ...`). Base size 16px. Title scale up to 36–48px on the homepage hero. Adequate line height (1.5) for body text, tighter (1.2) for titles.
- **Page header pattern:** consistent across all four pages. Top strip in maroon, ~48–56px tall, containing the workshop title in small white text top-left and a "Home" link top-right (the homepage shows no Home link since it *is* home; the other three pages all show it).
- **Button styles:** primary (maroon background, white text), secondary (white background, maroon border and text), tertiary (text-only with underline on hover). Adequate touch targets (>= 40px tall).
- **Door panel pattern (homepage-specific):** large clickable cards with title, short description, and clear hover affordance.
- **Block accent palette (Companion-specific):** small color set for R0/S/M/R/Q/O/X block accents. Use the palette established in the prior platform's design (the BUS 1204 palette) if it's clearly documented somewhere CC can access; otherwise define a fresh set: R0 = blue, S = green, M = purple, R = amber, Q = teal, O = orange, X = magenta. Each block accent is a thin colored border or top strip plus a small icon. Subtle, not loud.
- **plib-* primitives** carried forward from the prior platform: `.plib-copy-btn`, `.plib-textarea` with auto-resize and word/char counter, `.plib-aria-live` announcement region, focus-visible outlines. These are well-established; CC should preserve their patterns rather than reinvent them.

The CSS file is the source of truth for visual consistency across the four pages. All four `index.html` files import it via `<link rel="stylesheet" href="/amcis-2026/assets/shared.css">` or relative paths as appropriate.

### Part 2 — The homepage (hub)

**D2.1 Author `/index.html` as the polished landing page.**

The homepage carries:

1. **Page header strip** (per the shared design system) — workshop title in small text top-left, no Home link (this is home).

2. **Hero section.** Workshop title in large, confident typography:

   > **Teaching Inside the Thread**
   > *An AI-Centered Pedagogy*

   Below the title, the byline:

   > AMCIS 2026 Workshop · Reno, Nevada · August 20, 2026
   > Onur Seref, Pamplin College of Business, Virginia Tech

   Generous whitespace around the hero. The title and byline should feel anchored, not crammed.

3. **Three-door section.** Three large clickable panels arranged horizontally (collapsing to vertical on narrow viewports). Each panel:

   - **Panel 1: The Framework**
     - Title: "The Framework"
     - Description: "An AI-Centered Pedagogy for the AI era. Three slides walk through the position: the shift from AI-as-tool to learning-inside-the-thread, the three-phase curricular progression, and the human-AI collaboration loop."
     - Clicks through to `/framework/`

   - **Panel 2: The Companion**
     - Title: "The Companion"
     - Description: "The hands-on artifact. A triage interface that takes your teaching goal, hands you a tailored prompt, opens a custom AI agent, and returns you to a structured reflection. Use it during the workshop and afterward."
     - Clicks through to `/companion/`

   - **Panel 3: Under the Hood**
     - Title: "Under the Hood"
     - Description: "How this artifact was designed and built. The framework articulated formally, the methodology behind the workflow, and the human-AI discipline used to produce it. In active drafting."
     - Clicks through to `/under-the-hood/`

4. **Footer.** Small text at the bottom: a one-line acknowledgment of AMCIS 2026 and Reno, NV as the venue, plus a "Last updated: [date]" stamp. Optional: a small contact line ("For questions: [email or contact link]"). Onur to decide whether to include contact.

The homepage is the most design-load-bearing page in the artifact. It is the first impression for Dean Sarker, Jason, and AMCIS attendees. Polished, restrained, confident.

### Part 3 — The Framework spoke

**D3.1 Author `/framework/index.html` as a three-page slide flow.**

Three logical pages, navigable as a small flow:

- **Page 1:** displays `slide1.png` (the Old vs. New Framework slide). Next button visible bottom-right. Home link top-right of the header strip.
- **Page 2:** displays `slide2.png` (the Three-Phase Progression). Previous and Next buttons.
- **Page 3:** displays `slide3.png` (the Human-AI Collaboration Loop). Previous button. No Next (this is the last page); instead, a Home link that's slightly more prominent than the header's Home link.

Each page renders the slide image at maximum responsive width while preserving aspect ratio. The image should dominate the viewport — these slides are dense and benefit from screen real estate.

Below each slide image, a small caption identifies the slide ("Slide 1 of 3: From AI-as-Tool to Learning Inside the Thread", etc.). No additional text content per page in v1; the slides themselves carry the message.

**Implementation note for CC:** the three logical pages can be implemented as three separate HTML routes (`/framework/`, `/framework/2/`, `/framework/3/`) or as a single HTML file with three sections shown/hidden via JavaScript (more like a slide deck behavior). Single file with JS is preferred — it's lighter, gives smoother transitions, and matches the "slide deck" mental model. Use URL hash routing (`#1`, `#2`, `#3`) so individual slides remain linkable.

**D3.2 Navigation behavior.**

- Prev/Next buttons advance the visible slide. They are disabled at the ends (no prev on slide 1, no next on slide 3).
- Keyboard support: left/right arrow keys advance, same behavior as the buttons.
- The Home link in the header always returns to the workshop homepage (`/amcis-2026/`).
- A small slide counter ("1 of 3") sits next to the navigation buttons.

### Part 4 — The Companion spoke

**D4.1 Adapt the prior platform's state machine for AMCIS at `/companion/index.html`.**

The state machine is substantively the prior platform's logic. Eight screens managed by a `companionState` object: Step 1 → Step 2 → Step 3 → Step 4 → Review → Bridge → Reflection → optional X. Single-file HTML with embedded JS, imports the shared CSS, plus its own internal CSS for state-machine-specific styles.

**Page header:** workshop title small text top-left, "Home" link top-right (returns to `/amcis-2026/`). No suppress-header logic — The Companion is standalone, not iframe-embedded.

**State machine pattern:** single screen visible at a time, controlled by a `currentScreen` variable. Backward navigation allowed until the Bridge screen commits; after commit, the session is closed and only "Start another path" reopens triage.

**D4.2 Block accents on each screen.**

Per SPEC v0.2 §5.2, each screen carries a light block accent. CC must implement these as part of the page CSS, drawing from the block accent palette in the shared CSS:

- **Step 1 through Step 4 + Review:** R0 accent (blue). The triage flow assembles the R0; the screens are part of that assembly. A thin blue top strip and a small "Session opener" label in the screen's corner.
- **Bridge:** S accent (green). The Bridge screen displays the assembled prompt (the S block, or the M-Open depending on framing). Thin green top strip, "Prompt block" label, plus a small line of explanatory text noting that this prompt is the M-Open if the faculty member chooses to use that framing.
- **Reflection:** R accent (amber) as the dominant accent. The reflection textbox itself is styled with an amber border. Below or beside the textbox, the Q block and O block appear with their own block styling (teal for Q, orange for O). Three block types visible on one page, naturally.
- **X (opt-in capstone):** X accent (magenta). Its own screen, accessed only after a reflection is saved.

The accents are **light**. Thin borders, small icons, corner labels. Not bordered cards with prominent block IDs. Faculty who don't care barely register the marking.

**D4.3 Step 1 content — AMCIS audience.**

Replace the prior platform's Step 1 content with the seven AMCIS categories per SPEC v0.2 §6.1:

1. Course design and architecture
2. Teaching technical content
3. Cases, examples, and applications
4. Engagement and interaction
5. Assessment in the AI era
6. Doctoral training and supervision
7. Building learning artifacts

Plus an "Other" option that opens a free-text input (mirroring the prior platform's pattern).

Each category gets a short one-line description visible under the title in the grid, helping faculty pick the right one. CC drafts these short descriptions during build; Onur reviews and edits in HANDOFF_02.

**Grid layout:** 4 columns × 2 rows on wide viewports (3 categories + "Other" on row 2, with row 1 holding categories 1–4 and row 2 holding categories 5–7 plus Other). On medium viewports (720–1023px), 2 columns × 4 rows. On narrow viewports, single column.

**D4.4 Step 2 content — placeholder for HANDOFF_02.**

Each Step 1 category gets a single placeholder Step 2 item plus "Other":

- Category 1 → Step 2 item: "Sample focus area for Course design and architecture (placeholder)"
- Category 2 → Step 2 item: "Sample focus area for Teaching technical content (placeholder)"
- ...and so on for all seven.

The placeholder text is sufficient to wire Step 2 through to Step 3. Real Step 2 content is drafted in HANDOFF_02.

**D4.5 Step 3 content — IS-appropriate context.**

Per SPEC v0.2 §6.3:

- **Course topic** (text input). Retained, no department dropdown.
- **Student level** (Undergraduate / Master's / Doctoral / Mixed).
- **Class format** (In-person / Online / Hybrid).
- **Current approach** (optional, free text, IS-flavored prompt: "How are you currently teaching this, if at all? If you're designing from scratch, leave blank.").
- **Institution type** (optional dropdown: R1 / R2 / regional / liberal arts / professional / Other).

The "department dropdown" from the prior platform is **removed entirely**, including its config entries.

**D4.6 Step 4 content — placeholder for HANDOFF_02.**

Same as Step 2: each Step 1 × Step 2 combination gets a single placeholder material option ("Sample material option — placeholder") plus an "Other" free text. Real Step 4 content matures with Step 2 in HANDOFF_02.

**D4.7 Review screen.**

Standard pattern from the prior platform: all four steps shown, each with inline "Edit" affordance that jumps back to the corresponding step. The primary action button reads "Copy prompt and open the Companion" (parallel to the prior platform's "Copy prompt and open the agent" but updated for the AMCIS context).

Clicking the primary button commits the session: clipboard receives the assembled prompt, the AMCIS Teaching Companion GPT URL opens in a new tab, the triage record is POSTed to the Google Form, and the platform transitions to the Bridge screen.

**D4.8 Bridge screen.**

Standard Bridge pattern from the prior platform, with the S accent applied. Contains:

- Confirmation message: "Your prompt is on your clipboard — the AMCIS Teaching Companion should have opened in a new tab."
- The agent URL displayed prominently as a clickable link.
- A "Copy the prompt again" button (secondary action, clipboard insurance).
- The assembled prompt visible in a read-only textarea.
- A small line of text framing the M block lightly: "This prompt is your M-Open — the start of a multi-turn exchange. When you're done, you can paste an M-Close into the thread or simply close it."
- A primary "I'm back — share a reflection" button at the bottom that transitions to the Reflection screen.

**D4.9 Reflection screen — expanded with Q and O blocks.**

The Reflection screen is the most visually framework-rich screen. Three block types on one page:

- **R block (reflection textbox):** "Share a short reflection on what changed for you." Amber accent, R icon, "Reflection block" label. Word counter (suggested length 50–250 words).
- **Q block (checkbox group):** Per SPEC v0.2 §6.4 candidate. "Which of these AI-in-teaching practices feels most likely to change something about your teaching this fall?" Five checkboxes. Teal accent, Q icon, "Selection block" label.
- **O block (ranking interaction):** Per SPEC v0.2 §6.4 candidate. "Rank these dimensions of AI-assisted teaching by how much they concern you." Six items, drag-to-reorder or up/down buttons (whichever is more accessible — CC chooses). Orange accent, O icon, "Ordering block" label.

Plus an optional name field at the bottom, and a "Save reflection" primary action.

The Q and O block content for v1 is the candidate content from SPEC v0.2 §6.4. Final content is refined in HANDOFF_02.

Save behavior: POST a reflection record to the Google Form with the payload structure per SPEC v0.2 §5.8. Then transition to a confirmation state on the same screen (don't navigate away) that:

- Confirms the reflection was saved
- Offers two next actions: "Try an X block — open exploration" (transitions to the X screen) or "Start another path" (resets to Step 1 with a new session ID)

**D4.10 X screen — opt-in capstone.**

A new screen reached only by clicking "Try an X block" from the Reflection confirmation state. The X screen carries:

- The X accent (magenta) and "Exploration block" label
- Short orienting text per SPEC v0.2 §6.5: "If you have time, try an X block — open a free exploration with the agent. Type `### X` as your first line and ask anything the workshop didn't address. The thread captures it; we don't grade it."
- A "Copy `### X` prefix" button (a small clipboard convenience — copies just `### X\n` to the clipboard so faculty can paste it as the start of their next message in the GPT thread)
- A "Re-open the Companion in a new tab" link (re-opens the GPT URL, in case the faculty member closed the tab)
- A "Done — start another path" button (returns to Step 1)

No data submission on the X screen. The X block is fully off-platform.

**D4.11 Config-driven content via `companion/config.json`.**

All triage content (Step 1 categories, Step 2 placeholders, Step 4 placeholders, Step 3 fields), the Q and O block content, the agent URL, the form credentials, and the prompt template live in `companion/config.json`. The HTML reads the config on page load and renders accordingly.

Top-level config shape:

```json
{
  "title": "Teaching Inside the Thread",
  "agent_url": "https://chatgpt.com/g/g-6a04e57a41208191ac7ef63d967053f8-amcis-teaching-companion",
  "form": {
    "submission_url": "https://docs.google.com/forms/d/e/1FAIpQLSfr1k5pksXMujds0RpFEdpc8bTVxk5aWaZVyQANSuMn71j5GA/formResponse",
    "entry_type": "entry.1850646152",
    "entry_session_id": "entry.560367375",
    "entry_timestamp": "entry.1473660026",
    "entry_payload": "entry.1114220693"
  },
  "step1": { /* 7 categories + Other */ },
  "step2": { /* placeholder items per category */ },
  "step3": { /* field definitions */ },
  "step4": { /* placeholder items per category × focus pair */ },
  "review": { /* primary button label, copy hints */ },
  "bridge": { /* confirmation text, M-Open framing line */ },
  "reflection": {
    "prompt": "...",
    "q_block": { /* checkbox content */ },
    "o_block": { /* ordering content */ }
  },
  "x_block": { /* orienting text */ },
  "prompt_template": "...slot-substitution template..."
}
```

**D4.12 Prompt assembly — slot substitution.**

The prompt template lives in `config.json` as `prompt_template`. The template uses slot-substitution placeholders (`{step1_label}`, `{step2_label}`, `{course_topic}`, etc.) that get replaced at Review-to-Bridge commit time with the faculty member's actual selections.

The assembled prompt is what gets copied to the clipboard and what gets submitted to the Google Form as part of the triage payload.

CC drafts the v1 prompt template based on the prior platform's template, adapted for the AMCIS audience and the seven-section output schema. Onur reviews in HANDOFF_02.

**D4.13 Data submission helper.**

Implement `submitToGoogleForm(type, sessionId, timestamp, payload)` per the prior platform's pattern: builds a `FormData` object with the four entries keyed by the entry IDs from `config.form`, calls `fetch(config.form.submission_url, { method: 'POST', mode: 'no-cors', body: formData })`, catches errors and logs to console, returns a Promise.

Two submission points:
- **Triage commit** on Review → Bridge transition. Payload is the full triage state (all four steps + the assembled prompt).
- **Reflection save** on Reflection → confirmation transition. Payload is the reflection structure per SPEC v0.2 §5.8 (text + q_responses + o_responses + optional_name).

**D4.14 Session management.**

- `session_id` is a UUID v4 generated on Companion page load and held in the `companionState` object.
- It persists across all screens in the session.
- "Start another path" generates a new session ID.

### Part 5 — Under the Hood spoke (stub)

**D5.1 Author `/under-the-hood/index.html` as an informative stub.**

The Under the Hood stub page contains:

1. **Page header strip** (per shared design system) with Home link.

2. **Hero section.** Title "Under the Hood" plus a one-line subtitle ("How this artifact was designed and built").

3. **Status banner** — a clearly visible note near the top:

   > **This section is in active drafting.** The methodology, workflow exposition, and replication scaffolding will be filled in over the coming weeks alongside the workshop's preparation for AMCIS 2026.

4. **Placeholder section structure.** Render the following section headers as a table of contents, each with a one-paragraph "what this section will contain" stub. Sections:

   - **The Framework, Articulated** — formal articulation of Thread-Centered Pedagogy as a position. ~800 words target.
   - **The Workflow** — the SPEC → HANDOFF → CC discipline used to build this artifact. Will include a polished workflow diagram with hover-explanations on the nodes.
   - **Calibration** — how the AMCIS Teaching Companion's instruction body was developed and tested.
   - **The Agent, Verbatim** — the AMCIS Teaching Companion's instruction body shown in full.
   - **Replication** — invitation for other faculty to adapt this pattern to their own contexts.
   - **References and Acknowledgments** — relevant HCI and IS pedagogy literature; people who contributed.

5. **Byline at the bottom:**

   > Onur Seref · Pamplin College of Business · Virginia Tech

The stub is functional: a reader scrolling through gets a clear picture of what Under the Hood will become, the section structure they can expect, and the framing that the content is in active drafting rather than missing.

CC does NOT draft the substantive content for any of the six sections in HANDOFF_01. Each section gets only its one-paragraph "what this will contain" stub.

---

## Constraints

- **Do not draft real Step 2 or Step 4 content** beyond the placeholders specified. Real content is HANDOFF_02 work.
- **Do not modify the GPT instruction body.** The placeholder body in the GPT is sufficient; calibration is a separate cycle.
- **Do not introduce new dependencies.** No npm packages, no CDN-imported frameworks, no build step. Plain HTML/CSS/JS, served as static files.
- **Single HTML file per spoke.** Each spoke's `index.html` embeds its own page-specific JS and per-page CSS. Shared CSS imports `assets/shared.css`. No splitting into multiple JS files per spoke.
- **No em dashes in user-facing copy.** Including in panel descriptions, button labels, framing text, status banners, anywhere visible to attendees. Internal documents (this HANDOFF, SPEC.md, comments) can use them. The constraint applies to rendered HTML content. (En dashes for date ranges are fine.)
- **No contrastive constructions in user-facing copy.** No "not X, but Y" patterns. Direct positive claims only.
- **Respect SPEC v0.2 verbatim.** If anything in this handoff conflicts with SPEC, SPEC wins. Surface the conflict; do not silently resolve.
- **Preserve the GPT URL and form credentials exactly as given.** No editing, no reformatting.
- **No prior-project lineage on visible pages.** Per SPEC v0.2 §5.5, no references to earlier workshops, no "adapted from" language. The artifact reads as freshly composed for AMCIS.

---

## Expected outputs

**New:**
```
/index.html                       (homepage)
/assets/shared.css                (design system)
/framework/index.html             (3-page slide flow)
/companion/index.html             (state machine)
/companion/config.json            (content + form + agent URL)
/under-the-hood/index.html        (stub)
```

**Onur places (out of scope for CC, but expected before testing):**
```
/assets/slide1.png
/assets/slide2.png
/assets/slide3.png
```

---

## Done criteria

**Architecture and shared CSS:**
- [ ] Directory structure matches §D1.1 exactly.
- [ ] `assets/shared.css` exists with the design tokens, header pattern, button styles, door panel pattern, and block accent palette per §D1.2.
- [ ] All four HTML files import `assets/shared.css`.

**Homepage:**
- [ ] Workshop title and byline render per §D2.1.
- [ ] Three door panels render, each with the correct title and description.
- [ ] Each panel is clickable and navigates to the correct spoke.
- [ ] Layout is responsive (horizontal on wide viewports, vertical on narrow).
- [ ] Footer renders with date stamp.

**The Framework spoke:**
- [ ] Three slide pages render `slide1.png`, `slide2.png`, `slide3.png` respectively.
- [ ] Prev/Next navigation works between slides.
- [ ] Keyboard left/right arrow navigation works.
- [ ] Home link returns to `/amcis-2026/`.
- [ ] Hash routing (`#1`, `#2`, `#3`) works for direct linking.
- [ ] When slide images are missing, placeholder caption shows without breaking layout.

**The Companion spoke — structure:**
- [ ] All eight screens render: Step 1, Step 2, Step 3, Step 4, Review, Bridge, Reflection, X.
- [ ] State machine transitions correctly: forward and backward navigation work pre-commit, locked post-commit.
- [ ] `companionState` object persists across screens; backward navigation does not reset state.
- [ ] Session ID (UUID v4) generated on page load.
- [ ] Block accents render per §D4.2 — light, not loud, consistent with the palette.

**The Companion spoke — content:**
- [ ] Step 1 renders 7 categories + Other per §D4.3.
- [ ] Step 2 renders placeholder items per §D4.4.
- [ ] Step 3 renders the five fields per §D4.5; department dropdown is not present.
- [ ] Step 4 renders placeholder items per §D4.6.
- [ ] Review screen shows all selections with inline Edit affordances.
- [ ] Bridge screen shows the agent URL, the assembled prompt, the "Copy again" button, the M-Open framing line, and the "I'm back" button.
- [ ] Reflection screen shows the R textbox, Q block (checkboxes), O block (ranking), and Save button.
- [ ] X screen shows the orienting text, the `### X` copy button, and the navigation options.

**The Companion spoke — data flow:**
- [ ] Clicking "Copy prompt and open the Companion" copies the assembled prompt to clipboard, opens the GPT URL in a new tab, POSTs the triage record to the Google Form, and transitions to Bridge.
- [ ] Clicking "Save reflection" POSTs the reflection record (including Q and O responses) to the Google Form and transitions to the confirmation state.
- [ ] Both submissions appear as new rows in the connected Google Sheet within a few seconds of each action.
- [ ] Triage payload includes the full assembled prompt.
- [ ] Reflection payload includes Q and O responses.
- [ ] Submission failures are logged to console only — no user-facing error UI.

**Under the Hood spoke:**
- [ ] Page renders with title, subtitle, byline.
- [ ] Status banner is visible and clear.
- [ ] Six placeholder sections are present with one-paragraph stubs each.

**Hygiene:**
- [ ] No em dashes in any rendered HTML content.
- [ ] No contrastive constructions in any rendered HTML content.
- [ ] No new dependencies (no `package.json`, no node_modules, no CDN imports for frameworks).
- [ ] All files are plain HTML/CSS/JS, no build step required.
- [ ] No prior-project lineage on any visible page.

**End-to-end smoke:**
- [ ] Visiting `/amcis-2026/` shows the homepage with three working doors.
- [ ] Clicking each door reaches the corresponding spoke.
- [ ] In The Companion, completing a triage from Step 1 through reflection results in two rows in the Google Sheet (one `triage`, one `reflection`), both with the same session_id.
- [ ] Clicking the X capstone and then "Done" returns to a clean Step 1.

---

## Notes for CC

- Single-file-per-page is preferred. Resist the temptation to split JS into modules; HTML files with embedded `<script>` tags are easier to deploy on GitHub Pages and easier for Onur to inspect.
- The slide image files (`slide1.png` etc.) are placed by Onur. If they're absent when you run, render placeholders and continue — do not block on their absence.
- The Companion's state machine is similar to but not identical to the prior platform's. The structural differences: a new X screen post-Reflection, expanded Reflection with Q and O blocks, no iframe header suppression, light block accents on each screen. Don't copy the prior `index.html` wholesale; adapt thoughtfully.
- The Q block's checkbox content and the O block's ranking content are first-draft per SPEC v0.2 §6.4. They will be refined in HANDOFF_02.
- For the O block's ranking interaction, use up/down buttons rather than drag-and-drop in v1. Drag-and-drop adds accessibility complexity and is harder to test; buttons are simple and screen-reader-friendly. We can upgrade to drag in a later cycle.
- The `### X` copy button copies literally the four characters `### X` followed by a newline. Faculty paste this as the start of their next message in the GPT thread.
- For testing data submission locally, you can simulate the form post with `fetch(... mode: 'no-cors')` — the response will be opaque, but the row should still appear in the sheet. If it doesn't, check the entry IDs against §D4.11.
- Browser console should be silent on successful submissions. Only log on errors.
- If you encounter any ambiguity not resolved by SPEC v0.2 or this HANDOFF, surface it as a question rather than guessing.
