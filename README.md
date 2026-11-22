# FBScript Agent Skills

Portable [Agent Skills](https://agentskills.io) authored and curated by **[Fernando Bittencourt](https://github.com/FernandoBittencourt)**.

This repository is **not** an aggregator of third-party skills. Every published skill is reviewed before merge.

## Skills

| Skill | Version | Description |
| --- | --- | --- |
| [`create-project-cards`](skills/create-project-cards/) | `1.0.0` | Epic → Feature → Task issues on a GitHub Project |

Pin a release with the git tag `create-project-cards@1.0.0` (per-skill SemVer in each `SKILL.md` `metadata.version`).

## Install

Copy or junction the skill folder (must contain `SKILL.md`) into the path your tool loads:

| Tool | Personal | Project |
| --- | --- | --- |
| Cursor | `~/.cursor/skills/<name>/` | `<repo>/.cursor/skills/<name>/` |
| Claude Code | `~/.claude/skills/<name>/` | `<repo>/.claude/skills/<name>/` |
| Codex | `~/.codex/skills/<name>/` | `<repo>/.codex/skills/<name>/` |

Cursor also discovers skills under `~/.claude/skills/` and `~/.codex/skills/`.

### Examples (Windows PowerShell)

```powershell
# Personal (Cursor) — junction to this clone
New-Item -ItemType Junction -Path "$env:USERPROFILE\.cursor\skills\create-project-cards" `
  -Target "C:\Users\ferna\Projects\agent-skills\skills\create-project-cards"

# Or copy
Copy-Item -Recurse .\skills\create-project-cards "$env:USERPROFILE\.cursor\skills\create-project-cards"
```

```bash
# Personal (Unix) — symlink
ln -s /path/to/agent-skills/skills/create-project-cards ~/.cursor/skills/create-project-cards
```

Product-specific board IDs (owner, repo, Project number) belong in the **product** repo (e.g. `docs/GITHUB_PROJECT.md`), not in these skills.

## Versioning

- Each skill has its own SemVer in `metadata.version`.
- There is no global repo SemVer.
- Bump and tag only the skill you changed: `git tag create-project-cards@x.y.z`.

## Contributing

PRs that improve clarity, fixes, or install docs are welcome.

- Behavior changes: open a PR; maintainer validates intent.
- **New skills:** issue or PR — only merged if the maintainer will keep them.
- Do **not** commit secrets, tokens, or private project identifiers into skills.
- PRs that add scripts with network/exfil risk will be rejected or audited line by line.

## License

MIT — see [LICENSE](LICENSE).

Author: [FBSCRIPT](https://fbscript.com.br)
