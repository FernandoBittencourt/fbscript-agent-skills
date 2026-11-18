---
name: create-project-cards
description: >
  Create or update GitHub issues and Project cards using an Epic → Feature → Task
  hierarchy. Use when planning epics, features, implementation tasks, or moving
  work to Done on a GitHub Project board.
license: MIT
metadata:
  author: FBSCRIPT
  homepage: https://fbscript.com.br
  version: "1.0.0"
---

# Create project cards

## When to use

- Planning or splitting work into Epic / Feature / Task on GitHub
- Creating or updating issue bodies, labels, and Project board membership
- Recording Done with evidence after the maintainer accepts delivery

Do **not** use for one-line typos or drive-by renames (a Task is enough; skip Epic).

## Resolve board (required)

Never hardcode owner, repo, or Project number in this skill’s instructions for a product.

Resolve in order:

1. `docs/GITHUB_PROJECT.md` in the current workspace (preferred)
2. Project rules that name the GitHub Project / repo
3. Ask the user for owner, repo, and Project number/URL

Use `gh` against that owner/repo/project only.

## Hierarchy

1. **Epic** — versionable delivery; **index of Features** (optional section for tasks with no Feature).
2. **Feature** — playable/technical slice of the Epic; owns the **Tasks** table.
3. **Task** — one implementation/PR unit; body links Epic + Feature.

| Type | Labels | Title |
| --- | --- | --- |
| Epic | `epic` (+ backlog label if the product uses one) | `Epic: …` |
| Feature | area label (e.g. `multiplayer`) — **not** `epic` | `Feature: …` |
| Task | area label | `Area: …` (e.g. `Multiplayer: …`) |

### Inventory rules

- Epic body: table of **Features** (and, only if needed, **Tasks without a Feature**). Do **not** duplicate the Feature’s full task list on the Epic.
- Feature body: `**Epic:** #N` + table **Tasks for this feature**.
- Task body: `**Epic:** #N` and `**Feature:** #M` (or Epic only if orphan task).
- Mark Feature/Task **Done** only with evidence **and** an updated inventory line on the Epic (and Feature, if applicable).

### Create flow

1. Title + labels (table above).
2. Body from templates below.
3. Update Epic inventory (and Feature inventory for a new Task).
4. Add the issue to the resolved GitHub Project.

### Done (maintainer accepted)

1. Comment evidence on the Epic and delivered Feature/Task issues (commit SHA, smoke note — **no secrets**).
2. Move cards to Done: use the product’s Done script if present; otherwise `gh project` / Project UI via `gh`.
3. Close delivered issues; refresh acceptance notes on the Epic body.

## Body templates

### Epic

```markdown
## Context
…

## Features
| Feature | Issue | Status |
| --- | --- | --- |
| … | #… | Todo |

## Tasks without feature (optional)
| Task | Issue | Status |
| --- | --- | --- |

## Acceptance
- [ ] …
```

### Feature

```markdown
**Epic:** #N

## Context
…

## Acceptance criteria
- [ ] …

## Tasks for this feature
| Task | Issue | Status |
| --- | --- | --- |

## Test plan
- [ ] …
```

### Task

```markdown
**Epic:** #N
**Feature:** #M

## Context
…

## Acceptance criteria
- [ ] …

## Test plan
- [ ] …
```

## Anti-patterns

- Creating an Epic for a typo or single-file rename
- Same title used for both a Feature and a Task
- Listing every Task on the Epic when they already live on the Feature
- Assuming a default GitHub user, private repo name, or Project number

## Security

- Never put tokens, `.env` values, API keys, save dumps, personal paths with secrets, or `gh auth` / `GH_TOKEN` output in issue bodies or comments.
- Do not print credentials to the chat or logs when running `gh`.
- Evidence = public commit refs, high-level smoke results, links the repo already exposes.
