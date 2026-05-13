# HANDOFF_01_PATCH — Companion content container width

**Project:** AMCIS 2026 Workshop — Teaching Inside the Thread
**Spec reference:** `docs/AMCIS_SPEC.md`
**Patches:** `HANDOFF_01.md`
**Cut:** Single targeted fix — content container width on The Companion

---

## Problem

On The Companion's screens, the content container is capped too narrowly. The result is visible on Step 1: the 4×2 grid of category cards forces each card to ~22% of the container width, which forces card headers ("Course design and architecture," etc.) to wrap onto three lines and descriptions to break aggressively. The page is harder to scan and reads as cramped despite plenty of available browser viewport.

The narrow cap was a sensible default for an iframe-embedded layout, where the wrapper provided the outer chrome. The Companion at `contextmaps.github.io/amcis-2026/companion/` is standalone; the wider cap is appropriate.

## Fix

Increase the content container's maximum width on The Companion. Specifically:

1. **Locate** the CSS rule that sets `max-width` on the main content wrapper inside `companion/index.html` (or in `assets/shared.css` if that's where it lives — check both).

2. **Raise the cap** to **`1280px`** (up from whatever the current value is, likely around 960–1100px).

3. **Preserve** the existing horizontal centering (`margin: 0 auto` or equivalent) so the container stays centered on wide viewports.

4. **Preserve** the existing horizontal padding so content does not run flush against the container edges.

5. **Preserve** all responsive behavior. On viewports narrower than 1280px, the container should fill available width minus padding (standard fluid behavior). The change is only to the cap on wide viewports.

## Constraints

- **Do not** modify the Step 1 grid structure (still 4 columns × 2 rows on wide viewports).
- **Do not** modify the card content (titles, descriptions stay verbatim).
- **Do not** change the homepage, framework, or under-the-hood layouts. Only The Companion's content container.
- If the same container class is used across multiple spokes via shared CSS, verify that raising the cap does not break the homepage's door-panel grid or any other spoke's layout. If it would, split the rule so The Companion uses the wider cap and other spokes keep their existing cap.

## Expected outcome

After the fix, with a browser viewport at ~1400px or wider:

- The content container reaches up to 1280px wide (centered with margins on either side on viewports wider than ~1340px).
- Step 1 cards are noticeably wider, around 280-300px each instead of ~220px.
- Card titles wrap onto 1 or 2 lines instead of 3.
- Descriptions wrap into shorter paragraphs (3-4 lines instead of 6-8).
- Vertical height of the Step 1 grid drops correspondingly.

On viewports between 720px and 1280px, the container fills available width (no change in feel).

On viewports below 720px, existing single-column responsive behavior is preserved.

## Done criteria

- [ ] Container max-width on The Companion is 1280px.
- [ ] Step 1 grid still 4×2 on wide viewports; cards are visibly wider.
- [ ] No other spoke's layout is affected.
- [ ] Responsive behavior on narrow viewports is unchanged.
- [ ] No copy or content changes.

## Notes for CC

This is a one-file (possibly two-file) change touching CSS only. Should take a single targeted edit. If you find the width rule is defined in multiple places (e.g., once in shared CSS, once overridden in `companion/index.html`), update at the most specific location and leave broader defaults alone, unless they too are too narrow for The Companion's needs.
