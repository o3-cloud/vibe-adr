---
status: "accepted"
date: 2025-11-23
decision-makers: ["Owen Zanzal"]
consulted: []
informed: []
ai-agents: ["GPT-5 Codex CLI"]
autonomy-level: "assistive"
tags: ["documentation", "ai", "guardrails"]
---

# Add Anti-Goals & Guardrails to ADRs

## Context and Problem Statement

Current Vibe ADRs clearly describe what we intend to do, but they only implicitly
capture what we will not do and which constraints must not be violated. This works
for careful human readers, but it leaves too much ambiguity for AI agents and busy
collaborators who need fast, machine-friendly guidance on boundaries.

As we lean more on tools like Claude Code, GPT-based CLIs, and other agents to
implement or refactor decisions, we need a dedicated place in each ADR to spell out
explicit non-goals and hard guardrails. Without that, agents may propose solutions
that technically satisfy the outcome but break important invariants, violate safety
constraints, or expand scope beyond what the team intended.

## Vibe Context

Decisions should feel safe, grounded, and bounded. Humans and AI agents should sense
where experimentation is welcome and where it is not. The Vibe ADR format already
captures intent and trade-offs; adding Anti-Goals & Guardrails makes the emotional
tone clearer: "You are free to explore inside this shape, but not beyond it."

## Decision Drivers

- Make it easy for agents to respect scope and constraints
- Reduce accidental overreach or risky suggestions from AI tools
- Keep boundaries visible in the same place humans look for decisions

## Considered Options

- Continue relying on freeform prose to express limits
- Add an explicit **Anti-Goals & Guardrails** section to the template
- Encode anti-goals only as additional YAML metadata fields

## Decision Outcome

Chosen option: **"Add an explicit Anti-Goals & Guardrails section to the template"**,
because it keeps constraints close to the natural-language decision narrative while
remaining easy for both humans and agents to scan and extract. YAML metadata alone
would be harder to maintain and less discoverable for casual readers.

### Anti-Goals & Guardrails

- **Anti-Goals**
  - Do not push constraint tracking into YAML-only metadata or separate documents.
  - Do not let Anti-Goals & Guardrails devolve into vague platitudes; each bullet must be decision-specific.
  - Do not treat the new section as optional when publishing or updating ADRs.
- **Guardrails**
  - Every ADR must include Anti-Goals & Guardrails directly under the Decision Outcome before the Consequences.
  - Authors should cap each list to concise, actionable bullets (2–4) that future agents can checklist.
  - Tooling, prompts, and confirmation steps must reference this section as the canonical boundary description.

### Anti-Goals & Guardrails Pattern

Each ADR based on the Vibe template will add a dedicated section under the Decision
Outcome, with two bullet lists:

- **Anti-Goals** – Outcomes we explicitly do _not_ want, or scopes intentionally left
  out (for example, "do not introduce new services," "does not redesign the API
  surface," "does not add persistence").
- **Guardrails** – Hard constraints or invariants that implementations must respect
  (for example, "must remain backwards compatible with v1 clients," "keep latency
  under 200ms p95," "no new third-party dependencies without review").

Authors should write short, imperative bullets that a future human or AI can easily
use as a checklist while implementing or refactoring.

### Consequences

- Good: Makes decision boundaries explicit for both humans and AI agents
- Good: Provides a standard place to encode scope limits and invariants
- Good: Enables simple tooling to extract constraints for prompts and checks
- Bad: Adds a small authoring overhead to keep Anti-Goals & Guardrails current

### Confirmation

- Update `docs/decisions/VIBE_ADR_TEMPLATE.md` to include an **Anti-Goals & Guardrails**
  section under the Decision Outcome
- Backfill concise Anti-Goals & Guardrails sections into existing ADRs
- Run `npx markdownlint "**/*.md"` to confirm formatting
- Periodically run `npx markdown-link-check README.md docs/decisions/**/*.md` to
  ensure new cross-references remain valid

---

## Pros and Cons of the Options

### Freeform Prose Only

- Good: No template changes required
- Bad: Limits and constraints stay scattered and easy to miss
- Bad: Harder for agents to reliably extract and follow boundaries

### YAML Metadata Only

- Good: Machine-readable and easy to script against
- Good: Fits neatly into existing front matter
- Bad: Less discoverable for humans reading the narrative
- Bad: Encourages terse constraints that may lack nuance

### Template Section (Chosen)

- Good: Gives humans and agents a predictable place to look for boundaries
- Good: Works well in prompts, screenshots, and rendered views
- Good: Flexible enough to mix nuance with structure
- Neutral: Still leaves the door open for optional YAML fields later if needed

---

## More Information

Revisit this decision if Anti-Goals & Guardrails sections consistently go unused or
become noisy. If agents or humans report confusion, consider adding lightweight YAML
fields (`anti-goals`, `guardrails`) that mirror the section content for tooling.

---

# AI-Specific Sections

## AI Guidance Level

Chosen level: **strict**

## AI Tool Preferences

- Primary tool: GPT-5 Codex CLI
- Model/version: GPT-5 (Codex CLI harness)
- Parameters: Default harness settings
- Context files: README.md, docs/decisions/\*.md, docs/decisions/VIBE_ADR_TEMPLATE.md

## Test Expectations

- Test 1: Lint passes with `npx markdownlint "**/*.md"`
- Test 2: Link validation passes with
  `npx markdown-link-check README.md docs/decisions/**/*.md`
- Acceptance criteria: New and updated ADRs include a clear Anti-Goals & Guardrails
  section aligned with this pattern

---

## Next Steps

### Immediate Actions

- Add an **Anti-Goals & Guardrails** section to the Vibe ADR template
- Update recent ADRs (0001, 0002, and future ones) to follow the pattern

### Implementation Sequence

1. Edit `docs/decisions/VIBE_ADR_TEMPLATE.md` to add the section under Decision Outcome
2. Update existing ADRs to define at least 2–3 bullets each for Anti-Goals and Guardrails
3. Incorporate the new section into future agent prompts and llms.txt examples

### Ownership

- Primary implementer: Owen Zanzal
- Supporting roles: GPT-5 Codex CLI
- Stakeholders to notify: Future collaborators relying on ADRs and AI tools

---

## Dependencies

- 0001-adopt-vibe-adr: Adopt Vibe ADR for Decision Records
- 0002-define-llms-txt: Define llms.txt Bootstrap Instructions

---

## Risk Assessment

### Technical Risks

- Risk: Authors may duplicate or contradict other constraints in the ADR  
  Mitigation: Treat Anti-Goals & Guardrails as the single source of truth for
  boundaries and adjust other sections to point to it

### Business Risks

- Risk: Overly strict guardrails could block useful experimentation  
  Mitigation: Encourage authors to keep guardrails focused on invariants, not
  preferences, and to flag experimental ADRs explicitly

---

## Human Review

- Review required: yes
- Reviewers: Owen Zanzal
- Review stage: before
- Review criteria: Clarity of Anti-Goals and Guardrails, consistency with template,
  and usefulness for AI tooling

---

## Feedback Log

### Implementation Notes

- 2025-11-23: ADR drafted via GPT-5 Codex CLI session to standardize boundaries

### AI Agent Feedback

- GPT-5 Codex CLI (2025-11-23): Explicit guardrails and anti-goals greatly improve
  prompt quality and reduce unintended scope creep

---

## Learning Reinforcement

- Making boundaries first-class improves collaboration with agents
- Small, structured sections can significantly raise implementation quality
- Guardrails work best when treated as living, revisitable constraints
