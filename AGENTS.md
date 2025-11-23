# Repository Guidelines

## Project Structure & Module Organization

This workspace centers on living documentation rather than runtime code. Keep the root `README.md` as the north-star narrative, and file new architectural decisions under `docs/decisions/` using sequential, kebab-case filenames (for example, `docs/decisions/0001-adopt-vibe-loop.md`). Reuse `docs/decisions/VIBE_ADR_TEMPLATE.md` as the source of truth; copy it into each new ADR and trim unused sections. Any supporting diagrams or assets should live alongside the ADR that references them (for example, `docs/decisions/assets/0001-sequence.png`) so context never drifts.

## Build, Test, and Development Commands

There is no build pipeline yet, but treat documentation hygiene as the CI equivalent. Run `npx markdownlint "**/*.md"` before opening a PR to catch heading, spacing, and link issues. Use `git diff --stat` to confirm ADRs only touch the intended files, and `gh pr view --web` after pushing to preview rendered Markdown when needed.

## Coding Style & Naming Conventions

Write in concise, actionable prose aimed at future agents and collaborators. Prefer 80–100 character line wraps, ATX headings, and fenced code blocks with language tags. ADR filenames stay sequential, zero-padded to four digits, and use descriptive kebab-case slugs. Within documents, bold key decisions, use bullet lists for drivers and consequences, and keep YAML front matter valid.

## Testing Guidelines

Treat every ADR as a testable hypothesis. Link commits in the `Confirmation` section and describe manual or automated checks that validate the decision. If automated verification exists, document the command (for example, `npm test` or `pytest`) even if it lives outside this repo. Broken links are regressions—run `npx markdown-link-check README.md docs/decisions/**/*.md` when adding cross-references.

## Commit & Pull Request Guidelines

Follow Conventional Commits (`feat:`, `docs:`, `refactor:`) to keep history searchable by intent. Group related ADR changes and their implementation references within a single PR; quote ADR IDs in commit bodies for traceability. PR descriptions should state the problem, summarize the decision, and list validation steps. Include screenshots or rendered previews when the change affects diagrams or rich content.

## Agent Collaboration Tips

Keep agent prompts grounded in the latest ADRs by attaching `README.md`, the relevant `docs/decisions/*.md`, and the template when requesting edits. Ask the agent to outline consequences and follow-up tasks so the ADR stays actionable. After an agent session, update the `Feedback Log` in the ADR with anything notable the model discovered or struggled with.
