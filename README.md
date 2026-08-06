# alex-skills

My Claude skills, kept in git so I can version them, diff them, and roll one back when a
"small improvement" makes it worse.

This repo doubles as a plugin marketplace. Everything in it is markdown — no hooks, no MCP
servers, no scripts. Nothing here executes.

## Install in Claude Code

```bash
claude plugin marketplace add alex-radengineer/alex-skills
```

```bash
claude plugin install engineering-skills@alex-skills
```

Pull later changes with `/plugin marketplace update`.

## Install in Cowork

Cowork doesn't read git marketplaces; it takes a `.plugin` file instead. Build one from the
repo root:

```bash
zip -r /tmp/engineering-skills.plugin . -x '*.git*' '*.DS_Store' && open /tmp
```

Drop the resulting file into a Cowork chat and accept it. Repeat after any update — there's
no automatic path here yet.

## Skills

| Skill | What it does |
| --- | --- |
| `mechanical-engineering-research` | Thermal-fluid research with source hierarchies and stated validity ranges. Covers CFD setup review, experiment planning, literature reviews, DOE/NSF-style proposal narratives, paper drafting, and invention disclosure support. Nine reference files load on demand. |

Origin: adapted from a skill published through MCPmarket by a University of Arkansas ME
researcher, stripped of its sync plugin and telemetry hooks. Reviewed before import.

## Adding a skill

Make `skills/<skill-name>/SKILL.md` with `name` and `description` in the frontmatter. The
description is what Claude matches against, so write it the way you'd actually ask for the
thing. Bump the version in both files under `.claude-plugin/`, then commit.

Long reference material belongs in `skills/<skill-name>/references/` and gets pulled in only
when it's needed, which keeps the always-loaded part small.

## Before importing anything from outside

Read it first. A `SKILL.md` is a set of instructions Claude will follow, so treat a skill
from a marketplace the way you'd treat a dependency you're about to vendor: check what it
tells the model to do, and check for `hooks/`, `.mcp.json`, or anything under `scripts/`
riding along with it.
