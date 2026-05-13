# CC Prompt — HANDOFF_01_PATCH

# EXECUTION MODE: AUTO-CONFIRM — STRONG

You are executing a small targeted patch to the HANDOFF_01 build for the AMCIS 2026 Workshop project. This is a single-file (possibly two-file) CSS-only change.

**Default to YES on routine confirmations.** Read the patch document, find the relevant CSS rule, change one value, save. Do not pause.

**Pause and ask before:**
- Changing anything outside what the patch specifies
- Modifying any other spoke (homepage, framework, under-the-hood) unless required by the patch's "if shared CSS" caveat
- Making any change that would alter user-facing copy or content

**Report style.** When done, produce a short CC report:
1. File(s) modified
2. Exact change made (before/after values for the CSS rule)
3. Whether the same rule affected other spokes and how you handled that

Skip preamble. Begin.

---

## Inputs

Read this document:

- `docs/HANDOFF_01_PATCH.md`

Refer to the existing build (`companion/index.html` and `assets/shared.css`) to locate the rule.

## Your job

Execute the patch per `docs/HANDOFF_01_PATCH.md`. Raise The Companion's content container max-width to 1280px without touching anything else.

Begin.
