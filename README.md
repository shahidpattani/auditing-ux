# auditing-ux
# auditing-ux

A Claude skill for evidence-based UX/UI audits and heuristic evaluations. Turns Claude into a working UX auditor that reasons about real artifacts the way an experienced practitioner would — pulling in the right combination of usability heuristics, cognitive science, accessibility standards, and persuasion ethics for the artifact in front of it, not reciting frameworks from memory.

---

## What it does

Give Claude a screen, a flow, a set of screenshots, or even a written description of one, and this skill produces severity-rated, prioritized findings tied to the actual users and tasks at stake — not a generic checklist.

Every finding earns its place. An observation isn't done until it specifies what's happening, which principle explains why it matters, how bad it is and why, and exactly what to change.

**Scoped requests work just as well as full audits.** "Check this cancellation flow for dark patterns" uses only the relevant lenses. "Run an FTU pass on this onboarding screen" runs the triage layer only. "Audit the whole checkout flow" runs the full machinery.

---

## When to use it

Use this skill whenever you'd ask a UX practitioner to look at something:

- Audit, review, critique, or sanity-check a screen, app, flow, or prototype
- Run a first-time-user (FTU), TRUST, or cognitive-load (COG) quick scan
- Check for dark patterns or ethics issues in a conversion, pricing, or cancellation flow
- Evaluate RTL or multilingual support (Arabic, Hebrew, Persian/Farsi, Urdu, and others)
- Assess accessibility (WCAG 2.2 / POUR)
- Compare a design against a specific heuristic framework
- Get a severity-rated, prioritized list of what to fix before launch

---

## How it works

The skill runs a structured six-phase process:

**Phase 1 — Establish context.** Before touching any framework, understand what the artifact is, who uses it, what the goal of the audit is, and any regulatory or accessibility constraints. The same visual-weight issue carries different severity on a checkout page than on an internal admin tool.

**Phase 1.5 — Triage scan (FTU / TRUST / COG).** A fast practitioner-developed pass that catches what familiarity blinds a team to. Three groups:
- **FTU** — five checks on what a brand-new user can actually do: next action obvious within 5 seconds, no prerequisite knowledge required, recoverable mistakes, useful empty states, jargon budget.
- **TRUST** — seven checks for high-stakes moments: preview before commit, test mode, state clarity, reversibility, audit trail, volume signposting, no dark patterns.
- **COG** — four countable warning flags: decisions before progress, competing primary actions, new concepts per screen, words of body copy.

**Phase 2 — Method selection.** Heuristic evaluation for broad "review this" requests. Cognitive walkthrough when learnability or a specific task is the focus. Accessibility-scoped or persuasion-ethics-scoped reviews when the request is narrower. The method is stated explicitly, once, before diving in — along with the expert-judgment caveat that inspection methods produce informed hypotheses, not validated user data.

**Phase 3 — Lens selection.** Only the frameworks that actually apply to this artifact are loaded. A lookup table maps artifact characteristics to the right reference file — e.g., dense data UIs get Gerhardt-Powals; conversion flows get the persuasion and dark-patterns lens; multilingual interfaces get the i18n/RTL reference. Most audits use three or four lenses, not all thirteen.

**Phase 4 — Walk the artifact.** For each issue: concrete observation → mapped principle(s) → why it matters for these specific users → severity with rationale → specific, actionable recommendation. A deduplication rule prevents counting the same underlying cognitive mechanism twice when multiple lenses point at the same root cause.

**Phase 5 — Consolidate and prioritize.** Group by severity, then by reach. The two or three things that matter most surface at the top, not buried in a flat list ordered by when they were noticed.

**Phase 6 — Report.** A fixed-format output — method/scope, summary, findings table, prioritized next steps — so findings stay comparable across audits and actionable for a team.

---

## Reference library

The skill ships with thirteen reference files, loaded selectively per audit:

| Reference | What it covers |
|---|---|
| `ftu-trust-cog.md` | FTU, TRUST, COG triage checks — run first on most audits |
| `nielsen-heuristics.md` | Nielsen's 10 usability heuristics — baseline lens for almost any audit |
| `shneiderman-golden-rules.md` | Eight golden rules — strongest for multi-step dialogs and task flows |
| `gerhardt-powals-cognitive.md` | Cognitive engineering principles — strongest for data-dense and decision-support UIs |
| `laws-of-ux.md` | Hick's, Fitts's, Miller's, Jakob's, Peak-End — decision load, target acquisition, chunking, conventions, emotionally significant moments |
| `norman-design-principles.md` | Affordances, signifiers, mapping, feedback, Gulf of Execution/Evaluation |
| `gestalt-principles.md` | Visual grouping and perception — layout, hierarchy, scannability |
| `ia-heuristics-covert.md` | Abby Covert's 10 IA heuristics — navigation, search, findability |
| `wcag-accessibility.md` | WCAG 2.2 / POUR with current regulatory dates |
| `i18n-rtl.md` | RTL mirroring, text expansion, pluralization, locale formatting |
| `persuasion-and-dark-patterns.md` | Cialdini's persuasion principles + dual-axis dark-pattern test |
| `severity-and-prioritization.md` | Nielsen's 0–4 severity scale with three-factor rating guidance |
| `inspection-methods.md` | Heuristic evaluation vs. cognitive walkthrough vs. HEART/SUS/PURE |

---

## Output format

Every audit produces a structured report:

```
# UX Audit: [artifact name]

## Method & scope
[Method, lenses applied, scope, expert-judgment caveat]

## Summary
[2–4 sentences: the handful of issues that matter most]

## Findings
| ID | Observation | Principle(s) | Severity | Why it matters here | Recommendation |
|----|-------------|-------------|----------|---------------------|----------------|

## Prioritized next steps
1. [Most important — tied to finding ID, one-line reason]
2. ...
```

The structure is fixed so findings stay comparable across audits. The judgment lives inside each row — not in whether the row exists.

---

## What it won't do

- **Fabricate quantitative scores.** HEART breakdowns, SUS scores, NPS, and PURE difficulty ratings require real usage telemetry or user-administered questionnaires. If asked for these without data, the skill says so and offers the inspection-based alternative.
- **Pad findings to look thorough.** A 6-finding audit with specific, well-reasoned entries is more useful than 25 generic ones. Findings that can't clear the Phase 4 bar — concrete observation, mapped principle, contextual stakes, rated severity with rationale, specific recommendation — don't make it into the table.
- **Apply every framework to every audit.** Loading all thirteen lenses for a focused "check this for dark patterns" request would be noise. The scope of the request determines the scope of the audit.

---

## Repository structure

```
auditing-ux/
├── SKILL.md                              # Main skill instructions
├── assets/
│   └── audit-report-template.md         # Fixed-format output template
└── references/
    ├── ftu-trust-cog.md
    ├── nielsen-heuristics.md
    ├── shneiderman-golden-rules.md
    ├── gerhardt-powals-cognitive.md
    ├── laws-of-ux.md
    ├── norman-design-principles.md
    ├── gestalt-principles.md
    ├── ia-heuristics-covert.md
    ├── wcag-accessibility.md
    ├── i18n-rtl.md
    ├── persuasion-and-dark-patterns.md
    ├── severity-and-prioritization.md
    └── inspection-methods.md
```

---

## Example

**Input:** "Can you look at our signup flow? Users enter email, then password, then full name, then company name, then phone number, then job title, all on separate screens, before they can see the product."

**Finding (abridged):**

> **Observation:** Six sequential screens, each gated behind a "Next" button, before the user reaches any part of the actual product.
>
> **Principle(s):** Hick's Law (sequence length compounds time-to-value) + Nielsen heuristic of user control and freedom (no visible way to skip non-essential fields or preview what's coming next).
>
> **Why it matters here:** For a B2B trial signup where value has to be demonstrated before an evaluator commits, every additional screen before first value is a point where an uncommitted user can abandon. Job title and phone number are classic conversion-killers when front-loaded.
>
> **Severity:** Major (3) — affects 100% of new users on the only path into the product, with no workaround.
>
> **Recommendation:** Collapse to two screens: email + password to create the account; optional company/role fields after the user has seen the product, inside onboarding rather than blocking it.

---

## Version

`v1.1`
