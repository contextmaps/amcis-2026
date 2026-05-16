# HANDOFF_03C: Homepage header polish and Under the Hood slide sizing

**Project:** AMCIS 2026 Workshop: Teaching Inside the Thread
**Spec reference:** `docs/AMCIS_SPEC.md` v0.3
**Workshop date:** 2026-08-20
**Cut:** Small. CSS-only polish. Four fixes across two files, all visual, no logic or content changes. This is the final cleanup before the draft site is shared with reviewers.

---

## Goal of this iteration

The workshop site is a complete, working first draft after HANDOFF_03B. Four small visual issues were caught in a review pass. This handoff fixes all four. Every change is CSS-only. No HTML structure changes, no JavaScript changes, no content changes, no config changes.

After this handoff, the site is ready to be shared with external reviewers.

---

## Current state of the repository

After HANDOFF_03B executed, all three spokes are functional:

```
/index.html                              (homepage, three doors)
/assets/shared.css                       (design system)
/assets/slide1.png ... slide7.png         (Framework + Under the Hood slides)
/framework/index.html                    (three-slide viewer)
/companion/index.html                    (Companion state machine)
/companion/config.json                   (content tree)
/under-the-hood/index.html               (four-slide viewer)
/docs/...                                (specs, handoffs, agent definition)
```

---

## The four fixes

### Fix 1: Homepage header block: center-align

**Current state:** On the homepage (`index.html`), the page title, the conference/location/date line, the author byline, and the description paragraph are all left-aligned, sitting against the left edge of the content area.

**Target state:** The header block is center-aligned over the three door panels below it. Specifically:

- The page title ("Teaching Inside the Thread: An AI-Centered Pedagogy") is centered.
- The conference/location/date line ("AMCIS 2026 Workshop, Reno, Nevada, August 20, 2026") is centered.
- The author byline ("Onur Seref, Pamplin College of Business, Virginia Tech") is centered.
- The description paragraph is handled per Fix 2 below.

The header block (title + details + paragraph) should be horizontally centered over the row of three door panels, so the whole page reads as a balanced, centered composition.

### Fix 2: Homepage description paragraph: width and alignment

**Current state:** The description paragraph above the three door panels is constrained to a narrower max-width than the row of three panels. Its right edge stops short of the panel row's right edge, making the layout look unbalanced.

**Target state:** Two coordinated changes:

1. **Width:** The description paragraph's container is set to the same width as the row of three door panels. The paragraph's right edge aligns with the right edge of the third panel; its left edge aligns with the left edge of the first panel.

2. **Text alignment:** The paragraph's *text* remains left-aligned within that container. The container is centered on the page (consistent with Fix 1), but the paragraph text itself is left-aligned, not center-aligned. A roughly 100-word paragraph is more readable with a clean left edge than with center-aligned ragged text.

So: the paragraph's container is panel-row-width and centered; the text inside it is left-aligned.

### Fix 3: Banner title: no change

**This is a no-op fix, recorded for completeness.** The banner title in the top-left of the shared header reads "Teaching Inside the Thread" (the short form). It was considered whether to expand this to the full title. The decision is to keep it short. The banner title is a persistent navigation element and works best concise; the full title already appears as the homepage H1.

No change is required for Fix 3. It is listed here only so the handoff's fix-numbering matches the review notes that prompted this handoff.

### Fix 4: Under the Hood slide sizing: constrain by height

**Current state:** The Under the Hood spoke (`under-the-hood/index.html`) displays its four slide images constrained by width (the image fills the frame width). The Under the Hood slide images have a different aspect ratio than the Framework slides: they are taller relative to their width. Because the viewer sizes by width, the taller Under the Hood images render tall enough to push the Previous/Next navigation buttons below the visible viewport.

**Target state:** The Under the Hood slide image is constrained by **height** rather than width. Set a max-height on the slide image such that the image, its caption line, and the Previous/Next navigation buttons all fit within a standard viewport without scrolling. The image width scales proportionally; the image is horizontally centered within its frame, which means it will be somewhat narrower than the frame. That is acceptable and expected.

Recommended approach: use a viewport-relative max-height (for example `max-height: 70vh`, tuned to whatever value fits the image plus caption plus nav buttons cleanly at a standard 1080p viewport). A viewport-relative value adapts better across display sizes than a hardcoded pixel height. CC tunes the exact value during implementation.

**Constraint on Fix 4:** This change applies only to the Under the Hood spoke. Do not modify the Framework spoke's slide sizing. The Framework slides have a wider aspect ratio and currently fit correctly; their width-based sizing stays as it is. The two spokes will size their slides differently because their images have different aspect ratios. That is correct and intentional.

---

## Constraints

- **CSS-only.** No HTML structure changes. No JavaScript changes. No content changes. No changes to `companion/config.json`. If a fix appears to require an HTML or JS change, stop and surface it rather than proceeding.
- **Two files only.** Fixes 1 and 2 are in `index.html` (or in `assets/shared.css` if the homepage header styles live there; CC determines which based on where the relevant rules currently are). Fix 4 is in `under-the-hood/index.html` (or `assets/shared.css`, same determination). Fix 3 is a no-op.
- **Do not modify the Framework spoke.** Fix 4 is Under-the-Hood-only. The Framework viewer's slide sizing stays exactly as it is.
- **Do not modify the Companion spoke**, the agent definition, the specs, or any handoff documents.
- **Do not modify image files.**
- **Do not add dependencies.**
- **No em dashes** in any rendered text (none of these fixes add rendered text, but verify nothing is introduced).
- **Preserve all existing behavior.** Navigation, slide viewers, the Companion state machine, data submission: all unchanged. These are visual-only fixes.

---

## Expected outputs

**Modified files:**

```
/index.html                  (Fixes 1 and 2: or assets/shared.css if header styles live there)
/under-the-hood/index.html   (Fix 4: or assets/shared.css if viewer styles live there)
/assets/shared.css           (only if the relevant rules live here rather than in the page files)
```

CC determines whether the relevant CSS lives in the page files' embedded style blocks or in `shared.css`, and edits accordingly. If editing `shared.css`, CC must ensure Fix 4's height constraint is scoped so it applies only to the Under the Hood viewer and not the Framework viewer (for example via a page-specific wrapper class).

**Unchanged files:**

```
/framework/index.html
/companion/index.html
/companion/config.json
/assets/*.png
/docs/*
```

---

## Done criteria

**Fix 1: header centering:**
- [ ] Homepage title is centered
- [ ] Conference/location/date line is centered
- [ ] Author byline is centered
- [ ] The header block is horizontally centered over the three door panels

**Fix 2: description paragraph:**
- [ ] The description paragraph's container width matches the width of the three-panel row
- [ ] The paragraph's left edge aligns with the first panel's left edge
- [ ] The paragraph's right edge aligns with the third panel's right edge
- [ ] The paragraph text itself is left-aligned (not center-aligned)
- [ ] The paragraph container is centered on the page

**Fix 3: banner title:**
- [ ] No change made (no-op, recorded for completeness)

**Fix 4: Under the Hood slide sizing:**
- [ ] Under the Hood slide images are constrained by height, not width
- [ ] The slide image, its caption, and the Previous/Next buttons all fit within a standard 1080p viewport without scrolling
- [ ] The slide image is horizontally centered within its frame
- [ ] The Framework spoke's slide sizing is unchanged
- [ ] If the change was made in `shared.css`, it is scoped to the Under the Hood viewer only

**General:**
- [ ] All changes are CSS-only
- [ ] No HTML structure changes
- [ ] No JavaScript changes
- [ ] No content or config changes
- [ ] All existing behavior preserved
- [ ] No new dependencies

**End-to-end smoke (suggested for Onur):**
- [ ] Homepage: title, details, byline, and paragraph all centered as a balanced block over the three panels
- [ ] Homepage: the description paragraph spans the full panel-row width with left-aligned text
- [ ] Under the Hood: all four slides display with Previous/Next buttons visible without scrolling
- [ ] Under the Hood: slide images are centered and fully visible
- [ ] Framework spoke: slides display exactly as before (unchanged)
- [ ] Companion spoke: unchanged, still works end to end

---

## Notes for CC

- This is a small, visual-only polish handoff. Four fixes, one of which (Fix 3) is a deliberate no-op. The other three are CSS adjustments.
- For Fixes 1 and 2: the homepage header and the three-panel row already have layout containers. The work is aligning the header block's width and centering to the panel row, and setting the description paragraph's container to the panel-row width while keeping its text left-aligned. Find the existing container widths; match them.
- For Fix 4: the Framework viewer and the Under the Hood viewer likely share viewer CSS (HANDOFF_03B lifted the Framework pattern). If they share a class, Fix 4 must be scoped so the height constraint applies only to Under the Hood. A page-specific wrapper class or an Under-the-Hood-specific selector is the clean way to do this. Do not apply the height constraint to the Framework viewer.
- Tune the Fix 4 max-height value by checking that the image, caption, and nav buttons all fit at a standard 1080p viewport. A viewport-relative unit (vh) is preferred over a hardcoded pixel value.
- If any fix cannot be done CSS-only, stop and surface it. Do not make HTML or JS changes without flagging first.
