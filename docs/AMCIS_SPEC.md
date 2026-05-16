# AMCIS 2026 Workshop — Project Specification

**Title:** Teaching Inside the Thread: An AI-Centered Pedagogy
**Version:** 0.4
**Last updated:** 2026-05-16
**Workshop date:** Thursday, August 20, 2026 — afternoon session
**Workshop location:** AMCIS 2026, Reno, Nevada
**Duration target:** 90 minutes (collapsible to 45 — see §12)
**Lead facilitator:** Onur Seref (solo)
**Local partner:** Jason Talaei (UNR)
**Inviting authority:** Dean Saonee Sarker (Pamplin), co-chair AMCIS 2026

---

## 1. What this project is

A 90-minute hands-on workshop for IS faculty and doctoral students at AMCIS 2026, delivered through a single public web artifact at `contextmaps.github.io/amcis-2026/`. The artifact is structured as a hub-and-spoke site: a polished homepage with three navigable doors, each leading to one act of the workshop.

The workshop has two co-equal deliverables: (a) a working **Companion Interface** that attendees use live during the session and continue to access afterward, and (b) an **Under the Hood** section that exposes the framework, the design discipline, and the human-AI workflow behind the artifact. The Under the Hood section is the seed of a publishable paper.

The workshop's positioning is the public launch of an AI-Centered Pedagogy, demonstrated through a live Companion Interface artifact, with replication scaffolding for adoption.

The workshop's contract with attendees is the practical one: a useful workshop on AI in teaching that they can apply to their own courses immediately. The framework is the throughline of the experience, not the foreground. Faculty get the utility; the framework is visible to those who lean in.

---

## 2. Pedagogical thesis (the throughline)

Thread-Centered Pedagogy — the working name for the AI-Centered Pedagogy this workshop launches — treats AI-era learning as occurring inside an immutable turn sequence (the thread) rather than alongside the thread as an external tool. The course (or workshop) does not "use" AI; the learner is immersed in AI for the duration. The instructor's role is to design **structured learning blocks** — typed, named, capturable units of interaction — that the learner moves through inside the thread. A lightweight **Companion Interface** sits alongside the AI thread, scaffolding which blocks the learner engages with at which moment, with low-friction copy/paste between Companion and thread.

The framework's claim is that learning protocols decompose into typed units (blocks). The working vocabulary uses R0 (Session Opener), S (Prompt Block), M (Multi-Turn Block), R (Reflection Block), X (Exploration Block), Q (Selection Block), O (Ordering Block). Other instructors could imagine C blocks for computation, T blocks for theory, A blocks for analytics. The framework is the decomposition principle; the letters are one instantiation.

For AMCIS, the workshop is itself an instance of the framework:
- R0 = the platform's assembled prompt that establishes the agent's role
- S = the same assembled prompt, considered as a prompt block
- M = the faculty member's exchange with the agent
- R = the post-exchange reflection
- Q, O = optional structured selections / rankings on the reflection screen
- X = an opt-in free-exploration block at the end

Faculty experience the framework by doing the workshop, not by being lectured on it. The framework is named explicitly in **The Framework** spoke, instanced gently in **The Companion** spoke through light visual cues, and exposed fully in **Under the Hood**.

---

## 3. Conceptual contributions

The design process surfaced eight conceptual claims that the project is making. Each emerged from honest design work rather than top-down theorizing; each is articulable as a position other faculty could adopt, contest, or extend. These contributions belong in the methodology section of the eventual publication.

**About the framework's design discipline:**

1. **Triangulation principle.** Every learning-block interface element must satisfy three dimensions simultaneously: pedagogical action (names a concrete thing the faculty member can do), disciplinary signal (feels recognizable to the field's working vocabulary), and AI agent-compatibility (produces a tractable prompt seed). Items that fail any one dimension fail in practice, even if the other two are strong.

2. **Strategic ontological incompleteness.** Step 2 trees deliberately under-enumerate to preserve "Other" as a generative path rather than a fallback. Faculty agency and AI flexibility are both better served by leaving room than by pre-enumerating every plausible case.

**About what AI is doing to teaching:**

3. **AI pressure as curricular pressure.** AI's effect on courses is not primarily about classroom tool adoption; it reshapes learning outcomes, assessment structures, sequencing, policy, and course architecture itself. AI integration must be modeled as structural educational force, not as add-on enhancement.

4. **Assessment as evidence interpretation under AI conditions.** Assessment's primary challenge in the AI era is not cheating detection but evidence interpretation — what student work *evidences* about student thinking when the work is co-produced with AI. This reframes assessment from cheating prevention toward developmental epistemology.

5. **AI-conditioned cognition inside disciplinary learning.** Even teaching subject-matter content has been changed by AI's presence in students' cognitive environments. Disciplinary content stays, but the cognitive ground underneath it has shifted. Teaching debugging, process redesign, or methods cannot be the same after students have AI co-pilots.

**About what AI is doing to scholarly work:**

6. **AI interaction artifacts as teaching materials.** AI failures, prompt-variation logs, hallucinated outputs, and unstable classifications are legitimate pedagogical content. Teaching *through* AI's limitations is often more pedagogically useful than teaching with AI's polished outputs. The Step 4 materials lists carry this pattern across multiple categories.

7. **AI integration as supervisory negotiation.** AI in scholarly work is a relational and normative process, not a tool-adoption decision. Doctoral supervision under AI presence involves authorship norms, disclosure expectations, developmental judgment, and intellectual ownership — not just productivity workflows.

**The integrating claim:**

8. **AI-mediated interaction as a teachable design space.** Underlying all the above: interaction itself becomes designable. Faculty design not just content and assessment, but the structured shape of student-AI exchanges, the cognitive division of labor, conversational protocols, and reflective interaction patterns. This is what Thread-Centered Pedagogy is, expressed as a teachable design space.

---

## 4. The three-act arc

The workshop's three acts map one-to-one onto the three spokes. The acts are time blocks during live delivery; the spokes are the artifacts that persist after.

### Act 1 — The Framework (20–25 minutes)

Onur presents the framework by navigating through The Framework spoke live, paging through the three slides in sequence. He introduces the block alphabet with self-aware framing — the letters are a working vocabulary in his AI Literacy course, offered as one instantiation of a decomposition principle, not as canonical names.

This act is positioned as a research and pedagogy contribution, not a tutorial. The AMCIS audience studies AI adoption, HCI, and learning environments professionally; they should hear Act 1 as an intellectual offering.

### Act 2 — The Companion (40–45 minutes)

Faculty use The Companion live. They walk through:
- A triage (which functions as R0, establishing what they're doing today and assembling the agent's opening prompt)
- Receipt of the assembled prompt (S block, visible in the UI)
- Transition to the AMCIS Teaching Companion GPT via a Bridge screen
- Their own exchange with the agent (M, in ChatGPT)
- Return to the platform for a free-text reflection (R block)

The block framework is **not surfaced as vocabulary** in The Companion. As of v0.4, the framework's internal vocabulary (M-Open, X-block, Q/O block names) has been removed from the Companion's user-facing surfaces. Faculty experience the framework through the structure of the triage, not through framework terminology. The Framework spoke remains the place where block vocabulary is named and explained for curious users. Light visual accents (block-colored top borders, discreet screen markers) may remain, but no textual framework references appear in the working triage. See §6.2.

**No block engagement is enforced beyond R0.** The platform's assembled prompt is the R0; everything else is invitational. Faculty leave when they're done.

### Act 3 — Under the Hood (20–25 minutes)

Onur opens Under the Hood and walks through the methodology — how each Companion screen maps to a block in the framework, the config-driven structure, the slot-substitution prompt template, the agent definition, the disciplined human-AI workflow used to build the artifact, and the eight conceptual contributions §3 names. He frames his own position: a methodologist who codes but is not a full-stack web developer. The workflow with Claude made building a production artifact possible regardless of where the human's expertise sits. This generalizes.

Act 3 closes with a replication invitation. If time permits, Q&A. If not, Q&A is encouraged in post-conference correspondence.

---

## 5. Site architecture: hub and spoke

The workshop is delivered through a single coherent web artifact at `contextmaps.github.io/amcis-2026/`. One homepage as the canonical entry point, three independently navigable sub-sites as the substantive content.

### 5.1 Hub: the homepage

The homepage is the canonical URL for the workshop. It is the URL distributed to attendees on workshop day (via slide and QR code) and the URL used for citation in the eventual publication.

The homepage carries:
- The workshop title: "Teaching Inside the Thread: An AI-Centered Pedagogy"
- A short conference and authorship line
- Three navigable panels — visual entry points to each spoke
- Minimal additional chrome

### 5.2 Three spokes

**The Framework** (`/framework/`) — three-page slide flow rendering the Framework PNG images (slide1 through slide3).

**The Companion** (`/companion/`) — the hands-on Companion Interface, retuned for AMCIS audience with the locked content design (see §7).

**Under the Hood** (`/under-the-hood/`) — methodology section. As of v0.4, a four-slide flow rendering the Under the Hood PNG images (slide4 through slide7), mirroring the Framework spoke's slide-viewer pattern. The four slides are: (1) the disciplined human-AI development workflow, (2) the orchestration pipeline, (3) the calibration discipline, (4) the AI-centered educational ecosystem. The earlier plan for a prose-based publication-seed page was replaced by the visual slide approach; the eight conceptual contributions (§3) now live in this SPEC and the eventual paper rather than on the public page.

### 5.3 File structure on disk

```
amcis-2026/
├── index.html                  ← hub: homepage
├── assets/
│   ├── shared.css              ← design system across all four pages
│   ├── slide1.png ... slide3.png   ← Framework slides
│   └── slide4.png ... slide7.png   ← Under the Hood slides
├── framework/
│   └── index.html              ← three-slide viewer
├── companion/
│   ├── index.html              ← platform state machine
│   └── config.json             ← content + form + agent URL
└── under-the-hood/
    └── index.html              ← four-slide viewer
```

### 5.4 Shared design system

All four HTML pages import `assets/shared.css`. The shared stylesheet defines color tokens, typography, button styles, and the navigation header pattern (including the VT orange Home button, added in v0.4). Companion-specific primitives (the `tri-*` selection patterns, `plib-*` textarea and counter primitives) live in the Companion page's embedded styles.

---

## 6. Design decisions (settled; do not relitigate without cause)

### 6.1 Hub-and-spoke, not single-page-scroll

Four HTML pages connected by clean navigation. Separates contexts cleanly: pre-workshop review, workshop-day driving, and post-workshop reference all benefit from clean per-spoke navigation.

### 6.2 Visual alignment — framework vocabulary removed from Companion UI

**Revised in v0.4.** Earlier versions specified light block accents (small icons, colored borders, discreet labels) on each Companion screen, with the framework "lightly visible" to attentive users. Workshop-website review (the first feedback round, May 2026) established that the framework's internal vocabulary should not appear in the working triage at all. Faculty should not need to learn the framework's language (M-Open, X-block, Q/O) to use the Companion successfully.

As of v0.4: the Companion's user-facing surfaces carry no textual framework vocabulary. The M-Open explanatory note on the Bridge screen, the Q-block and O-block reflection prompts, and the X-block capstone screen have all been removed (see §7.5, §7.6). Light visual accents that carry no vocabulary (a block-colored top strip, for example) may remain, but nothing on a working triage screen names or explains a block type.

The Framework spoke remains the place where the block alphabet is named and explained, for users who choose to engage with it. The Companion demonstrates the framework through the structure of the experience; it does not teach the framework's terminology.

What we still do not do: full block-explicit UI with bordered cards and prominent block IDs.

### 6.3 Notation — keep, frame as instantiation not canon

The block alphabet (R0/S/M/R/X/Q/O) is preserved as the framework's working vocabulary. Onur introduces it in The Framework spoke with explicit framing that the letters are one instantiation of a decomposition principle, not canonical names. The notation lives in The Framework spoke and in internal documents; it does not appear in the Companion's user-facing triage (see §6.2).

### 6.4 Voluntary engagement only — no enforced block traversal

The platform's assembled prompt **is** the R0. Beyond R0, all block engagement is invitational. The triage and the reflection are available; nothing is required beyond completing the triage to reach the assembled prompt.

### 6.5 Public-surface neutrality — no prior-project lineage on visible pages

The homepage, The Framework, The Companion, and Under the Hood read as freshly composed for this workshop. Thread-Centered Pedagogy is presented as a position Onur has developed and is launching publicly here. Internal documents preserve build lineage; public surfaces stay clean.

### 6.6 Under the Hood and the publication seed

Under the Hood is co-equal to The Companion as a workshop deliverable. As of v0.4 it is implemented as a four-slide visual flow (see §5.2): the methodology, the orchestration pipeline, the calibration discipline, and the AI-centered educational ecosystem.

The eight conceptual contributions named in §3 are **not** rendered on the public Under the Hood page. They were judged too dense for a time-constrained workshop closing (90 minutes, with possible compression). They live in this SPEC (§3) and will form the conceptual core of an SSRN preprint drafted after the workshop. The Under the Hood slides convey the methodology and the rigor of the work; the formal conceptual argument is reserved for the paper.

### 6.7 Agent platform — public ChatGPT Custom GPT

The AMCIS Teaching Companion GPT URL:

```
https://chatgpt.com/g/g-6a04e57a41208191ac7ef63d967053f8-amcis-teaching-companion
```

### 6.8 Data capture — Google Forms

Form credentials:

```
SUBMISSION_URL:   https://docs.google.com/forms/d/e/1FAIpQLSfr1k5pksXMujds0RpFEdpc8bTVxk5aWaZVyQANSuMn71j5GA/formResponse
ENTRY_TYPE:       entry.1850646152
ENTRY_SESSION_ID: entry.560367375
ENTRY_TIMESTAMP:  entry.1473660026
ENTRY_PAYLOAD:    entry.1114220693
```

Submissions land in the `AMCIS 2026 Workshop Responses` sheet owned by `contextmaps@gmail.com`.

### 6.9 Hosting and deployment

- All four spokes hosted at `contextmaps/amcis-2026` deployed at `contextmaps.github.io/amcis-2026/`
- No iframe embedding; The Companion is standalone with its own header
- URL distribution at the workshop only

### 6.10 Skill badge — out of scope for v1

Dropped per §9.10 below.

### 6.11 Fallback for catastrophic failure

If venue Wi-Fi fails, Onur brings a PowerPoint deck walking through workshop content as a presentation. Companion is fail-graceful by design: failed submissions log to console; if GPT is unreachable, assembled prompt is on clipboard for paste into any AI tool.

---

## 7. Content design (locked)

This section captures the full content design developed through three rounds of external review. The complete Step 2 trees and Step 4 materials lists are encoded in `companion/config.json`; what follows is the architectural specification.

### 7.1 Step 1 — Seven categories

1. **Course design and curriculum architecture** — syllabus work, learning outcomes, course-level AI policy, curriculum mapping, course restructuring, new course design
2. **Teaching IS concepts, methods, and technologies** — technical lecture redesign, AI-code-debugging exercises, AI-co-pilot labs, progressive scaffolds, process redesign activities, governance/privacy/accountability units
3. **Cases, scenarios, and applied examples** — discipline-specific examples, AI-decision cases, case adaptation, AI-failure mini-cases, escalating sequences, platform-governance activities
4. **Engagement, interaction, and student-AI protocols** — discussion design, mixed human-AI activities, student-AI exchange protocols, debates, AI-limitation activities, AI-in-peer-review
5. **Assessment and academic integrity in the AI era** — assignment redesign, process-based rubrics, integrity-without-detection strategy, show-your-work requirements, oral defense components, AI-assisted-work feedback systems
6. **Research methods, theory, and evidence** — phenomenon-to-construct translation, theory-building exercises, AI-supported literature synthesis, evaluating AI-generated evidence, human-vs-AI qualitative coding, prompt reproducibility
7. **Doctoral training, supervision, and mentoring** — AI-augmented qualifying exams, dissertation coaching workflows, AI-as-teaching-partner methods modules, responsible-AI-writing supervision norms, AI-assisted-dissertation protocols, AI-supported feedback templates

Plus **Other** (free-text). As of v0.4, Step 1 uses a card-click selection pattern: the seven category cards plus the Other panel sit in a grid; a card is selected by clicking anywhere on its body, with the selection shown by a background color change. The earlier "Pick this area" radio button on each card was removed in the first feedback round. Typing in the Other panel's textarea clears any selected card; selecting a card clears the Other selection (the Other text is preserved). Steps 2 and 4 retain the radio-button + reveal-on-select pattern.

Three categories carry **"Best for..." boundary statements** (categories 3, 6, 7); the other four are self-explanatory from their titles.

### 7.2 Step 2 — Action-shaped focuses

Each Step 1 category has 6 Step 2 items + Other. Items are verb-first, action-shaped phrases sized to be recognized in a scan. Items are roughly ordered from common entry points (top) to more sophisticated moves (bottom).

The drafting discipline applied across all 42 Step 2 items:
- **Triangulation:** every item satisfies pedagogical action × disciplinary signal × AI agent-compatibility
- **Calibration:** roughly two-thirds of items use accessible operational language; one-third carry IS-native vocabulary as the deeper hook, always wrapped in pedagogical action verbs
- **Asymmetry:** categories don't pretend to parallel structure; some are craft-focused, some methodological, some interactional, some normative
- **Developmental language:** failure-pattern items are framed as misconceptions/confusions/distinctions, not as failures or weaknesses

### 7.3 Step 3 — Context fields

Five fields:

1. **Course topic** (free text, ~80 char max) — most informative single field for grounding the agent
2. **Student level** (dropdown: Undergraduate / Master's / Doctoral / Mixed)
3. **Class size** (dropdown: ≤25 / 26-60 / 61-150 / 150+ / Not applicable)
4. **Class format** (dropdown: In-person / Online (synchronous) / Online (asynchronous) / Hybrid)
5. **Teaching context and constraints** (free text, ~280 char max, optional) — replaces the "current approach" and "institution type" fields from earlier drafts; carries whatever constraints actually shape the faculty member's work

No department dropdown (course topic carries disciplinary signal).

### 7.4 Step 4 — Materials per Step 1 × Step 2 path

Each of the 42 Step 1 × Step 2 paths gets its own tailored Step 4 materials list. Step 4 asks: **"What materials or evidence would help the agent do *this specific work* well?"**

Step 4 drafting principles, applied to all 42 paths:
- **Arm's-reach realism** — materials should be things a faculty member actually has on their laptop or in their working context, not theoretically useful artifacts
- **Concrete and specific** — name documents, datasets, policies, workflows, not "course materials"
- **Uploadable or referenceable** — the agent should be able to use what's named
- **3-5 items + "I'm starting from scratch"** as the standard count, sized to what's realistic per path
- **AI interaction artifacts where they land honestly** — hallucinated outputs, prompt-variation logs, AI failures appear in Step 4 as legitimate materials, applied across multiple categories
- **No "Other" required at Step 4** — the materials are tailored; Other is available but less needed

### 7.5 Q and O blocks — removed in v0.4

Earlier versions specified a Q block (checkbox question) and an O block (ranking question) on the reflection screen, intended to demonstrate those block types and to capture reflection-time data that could double as workshop-impact evidence.

**Removed in v0.4.** Workshop-website review concluded that the Q and O blocks asked too much of the user at the end of an otherwise relaxed reflection experience, read as quiz-like, and were a cognitive imposition rather than a contribution. The reflection screen is now a single free-text reflection plus an optional name field. The data trade is accepted: the workshop loses per-user structured opinion data, but the triage selections themselves and the free-text reflection remain as substantive evidence for post-workshop analysis, and the triage selections are arguably a truer signal of faculty intent since they mirror the category panels the user already engaged with.

### 7.6 X block — removed in v0.4

Earlier versions specified an opt-in X block: a post-reflection capstone screen inviting free exploration with the agent.

**Removed in v0.4.** Workshop-website review concluded that the X-block screen was redundant (users in the agent thread can already converse freely without a prompt prefix) and that surfacing X-block vocabulary would confuse rather than help. The standalone X-block screen has been removed. The useful affordance from that screen, a "Re-open the Companion in a new tab" button, has been moved to the post-reflection confirmation panel, which now carries two buttons: "Re-open the Companion in a new tab" and "Done, start another path."

### 7.7 Prompt template

The user's selections substitute into this template:

```
I am an instructor of a [student_level] course teaching [class_format] in a class of [class_size] students.

Course: [course_topic]

[If teaching_context is provided:]
Teaching context and constraints: [teaching_context]

My teaching goal today is in the area of: [step1_goal]
Specifically, I want to: [step2_focus]

Materials I have on hand:
[materials_list, formatted as bullets]

[If materials_other is provided:]
Other materials or constraints: [materials_other]

Please give me a structured, actionable response covering: (1) the recommended AI tool for this work, (2) how to access it, (3) an opening prompt I can paste, (4) follow-up prompts to extend the work, (5) what to expect from a good first response, (6) estimated time, (7) a reflection reminder. Keep your entire response in this single message.
```

The opening sentence uses the "instructor of a [student_level] course" phrasing (revised in v0.4 from the earlier "[student_level] instructor"). The slot-substitution logic handles grammatical edge cases: a blank student level falls back to "I am an instructor teaching..."; a "Not applicable" class size drops the class-size clause; class format renders in natural prose ("in-person", "in a synchronous online format", and so on).

The seven-section output schema is **named inside the prompt itself** rather than left as hidden machinery in the agent's instruction body. This makes the response shape visible to faculty before they paste into the GPT, and provides redundant grounding for the agent.

### 7.8 Agent instruction body

The AMCIS Teaching Companion's instruction body is `docs/AGENT_DEFINITION.md`, at v1.3 as of this SPEC version. It is drafted for the IS audience with the seven-section output schema, the seven-tool universe and filter pattern (ChatGPT primary, Microsoft Copilot demoted to institutional-access-only), the no-preamble/no-epilogue discipline, the substantively-technical register, and a hybrid-input-tolerant fallback. The instruction body was developed through two rounds of external review and then compressed to fit ChatGPT's 8000-character Instructions field limit (the Instructions section is approximately 7,770 characters). The calibrated body is deployed to the live GPT and has been verified working. Further calibration, if needed, edits `docs/AGENT_DEFINITION.md` and re-pastes the Instructions section.

---

## 8. Workflow conventions

The artifact triad discipline:
- **SPEC.md → HANDOFF_NN.md → CC_PROMPT_HANDOFF_NN.md** for every iteration
- **Auto-confirm preamble** for CC prompts ("EXECUTION MODE: AUTO-CONFIRM — STRONG")
- **Per-handoff done-criteria checklists** and CC reports
- **SPEC versioning** with full change log
- **Tone:** direct, warm, unsentimental, no hedging, no apology preamble, no em dashes in user-facing copy, no contrastive constructions in user-facing copy. Pushback is welcomed in conversation.

---

## 9. Timeline

Workshop is August 20, 2026.

**Build phase (completed):**
- HANDOFF_01 and HANDOFF_01_PATCH: hub plus three spokes built; Companion working end-to-end; container width fix
- HANDOFF_02: full content swap, Pamplin-pattern Other UI adoption, seven-section schema surfaced
- Content design completed through three rounds of external review
- HANDOFF_03A: platform UX fixes (Step 1 card-click, Q/O and X removed, framework vocabulary removed, VT orange Home button, Review two-column, grammar fix)
- HANDOFF_03B: Under the Hood implemented as a four-slide viewer
- HANDOFF_03C: homepage header and Under the Hood slide-sizing polish
- Agent instruction body (AGENT_DEFINITION.md v1.3) drafted, reviewed, compressed, deployed to the live GPT, verified
- Draft site shared with Jason Talaei and Dean Sarker by email

**Following weeks:**
- Integrate any feedback returned from Jason Talaei
- GPT calibration follow-up if real-use testing surfaces drift
- Imagemap enhancement brainstorm (deferred, possibly informed by Jason's feedback)
- AMCIS program copy submission; workshop-day URL distribution (slide or QR code)
- Final dry run before AMCIS

---

## 10. Resolved items from prior versions

- Hub-and-spoke architecture (v0.2)
- Title locked (v0.2)
- GPT URL wired (v0.2)
- Google Form credentials verified (v0.2)
- Collapsible 45-minute variant defined (v0.2, §12 below)
- Container width on Companion (HANDOFF_01_PATCH)
- Seven Step 1 categories with revised names (v0.3, §7.1)
- All 42 Step 2 items locked (v0.3, encoded in config.json)
- Step 3 schema revised: class size restored, teaching context replaces institution type (v0.3, §7.3)
- All 42 Step 4 materials trees designed (v0.3, encoded in config.json)
- Prompt template names seven-section schema inline (v0.3, §7.7)
- Eight conceptual contributions identified (v0.3, §3); reserved for the paper, not the public page (v0.4, §6.6)
- HANDOFF_02 executed: content swap, Other UI adoption, seven-section schema surfaced (v0.3 era)
- HANDOFF_03A executed: platform UX fixes, Step 1 card-click redesign, Q/O blocks and X block removed, framework vocabulary removed from Companion UI, VT orange Home button, Review screen two-column, prompt template grammar fix (v0.4, §6.2, §7.1, §7.5, §7.6, §7.7)
- HANDOFF_03B executed: Under the Hood implemented as a four-slide viewer (v0.4, §5.2)
- HANDOFF_03C executed: homepage header centering and Under the Hood slide sizing polish (v0.4)
- Agent instruction body drafted, reviewed, compressed, and deployed to the live GPT as AGENT_DEFINITION.md v1.3; verified working (v0.4, §7.8)
- Outreach email sent to Jason Talaei, Dean Sarker cc'd, sharing the draft site (v0.4)

---

## 11. Open items

- **GPT calibration follow-up.** The agent body (v1.3) is deployed and verified working. Further calibration edits AGENT_DEFINITION.md and re-pastes the Instructions section, only if real-use testing surfaces drift.
- **Feedback from Jason Talaei.** The draft site has been shared. Any feedback returned is integrated as a later handoff. The 45-minute compression question (§12) is handled if Jason raises it; it was not raised in the email.
- **Imagemap enhancement (deferred).** The idea of hover-text on Framework slide regions (originally §2.C) is deferred to later in the summer, possibly informed by Jason's feedback. Not scoped or scheduled.
- **Pre-workshop logistics.** AMCIS program copy submission (text in Appendix A). Slide or QR code production for workshop-day URL distribution.

---

## 12. Collapsible 45-minute variant

If the workshop slot must be shared (for example with a UNR partner session) and compresses to 45 minutes total, the workshop adapts. Same architecture, same Companion artifact; live delivery compresses. This was not raised in the outreach exchange with Jason Talaei; it is retained here as a contingency.

- **Act 1 (The Framework):** 20–25 minutes → 10 minutes. Three slides become a single rapid pass.
- **Act 2 (The Companion):** 40–45 minutes → 25 minutes. Triage and prompt assembly completed; agent exchange abbreviated; reflection kept brief.
- **Act 3 (Under the Hood):** 20–25 minutes → 10 minutes. The four slides become a guided tour rather than detailed exposition; the closing message is preserved.

What is lost: depth of conceptual engagement, depth of agent exchange, reflective time. The artifact still works; live delivery becomes more transactional.

Build for 90. Adapt to 45 only if confirmed necessary.

---

## Appendix A: AMCIS program submission text

For submission to Dean Sarker when she requests program copy.

> **Workshop: Teaching Inside the Thread | [TIME]**
>
> This workshop introduces an AI-Centered Pedagogy for the AI era and demonstrates it through a hands-on learning artifact attendees use during the session and take with them afterward. The framework, Thread-Centered Pedagogy, treats AI-era learning as occurring inside an immutable turn sequence rather than alongside AI tools as an external resource. A lightweight Companion Interface scaffolds the experience without enforcing it. Attendees work through a live triage, receive a tailored prompt, engage with a custom AI agent calibrated for IS faculty, and return to a structured reflection. The session closes with a walkthrough of how the artifact was designed and built. Designed for IS faculty and doctoral students; intermediate level. Pre-requisites: a laptop and a ChatGPT account (free tier acceptable).

Word count: ~135. No em dashes, no contrastive constructions, no badge claim.

---

## Change log

- **v0.4 (2026-05-16):** Bookkeeping pass after the first feedback round; architecture unchanged. HANDOFF_03A: Step 1 redesigned to card-click selection (§7.1); Q and O blocks removed from the reflection screen (§7.5); the X-block capstone screen removed, its reopen button moved to the confirmation panel (§7.6); framework vocabulary removed from the Companion's user-facing surfaces (§6.2, §6.3, §6.4, Act 2); VT orange Home button added; Review screen given a two-column layout; prompt template opening line revised to "instructor of a [student_level] course" (§7.7). HANDOFF_03B: Under the Hood implemented as a four-slide viewer mirroring the Framework spoke, replacing the planned prose stub (§5.2, §5.3, §6.6). HANDOFF_03C: homepage header centered over the panel row, description paragraph widened to panel-row width, Under the Hood slides constrained by height so navigation stays visible. Agent instruction body finalized as AGENT_DEFINITION.md v1.3, compressed to ChatGPT's 8000-character limit, deployed to the live GPT and verified (§7.8). Eight conceptual contributions reserved for the eventual paper rather than rendered on the public Under the Hood page (§6.6). Outreach email sent to Jason Talaei with Dean Sarker cc'd. Imagemap enhancement logged as a deferred open item (§11).
- **v0.3 (2026-05-14):** Major content design lock after three rounds of external review. Seven Step 1 categories with revised names (§7.1). All 42 Step 2 items locked (encoded in config.json). Step 3 schema revised: class size restored, teaching context replaces institution type (§7.3). All 42 Step 4 materials trees designed (encoded in config.json). Prompt template names seven-section schema inline (§7.7). Eight conceptual contributions identified for Under the Hood methodology section (§3). "Building learning artifacts" dropped from Step 1; artifact-building surfaces as Step 2 items in multiple categories. "Cases, examples, and applications" renamed to "Cases, scenarios, and applied examples." "Teaching technical content" renamed to "Teaching IS concepts, methods, and technologies." "Doctoral training and supervision" → "Doctoral training, supervision, and mentoring." New category 6: "Research methods, theory, and evidence." Boundary statements added to three ambiguous categories.
- **v0.2 (2026-05-13):** Hub-and-spoke architecture (§5). Title locked. Three doors named. Public-surface neutrality (§6.5). Skill badge dropped (§6.10). The Companion no longer iframe-embedded (§6.9). Onur sole author on v1 surfaces (§6.6). Collapsible 45-minute variant (§12). GPT URL wired (§6.7). Google Form credentials verified (§6.8). AMCIS program submission text drafted (Appendix A). Open questions from v0.1 resolved.
- **v0.1 (2026-05-13):** Initial draft. Three-act arc settled. Voluntary block engagement throughout. Light visual accents. Under-the-hood page positioned as publication seed. Public ChatGPT Custom GPT for the agent. Google Forms data capture extended for Q/O responses. Step 1 categories revised for IS-dominant-with-breadth audience.
