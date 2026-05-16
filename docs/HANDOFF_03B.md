# HANDOFF_03B: Implement the Under the Hood spoke

**Project:** AMCIS 2026 Workshop: Teaching Inside the Thread
**Spec reference:** `docs/AMCIS_SPEC.md` v0.3 (SPEC v0.4 update follows separately)
**Workshop date:** 2026-08-20
**Cut:** Small. Replaces the Under the Hood stub with a working four-slide viewer, mirroring the Framework spoke's slide-viewer pattern.

---

## Goal of this iteration

The Under the Hood spoke currently ships as a stub: a placeholder page with an "in active drafting" notice and prose descriptions of sections that were planned but never built. Four slide images for Under the Hood now exist in `assets/`. This handoff replaces the stub with a real four-slide navigable viewer.

The viewer pattern is already proven. The Framework spoke (`framework/index.html`) is a working three-slide viewer with Previous/Next navigation, a slide counter, per-slide captions, and the shared site header. This handoff lifts that exact pattern, adapts it for four slides, and points it at the Under the Hood images.

After this handoff, all three spokes (Framework, Companion, Under the Hood) are functionally complete, and the workshop site is a complete first draft.

---

## Current state of the repository

After HANDOFF_03A executed:

```
/index.html                              (homepage, three doors)
/assets/shared.css                       (design system, VT orange Home button)
/assets/slide1.png, slide2.png, slide3.png   (Framework slides)
/assets/slide4.png, slide5.png, slide6.png, slide7.png   (Under the Hood slides, newly placed)
/framework/index.html                    (working three-slide viewer)
/companion/index.html                    (full Companion state machine)
/companion/config.json                   (full content tree)
/under-the-hood/index.html               (STUB: to be replaced by this handoff)
/docs/AMCIS_SPEC.md                      (v0.3)
/docs/AGENT_DEFINITION.md                (v1.3)
/docs/HANDOFF_*.md, CC_PROMPT_HANDOFF_*.md   (executed handoffs)
/docs/reference/                         (Pamplin reference files)
```

The four Under the Hood slide images are already in place at `assets/slide4.png` through `assets/slide7.png`. This handoff does not create or modify image files.

---

## Reference: how the Framework spoke works

`framework/index.html` is the pattern to mirror. Before doing anything else, CC reads `framework/index.html` in full to understand its structure. Key elements CC will find there:

- The shared site header (the maroon banner, the "Teaching Inside the Thread" text-link top-left, the orange "Home" button top-right)
- A slide display area showing one PNG at a time
- "Previous" and "Next" navigation buttons
- A slide counter ("1 of 3")
- A per-slide caption line
- Keyboard navigation (ArrowLeft / ArrowRight)
- The logic that disables "Previous" on the first slide and "Next" on the last slide

The Under the Hood viewer is the same thing with four slides instead of three.

---

## Deliverables

### D1: Replace the Under the Hood stub

Replace the entire contents of `under-the-hood/index.html`. The current stub content (the "in active drafting" notice, the "The Framework, Articulated" prose section, "The Workflow" prose section, and any other placeholder prose) is removed entirely. Under the Hood becomes purely a four-slide viewer, consistent with how the Framework spoke is purely its three slides with no surrounding prose.

### D2: Implement the four-slide viewer

Build the viewer by lifting the Framework spoke's slide-viewer pattern and adapting it for four slides.

- The viewer displays one slide image at a time, from `assets/slide4.png` through `assets/slide7.png`, in that order.
- Slide order: slide4 (position 1), slide5 (position 2), slide6 (position 3), slide7 (position 4).
- "Previous" and "Next" buttons navigate between slides, styled identically to the Framework spoke's buttons.
- "Previous" is disabled on slide 1 (slide4.png); "Next" is disabled on slide 4 (slide7.png).
- A slide counter displays "1 of 4", "2 of 4", etc., matching the Framework spoke's counter style.
- Keyboard navigation (ArrowLeft / ArrowRight) works, matching the Framework spoke.
- The viewer opens on slide 1 (slide4.png) by default.

### D3: Per-slide captions

Each slide has a caption line beneath it, matching the Framework spoke's caption pattern (the Framework spoke uses captions like "Slide 1 of 3: From AI as Tool to Learning Inside the Thread").

The four Under the Hood captions:

- Slide 1 (slide4.png): "Slide 1 of 4: A Disciplined Human-AI Development Workflow"
- Slide 2 (slide5.png): "Slide 2 of 4: The Orchestration Pipeline, From Specification to Deployed Artifact"
- Slide 3 (slide6.png): "Slide 3 of 4: The Calibration Discipline Behind Trustworthy Assessment"
- Slide 4 (slide7.png): "Slide 4 of 4: The AI-Centered Educational Ecosystem"

### D4: Shared header and navigation

The Under the Hood page uses the same shared site header as the other spokes:

- The maroon banner
- "Teaching Inside the Thread" text-link in the top-left, navigating to the homepage
- The orange "Home" button in the top-right, navigating to the homepage (the VT-orange treatment from HANDOFF_03A)

The page imports `assets/shared.css` for the design system, exactly as the other spokes do.

### D5: No bottom Back-to-Home button

Consistent with HANDOFF_03A's removal of the redundant bottom Back-to-Home button from the Framework spoke, the Under the Hood viewer does not have a bottom Back-to-Home button. The top-left text-link and the top-right Home button are the navigation home. Only the Previous/Next slide navigation appears at the bottom.

---

## Constraints

- **Do not create or modify image files.** The four slide images are already in `assets/`. This handoff only builds the viewer that displays them.
- **Do not modify the Framework spoke, the Companion spoke, the homepage, or `assets/shared.css`.** This handoff touches only `under-the-hood/index.html`. If the viewer needs any new CSS, and that CSS is genuinely specific to the Under the Hood page, it goes in an embedded `<style>` block in `under-the-hood/index.html`. If the Framework spoke's slide-viewer CSS is in `shared.css` and can be reused as-is, reuse it without modification.
- **Do not modify `docs/AMCIS_SPEC.md` or `docs/AGENT_DEFINITION.md`.** SPEC update is handled separately.
- **Do not add new dependencies.** No npm packages, no CDN imports. The Framework spoke's viewer is plain HTML/CSS/JS; the Under the Hood viewer is the same.
- **No em dashes** in any rendered HTML or caption text.
- **No contrastive constructions** in any rendered text.
- **Match the Framework spoke's visual treatment exactly.** The Under the Hood viewer should be visually indistinguishable from the Framework viewer except for the slide images themselves and the captions. Same button styles, same counter style, same caption placement, same layout proportions.

---

## Expected outputs

**Modified files:**

```
/under-the-hood/index.html    (stub replaced with the four-slide viewer)
```

**Unchanged files:**

```
/index.html
/framework/index.html
/companion/index.html
/companion/config.json
/assets/shared.css
/assets/*.png
/docs/*
```

This is a single-file handoff. Only `under-the-hood/index.html` changes.

---

## Done criteria

- [ ] `under-the-hood/index.html` stub content fully removed (no "in active drafting" notice, no placeholder prose sections)
- [ ] The page displays a four-slide viewer
- [ ] Slides display in order: slide4.png, slide5.png, slide6.png, slide7.png
- [ ] "Previous" and "Next" buttons navigate between slides
- [ ] "Previous" is disabled on slide 1; "Next" is disabled on slide 4
- [ ] Slide counter shows "1 of 4" through "4 of 4"
- [ ] Each slide shows its caption line beneath it
- [ ] ArrowLeft / ArrowRight keyboard navigation works
- [ ] The viewer opens on slide 1 (slide4.png)
- [ ] The shared header is present: maroon banner, top-left text-link to home, top-right orange Home button
- [ ] No bottom Back-to-Home button
- [ ] The page imports `assets/shared.css`
- [ ] The viewer is visually consistent with the Framework spoke's viewer
- [ ] No em dashes in any rendered text
- [ ] No new dependencies

**End-to-end smoke (suggested for Onur):**

- [ ] From the homepage, click the Under the Hood door; the four-slide viewer opens on slide 1
- [ ] Page through all four slides with Next; captions update correctly; counter updates
- [ ] Page back with Previous; navigation works in reverse
- [ ] Previous is disabled on slide 1, Next is disabled on slide 4
- [ ] ArrowLeft / ArrowRight keys page through slides
- [ ] The orange Home button and the top-left text-link both return to the homepage
- [ ] The viewer looks consistent with the Framework spoke

---

## Notes for CC

- This is a small handoff. The Framework spoke's slide viewer is working, tested code. Lift it; adapt it for four slides; point it at the Under the Hood images. Do not redesign the viewer or "improve" it. Visual and behavioral consistency with the Framework spoke is the goal.
- The only substantive differences between the Framework viewer and the Under the Hood viewer are: four slides instead of three, different image filenames (slide4-7 instead of slide1-3), different caption strings, and the page title. Everything else is identical.
- If the Framework spoke's viewer CSS lives in `assets/shared.css`, the Under the Hood viewer can reuse those same classes directly. If the Framework viewer's CSS is in an embedded style block in `framework/index.html`, replicate the needed rules in an embedded style block in `under-the-hood/index.html`. Do not modify `shared.css` or `framework/index.html` either way.
- The page `<title>` should be something like "Under the Hood: Teaching Inside the Thread" consistent with how the other spokes title their pages (check what the Framework spoke uses and match the pattern).
