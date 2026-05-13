# AMCIS 2026 Workshop — Project Specification

**Title:** Teaching Inside the Thread: An AI-Centered Pedagogy
**Version:** 0.2
**Last updated:** 2026-05-13
**Workshop date:** Thursday, August 20, 2026 — afternoon session
**Workshop location:** AMCIS 2026, Reno, Nevada
**Duration target:** 90 minutes (collapsible to 45 — see §11)
**Lead facilitator:** Onur Seref (solo)
**Local partner:** Jason Talaei (UNR)
**Inviting authority:** Dean Saonee Sarker (Pamplin), co-chair AMCIS 2026

---

## 1. What this project is

A 90-minute hands-on workshop for IS faculty and doctoral students at AMCIS 2026, delivered through a single public web artifact at `contextmaps.github.io/amcis-2026/`. The artifact is structured as a hub-and-spoke site: a polished homepage with three navigable doors, each leading to one act of the workshop.

The workshop has two co-equal deliverables: (a) a working **Companion Interface** — a triage platform that attendees use live during the session and continue to access afterward — and (b) an **Under the Hood** section that exposes the framework, the design discipline, and the human-AI workflow behind the artifact. The Under the Hood section is the seed of a publishable paper (SSRN preprint, with downstream journal submission).

The workshop's positioning is the public launch of an AI-Centered Pedagogy, demonstrated through a live Companion Interface artifact, with replication scaffolding for adoption.

The workshop's contract with attendees is the practical one: a useful workshop on AI in teaching that they can apply to their own courses immediately. The framework is the throughline of the experience, not the foreground. Faculty get the utility; the framework is visible to those who lean in.

---

## 2. Pedagogical thesis (the throughline)

Thread-Centered Pedagogy — the working name for the AI-Centered Pedagogy this workshop launches — treats AI-era learning as occurring inside an immutable turn sequence (the thread) rather than alongside the thread as an external tool. The course (or workshop) does not "use" AI; the learner is immersed in AI for the duration. The instructor's role is to design **structured learning blocks** — typed, named, capturable units of interaction — that the learner moves through inside the thread. A lightweight **Companion Interface** (HTML + JS + config) sits alongside the AI thread, scaffolding which blocks the learner engages with at which moment, with low-friction copy/paste between Companion and thread.

The framework's claim is that learning protocols decompose into typed units (blocks). Onur's working vocabulary uses R0 (Session Opener), S (Prompt Block), M (Multi-Turn Block), R (Reflection Block), X (Exploration Block), Q (Selection Block), O (Ordering Block). Other instructors could imagine C blocks for computation, T blocks for theory, A blocks for analytics. The framework is the decomposition principle; the letters are one instantiation.

For AMCIS, the workshop is itself an instance of the framework:
- R0 = the platform's assembled prompt that establishes the agent's role
- S = the same assembled prompt, considered as a prompt block
- M = the faculty member's exchange with the agent
- R = the post-exchange reflection
- Q, O = optional structured selections / rankings on the reflection screen
- X = an opt-in free-exploration block at the end

Faculty experience the framework by doing the workshop, not by being lectured on it. The framework is named explicitly in **The Framework** spoke, instanced gently in **The Companion** spoke through light visual cues, and exposed fully in **Under the Hood**.

---

## 3. Site architecture: hub and spoke

The workshop is delivered through a single coherent web artifact at `contextmaps.github.io/amcis-2026/`. The artifact is hub-and-spoke: one homepage as the canonical entry point, three independently navigable sub-sites as the substantive content.

### 3.1 Hub: the homepage

`contextmaps.github.io/amcis-2026/index.html`

The homepage is the canonical URL for the workshop. It is the URL distributed to attendees on workshop day (via slide and QR code) and the URL used for citation in the eventual publication.

The homepage carries:
- The workshop title: "Teaching Inside the Thread: An AI-Centered Pedagogy"
- A short conference and authorship line: "AMCIS 2026 Workshop · Reno, Nevada · August 20, 2026 · Onur Seref, Pamplin College of Business, Virginia Tech"
- Three navigable panels — visual entry points to each spoke. Each panel has a title, a short description (two to three sentences), and clear click affordance.
- Minimal additional chrome. The homepage is the front door; substance lives behind the doors.

The homepage must be polished. It is the first impression for Dean Sarker and Jason during pre-workshop review, and the first impression for attendees on workshop day. A skeletal homepage makes the entire artifact feel skeletal regardless of how strong the spokes are.

### 3.2 Spoke 1: The Framework

`contextmaps.github.io/amcis-2026/framework/`

A small slide deck rendered as a multi-page web flow. Three pages, one slide image per page (the three existing PNGs), with prev/next navigation between pages and a persistent "Back to home" link.

The Framework is the conceptual articulation of Thread-Centered Pedagogy. It is presented during Act 1 of the live workshop by walking through the three slides in sequence; it is also independently navigable post-workshop for anyone who wants to revisit the conceptual material.

PNG images are used directly in v1 (no HTML re-rendering of the slides). A future cycle may re-render the slides as native HTML/CSS for publication-figure quality; this is not required for v1.

### 3.3 Spoke 2: The Companion

`contextmaps.github.io/amcis-2026/companion/`

The hands-on Companion Interface. Substantively the platform pattern Onur has used before, retuned for the AMCIS audience and extended with light block accents, expanded reflection, and an opt-in exploration capstone.

The state machine: Step 1 (teaching goal) → Step 2 (specific focus) → Step 3 (teaching context) → Step 4 (available materials) → Review → Bridge → Reflection (with Q and O blocks) → optional X (exploration capstone).

The Companion is the workshop's hands-on artifact. Attendees use it live during Act 2 to triage their teaching goal, receive a tailored prompt, transition to the AMCIS Teaching Companion GPT, complete the exchange, and return to the platform for reflection.

The Companion is standalone (not iframe-embedded). Its page header carries the workshop title in small text top-left and a "Home" link top-right, anchoring it as part of the workshop site rather than reading as a free-floating tool.

### 3.4 Spoke 3: Under the Hood

`contextmaps.github.io/amcis-2026/under-the-hood/`

The methodology section. v1 ships as an informative stub: title, byline, a paragraph orienting the reader to what this section will contain, and placeholder section headers for the eventual content (workflow diagram, calibration cycles, the SPEC and HANDOFF discipline, the agent's instruction body, replication invitation, references).

The full content matures across subsequent handoffs and alongside the paper draft. The v1 stub is sufficient for Dean Sarker and Jason to see the architectural intent and confirm the direction without forcing premature drafting of the methodology section.

### 3.5 File structure on disk

```
amcis-2026/
├── index.html                  ← hub: homepage
├── assets/
│   ├── shared.css              ← design system across all four pages
│   ├── slide1.png
│   ├── slide2.png
│   └── slide3.png
├── framework/
│   └── index.html              ← three-page slide flow
├── companion/
│   ├── index.html              ← platform state machine
│   └── config.json             ← content + form + agent URL
└── under-the-hood/
    └── index.html              ← stub for v1
```

GitHub Pages serves each `index.html` at its directory route automatically. URLs are `contextmaps.github.io/amcis-2026/`, `.../framework/`, `.../companion/`, `.../under-the-hood/`.

### 3.6 Shared design system

All four HTML pages import `assets/shared.css`. The shared stylesheet defines color tokens, typography, button styles, navigation header pattern, and any plib-equivalent primitives needed across pages.

This is more explicit than the previous platform Onur built (which embedded all CSS in one HTML file because it was one file). With four HTML files, a shared stylesheet is the right factoring.

---

## 4. The three-act arc

The workshop's three acts map one-to-one onto the three spokes. The acts are time blocks during live delivery; the spokes are the artifacts that persist after.

### Act 1 — The Framework (20–25 minutes)

Onur presents the framework by navigating through The Framework spoke live, paging through the three slides in sequence. He introduces the block alphabet with self-aware framing — the letters are a working vocabulary in his AI Literacy course, offered as one instantiation of a decomposition principle, not as canonical names.

This act is positioned as a research and pedagogy contribution, not a tutorial. The AMCIS audience studies AI adoption, HCI, and learning environments professionally; they should hear Act 1 as an intellectual offering.

### Act 2 — The Companion (40–45 minutes)

Faculty use The Companion live. They walk through:
- A triage (which functions as R0 — establishing what they're doing today and assembling the agent's opening prompt)
- Receipt of the assembled prompt (S block, visible in the UI)
- Transition to the AMCIS Teaching Companion GPT via a Bridge screen (where M is gently named but not enforced)
- Their own exchange with the agent (M, in ChatGPT)
- Return to the platform for reflection (R block, optionally accompanied by Q and O blocks)
- An opt-in X block at the end for free exploration

The block framework is **lightly visible** throughout Act 2: small color accents and discreet icons mark each screen with the block it represents. Faculty who don't care barely register the marking. Faculty who lean in see the framework operating in real time, screen by screen.

**No block engagement is enforced beyond R0.** The platform's assembled prompt is the R0; everything else is invitational. The Bridge screen mentions M-Open and M-Close as available framing but does not require their use. The Q and O blocks on the reflection screen are intentionally interesting (see §6.4) but skippable. Faculty leave when they're done.

### Act 3 — Under the Hood (20–25 minutes)

Onur opens Under the Hood and walks through the methodology — how each Companion screen maps to a block in the framework, the config-driven structure, the slot-substitution prompt template, the agent definition, and the disciplined human-AI workflow used to build the artifact. He frames his own position: a methodologist who codes (R, Python) but is not a full-stack web developer. The workflow with Claude made building a production artifact possible regardless of where the human's expertise sits. This generalizes.

Act 3 closes with a replication invitation. If time permits, Q&A. If not, Q&A is encouraged in post-conference correspondence.

---

## 5. Design decisions (settled; do not relitigate without cause)

### 5.1 Hub-and-spoke, not single-page-scroll

The artifact is four HTML pages connected by clean navigation, not one long page with sections. This separates the contexts cleanly: Dean Sarker's review, workshop-day driving, and post-workshop reference all benefit from clean per-spoke navigation. A single long page would force scroll-state coordination that the workshop-day use case cannot tolerate.

### 5.2 Visual alignment — light block accents, not block-explicit

Each screen in The Companion receives a light block accent: a small icon and a thin colored border or top strip in the block's color. An unobtrusive label like "Session opener" or "Prompt block" sits in a corner, easy to ignore. The reflection screen carries a slightly stronger version: the reflection textbox is styled as an R block; below or beside it, one Q block and one O block appear with their own block styling. The opt-in X block at the end is its own screen.

What we do not do: full block-explicit UI with bordered cards, monospace block IDs, and prominent block headers on every screen. That would feel like the workshop is enrolling attendees in a curriculum. The light-accent approach is deliberate.

### 5.3 Notation — keep, frame as instantiation not canon

The block alphabet (R0/S/M/R/X/Q/O) is preserved as the working vocabulary. Onur introduces it in The Framework spoke with explicit framing that the letters are one instantiation of a decomposition principle, not canonical names. Under the Hood reinforces this. Attendees should leave with the framework, not the alphabet, as the portable insight.

### 5.4 Voluntary engagement only — no enforced block traversal

The platform's assembled prompt **is** the R0 — faculty engage with it implicitly by using the platform. **Beyond R0, all block engagement is invitational.**

- **M block.** The Bridge screen mentions that the assembled prompt is the M-Open and that faculty can paste M-Close or just close the thread when done. If this framing risks confusing faculty more than it demonstrates the idea, it should be softened or removed during calibration. The exchange with the agent is whatever the faculty member makes of it.
- **R block.** The reflection screen invites a reflection. It does not require one. Faculty can leave without writing.
- **Q and O blocks.** Intentionally interesting (see §6.4), skippable. The platform does not gate progress on them.
- **X block.** Opt-in. Post-reflection. Faculty who are done can close the platform; faculty who want to keep exploring have a structured way to continue.

This is the load-bearing decision for the workshop's tone. Voluntary interaction throughout. The platform demonstrates the framework by making it available, not by enforcing engagement.

### 5.5 Public-surface neutrality — no prior-project lineage on visible pages

The homepage, The Framework, The Companion, and Under the Hood read as freshly composed for this workshop. No references to prior workshops, no language suggesting this is a "retuned" or "adapted" version of anything earlier. Thread-Centered Pedagogy is presented as a position Onur has developed and is launching publicly here.

Internal documents (this SPEC, HANDOFF files, CC prompts) preserve the build lineage because that lineage matters for the methodology section of the eventual paper. But internal-document language stays internal.

This constraint applies to the agent's instruction body as well. When the AMCIS Teaching Companion's body is calibrated, any language that traces to an earlier audience is rewritten for the IS audience. The body reads as composed for AMCIS.

### 5.6 Under the Hood as publication seed

Under the Hood is co-equal to The Companion as a workshop deliverable. The full content (deferred from v1) will include:
- A clean prose articulation of Thread-Centered Pedagogy (~800 words, written formally enough to be the foundation of an SSRN preprint with minimal editing)
- The three Framework slides as figures
- The Companion Interface as Figure 1 (linked live)
- An annotated walkthrough mapping each Companion screen to its block type
- The SPEC.md from the project (curated for public reading) as the methodology section in seed form
- One HANDOFF as an exhibit of the workflow discipline
- The agent definition shown verbatim
- A short reflection on the workflow ("a methodologist who codes but is not a full-stack web developer; the disciplined workflow with Claude produced this artifact in two days")
- A short references section pulling in HCI and IS pedagogy literature
- An invitation to citation and adoption with contact information

Authorship for v1 is Onur Seref alone. Co-authorship for the eventual paper will be discussed offline with whoever ends up contributing.

### 5.7 Agent platform — public ChatGPT Custom GPT

A public ChatGPT Custom GPT named **AMCIS Teaching Companion** hosts the agent. The GPT URL is:

```
https://chatgpt.com/g/g-6a04e57a41208191ac7ef63d967053f8-amcis-teaching-companion
```

The GPT is currently configured with a placeholder instruction body. The real body is calibrated in a later cycle (HANDOFF_02 or as a separate calibration thread). The placeholder is sufficient for end-to-end platform testing in HANDOFF_01.

**Risk: ChatGPT free-tier message limits.** Faculty on free tier may hit a wall mid-workshop. Mitigation: the agent's instruction body produces a complete structured response in one message. Attendees with Plus accounts are unaffected. Pre-workshop communication encourages Plus accounts where possible.

### 5.8 Data capture — Google Forms

A Google Form owned by `contextmaps@gmail.com` captures triage and reflection submissions. Same pattern Onur has used before, verified working as of 2026-05-13.

**Form credentials:**

```
SUBMISSION_URL:   https://docs.google.com/forms/d/e/1FAIpQLSfr1k5pksXMujds0RpFEdpc8bTVxk5aWaZVyQANSuMn71j5GA/formResponse
ENTRY_TYPE:       entry.1850646152
ENTRY_SESSION_ID: entry.560367375
ENTRY_TIMESTAMP:  entry.1473660026
ENTRY_PAYLOAD:    entry.1114220693
```

The platform POSTs to the `formResponse` endpoint with `mode: "no-cors"`. Submissions land in the connected Google Sheet (`AMCIS 2026 Workshop Responses`) silently, no faculty-visible interruption, no backend, no auth.

**Payload schema for reflection submission** is enriched to capture Q and O block responses:

```json
{
  "type": "reflection",
  "session_id": "uuid-v4",
  "timestamp": "ISO-8601",
  "reflection_text": "...",
  "q_responses": [...],
  "o_responses": [...],
  "optional_name": null
}
```

Q and O responses are explicitly captured because they double as workshop-impact and paper data (see §6.4).

### 5.9 Hosting and deployment

- **All four spokes:** Hosted on GitHub Pages at `contextmaps/amcis-2026` deployed at `contextmaps.github.io/amcis-2026/`.
- **No iframe embedding.** The Companion is standalone. No suppress-header trickery; The Companion has its own polished header treatment.
- **URL distribution:** At the workshop only, via slide and QR code. Pre-workshop distribution to Dean Sarker and Jason is the homepage URL only.

### 5.10 Skill badge — out of scope for v1

The parallel AMCIS workshop offers a skill badge. Matching that signal would require infrastructure work that is unavailable for this iteration (Jim is unavailable due to fall semester start). Decision: drop the badge for v1. Program copy makes no badge claim. Post-conference, the badge can be added if a follow-up engagement justifies the effort.

### 5.11 Fallback for catastrophic failure

If venue Wi-Fi fails entirely, the workshop cannot run the hands-on portion (the agent requires internet). The fallback is a PowerPoint deck Onur brings that walks through the workshop's content as a presentation, with screenshots of the platform substituting for live use. This is a degraded experience by design; the goal is to deliver value even when the tech fails completely.

The Companion itself is fail-graceful by design: if Google Forms is down, submissions log to console and the user experience continues; if the GPT is unreachable, the assembled prompt is on the clipboard and faculty can paste it into any AI tool.

---

## 6. Content design

### 6.1 Step 1 — IS-dominant with broad-applicability options

Step 1 categories for AMCIS:

1. **Course design and architecture** — AI-aware syllabi, curriculum-level AI integration, course planning at higher level (broadly applicable)
2. **Teaching technical content** — IS courses (databases, systems analysis, programming, analytics, ML), technical pedagogy more generally (IS-dominant)
3. **Cases, examples, and applications** — case-method teaching, generating discipline-specific examples, applied scenarios (broadly applicable)
4. **Engagement and interaction** — discussion design, in-class AI activities, student-AI exchange protocols (broadly applicable)
5. **Assessment in the AI era** — assignment design under AI access, rubric revision, integrity strategy (universally relevant)
6. **Doctoral training and supervision** — qualifying exams, dissertation work, research methods training, mentoring with AI (IS-faculty-specific)
7. **Building learning artifacts** — custom GPTs for class, AI study companions, agentic tools (where Phase 3 of the framework intersects with Step 1; IS-dominant)

Each category gets 3–5 Step 2 items. Step 4 materials trees are designed per Step 1 × Step 2 pair, as in the prior platform pattern.

### 6.2 Step 2 — to be drafted

Each of the 7 Step 1 categories needs a Step 2 tree (3–5 items each). Step 2 content drafting is deferred to HANDOFF_02 — it is real content work that benefits from seeing the platform skeleton up first.

For HANDOFF_01, each category gets a single placeholder Step 2 item that proves the wiring works (e.g., "Sample focus area — placeholder for HANDOFF_02"). The faculty experience is broken-as-designed: the platform works end-to-end with placeholder content, ready for content drafting in the next cycle.

### 6.3 Step 3 — IS-appropriate context fields

- **Department dropdown:** removed. All attendees are IS-adjacent.
- **Course topic:** free text. Retained.
- **Student level:** Undergraduate / Master's / Doctoral / Mixed. Retained.
- **Class format:** In-person / Online / Hybrid. Retained.
- **Current approach:** retained, optional, lightly reframed for IS audience.
- **Institution type** (optional new field): R1 / R2 / regional / liberal arts / professional. Affects what advice the agent gives. Decision deferred to content design; default behavior is to include it.

### 6.4 Q and O blocks on the reflection screen — interesting, not pro forma

The Q and O blocks demonstrate framework breadth and produce workshop-impact data. Their content should be genuinely worth answering.

Candidate Q block (checkbox):

> *"Which of these AI-in-teaching practices feels most likely to change something about your teaching this fall?"*
> Options (curated): custom agents for course-specific tasks; assignment redesign under AI access; multi-turn coaching for students; AI-assisted assessment; doctoral student supervision tools.

Candidate O block (ranking):

> *"Rank these dimensions of AI-assisted teaching by how much they concern you."*
> Items: academic integrity; student dependence; equity of access; quality of feedback; faculty workload; curriculum drift.

Final Q and O content is designed during content drafting (HANDOFF_02 or a focused content cycle). The pattern matters more than the specific questions in v1.

### 6.5 X block — opt-in capstone

A final screen offered post-reflection:

> *"If you have time, try an X block — open a free exploration with the agent. Type `### X` as your first line and ask anything the workshop didn't address. The thread captures it; we don't grade it."*

X is the framework's exploration block. Here it is an authentic instance for adults: continue thinking with the agent on your own terms. Faculty who skip it lose nothing; faculty who engage with it experience a fifth framework block in action.

### 6.6 Agent instruction body

The AMCIS Teaching Companion's instruction body is drafted fresh for the IS audience. It carries the same structural pattern as the prior platform's agent (seven-section output, tool-universe filter, no preamble, no epilogue) but the prose itself is composed for AMCIS — no language tracing to a prior audience.

Calibration happens after HANDOFF_01 lands. The placeholder body currently in the GPT is sufficient for platform testing.

Total instruction body should fit comfortably under the ChatGPT GPT character limit. Calibration cycles run pre-workshop.

---

## 7. Workflow conventions

The project follows the artifact triad discipline:

- **SPEC.md → HANDOFF_NN.md → CC_PROMPT_HANDOFF_NN.md** for every iteration
- **Auto-confirm preamble** for CC prompts (the "EXECUTION MODE: AUTO-CONFIRM — STRONG" pattern from prior work)
- **Per-handoff done-criteria checklists** and CC reports
- **SPEC versioning** with full change log
- **Calibration cycles** for the agent definition
- **Tone:** direct, warm, unsentimental, no hedging, no apology preamble, no em dashes in user-facing copy, no contrastive constructions ("not X, but Y") in user-facing copy. Pushback is welcomed in conversation.

---

## 8. Timeline

Working-draft target: two days from HANDOFF_01 execution to a walkable artifact ready for Dean Sarker and Jason review. Workshop is August 20, 2026.

**Day 1:**
- HANDOFF_01 executes (hub + 3 spokes, Companion fully working, Under the Hood as stub)
- End-to-end walkthrough by Onur
- Initial polish pass

**Day 2:**
- HANDOFF_02: Step 2 content drafting, Q/O content drafting, polish
- Calibration cycles on the GPT instruction body begin
- Send draft to Dean Sarker and Jason for feedback

**Following weeks:**
- HANDOFF_03 and beyond: Under the Hood content drafting, agent calibration completion, feedback integration, final QA
- Final dry run before AMCIS

---

## 9. Resolved items from v0.1

- ~~Time allocation with UNR promptathon~~ → Design for 90 minutes canonical, collapsible to 45 if needed (see §11)
- ~~Repo URL and GitHub Pages path~~ → `contextmaps/amcis-2026` → `contextmaps.github.io/amcis-2026/`
- ~~GPT creation timing~~ → Placeholder GPT created, URL wired in HANDOFF_01, body calibrated later
- ~~Skill badge mechanics~~ → Dropped for v1 (see §5.10)
- ~~Authorship slot on Under the Hood~~ → Onur sole author for v1, co-authorship discussed offline as the work matures
- Step 2 content → Deferred to HANDOFF_02 (see §6.2)
- Q and O block specific questions → Deferred to HANDOFF_02 (see §6.4)

---

## 10. Open items

- **HANDOFF_01 execution.** The first build cycle is drafted alongside this SPEC version. CC execution pending.
- **GPT calibration.** Real instruction body is drafted after HANDOFF_01 lands. Calibration cycles follow the pattern of the prior platform's agent calibration.
- **Pre-workshop logistics.** AMCIS program copy submission to Dean Sarker (text drafted in Appendix A). Slide/QR code production for workshop-day URL distribution.
- **Custom domain (post-workshop, optional).** A custom domain like `tcp.contextmaps.org` is a nice-to-have for the publication seed. Not a v1 requirement.

---

## 11. Collapsible 45-minute variant

If Jason Talaei's UNR promptathon partnership consumes 45 minutes of the workshop slot, the workshop compresses to 45 minutes total. This variant uses the same architecture and the same Companion artifact; only the live delivery compresses.

**Compression strategy:**
- **Act 1 (The Framework):** 20–25 minutes compresses to 10 minutes. Three slides become a single rapid pass; the block alphabet is introduced as vocabulary the audience will encounter, not explored conceptually. The framework is named; the depth of its articulation moves to Under the Hood as the take-home material.
- **Act 2 (The Companion):** 40–45 minutes compresses to 25 minutes. Faculty complete the triage, receive the prompt, transition to the GPT, but the agent exchange (M block) is necessarily abbreviated. Q and O blocks remain on the reflection screen but faculty are likely to skip them or answer hastily. The opt-in X capstone is mentioned but not expected to be used during the session.
- **Act 3 (Under the Hood):** 20–25 minutes compresses to 10 minutes. Walkthrough becomes a guided tour rather than a detailed exposition. The replication invitation is preserved.

**What is lost in the 45-minute variant:** depth of conceptual engagement with the framework, depth of agent exchange, and the reflective time that lets the framework reveal land. The artifact still works; the live delivery is more transactional.

Build for 90. Adapt to 45 only if confirmed necessary.

---

## Appendix A: AMCIS program submission text

For submission to Dean Sarker when she requests program copy.

> **Workshop: Teaching Inside the Thread | [TIME]**
>
> This workshop introduces an AI-Centered Pedagogy for the AI era and demonstrates it through a hands-on learning artifact attendees use during the session and take with them afterward. The framework, Thread-Centered Pedagogy, treats AI-era learning as occurring inside an immutable turn sequence rather than alongside AI tools as an external resource. A lightweight Companion Interface scaffolds the experience without enforcing it. Attendees work through a live triage, receive a tailored prompt, engage with a custom AI agent calibrated for IS faculty, and return to a structured reflection. The session closes with a walkthrough of how the artifact was designed and built. Designed for IS faculty and doctoral students; intermediate level. Pre-requisites: a laptop and a ChatGPT account (free tier acceptable).

Word count: ~135. Comparable to the parallel workshop's blurb. No em dashes, no contrastive constructions, no badge claim.

The full title with subtitle ("Teaching Inside the Thread: An AI-Centered Pedagogy") appears on the homepage. The program copy uses the short title.

---

## Change log

- **v0.2 (2026-05-13):** Major refactor. Hub-and-spoke architecture established (§3). Title locked: "Teaching Inside the Thread: An AI-Centered Pedagogy." Three doors named: The Framework, The Companion, Under the Hood. Public-surface neutrality decided (§5.5) — no prior-project lineage on visible pages. Skill badge dropped for v1 (§5.10). The Companion no longer iframe-embedded (§5.9). Onur sole author on v1 surfaces (§5.6). Collapsible 45-minute variant defined (§11). GPT URL wired (§5.7). Google Form credentials verified and recorded (§5.8). AMCIS program submission text drafted (Appendix A). Open questions from v0.1 resolved (§9).
- **v0.1 (2026-05-13):** Initial draft. Three-act arc settled (framework → artifact → under-the-hood). Voluntary block engagement throughout. Light visual accents, not block-explicit UI. Under-the-hood page positioned as publication seed. Public ChatGPT Custom GPT for the agent. Google Forms data capture extended for Q/O responses. Step 1 categories revised for IS-dominant-with-breadth audience.
