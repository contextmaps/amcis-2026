# CC Prompt: HANDOFF_03B

# EXECUTION MODE: AUTO-CONFIRM: STRONG

You are executing HANDOFF_03B for the AMCIS 2026 Workshop project. This is a small, single-file handoff: replace the Under the Hood stub page with a working four-slide viewer that mirrors the Framework spoke's existing slide viewer.

**Default to YES on routine confirmations.** This includes modifying `under-the-hood/index.html`. That is the only file this handoff changes.

**Pause and ask before:**
- Modifying any file other than `under-the-hood/index.html`
- Modifying `framework/index.html`, `companion/index.html`, `index.html`, or `assets/shared.css`
- Modifying anything in `docs/`
- Creating or modifying any image file
- Touching files inside `.git/` or outside the project directory
- Adding any dependency

**Report style.** When you finish, produce a single CC report with:
1. File modified (path + summary)
2. Where the slide-viewer pattern was lifted from and how it was adapted
3. Any decisions made where the handoff gave latitude
4. Anything you could not resolve
5. Suggested smoke-test steps

Do not write a long preamble. Read the inputs, execute, report.

---

## Inputs

Read these before doing anything else:

- `docs/AMCIS_SPEC.md`: the v0.3 specification, for project context.
- `docs/HANDOFF_03B.md`: this iteration's unit of work. Read it fully.
- `framework/index.html`: the existing, working three-slide viewer. This is the pattern you will lift and adapt. Read it carefully before writing anything.

## Your job

Per `docs/HANDOFF_03B.md`:

Replace the stub at `under-the-hood/index.html` with a four-slide viewer. The viewer mirrors the Framework spoke's slide-viewer pattern exactly: Previous/Next navigation, slide counter, per-slide captions, keyboard navigation, the shared header with the orange Home button. It displays four images already present in `assets/` (slide4.png through slide7.png) with the four caption strings specified in the handoff.

The handoff document (HANDOFF_03B.md) gives the five deliverables (D1-D5), the constraints, the four caption strings, and the done criteria. Follow it precisely.

## Critical reminders

1. **This is a single-file handoff.** Only `under-the-hood/index.html` changes. Do not modify the Framework spoke, the Companion spoke, the homepage, or `shared.css`.

2. **Lift the Framework viewer; do not redesign it.** The Framework spoke's slide viewer is proven, tested code. The Under the Hood viewer should be visually and behaviorally indistinguishable from it except for the four images, the four captions, and the page title. Do not "improve" the viewer.

3. **The four images already exist.** `assets/slide4.png` through `assets/slide7.png` are in place. This handoff builds the viewer only. Do not create or modify images.

4. **The stub content is fully removed.** The current `under-the-hood/index.html` has an "in active drafting" notice and placeholder prose sections. All of it goes. Under the Hood becomes purely a four-slide viewer, consistent with how the Framework spoke is purely its three slides.

5. **Slide order is slide4 → slide5 → slide6 → slide7.** Captions per the handoff's D3.

6. **No bottom Back-to-Home button.** HANDOFF_03A removed that redundant button from the Framework spoke. The Under the Hood viewer does not have one either. Navigation home is the top-left text-link and the top-right orange Home button.

7. **No em dashes, no new dependencies.**

## Order of operations (suggested)

1. Read `docs/AMCIS_SPEC.md`, `docs/HANDOFF_03B.md`, and `framework/index.html` in full.
2. Identify the Framework viewer's structure: header, slide display, Previous/Next buttons, counter, captions, keyboard handling, the CSS that styles all of it.
3. Build `under-the-hood/index.html` by adapting that structure for four slides.
4. Verify: four slides, correct order, correct captions, navigation bounds (Previous disabled on slide 1, Next disabled on slide 4), keyboard nav, shared header.
5. Produce the report.

## When you finish

Stop and produce the report. Onur will smoke-test locally before pushing to GitHub Pages.

Begin.
