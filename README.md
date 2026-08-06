# alex-skills

My Claude skills, kept in git so I can version them, diff them, and roll one back when a
"small improvement" makes it worse.

This repo doubles as a plugin marketplace. Everything in it is markdown — no hooks, no MCP
servers, no scripts. Nothing here executes.

Two installs, because Cowork and Claude Code track plugins separately. Same repo for both.

## Install in Cowork

Account-scoped, so do it once and every machine you sign into picks it up. All clicking, no
terminal.

1. Claude desktop app, left sidebar, **Customize**
2. **Plugins** → **Add marketplace**
3. Enter `alex-radengineer/alex-skills` and confirm
4. **Install** on the `engineering-skills` entry

Updating: Customize → Plugins, find the `alex-skills` marketplace, click **Update**. Nothing
auto-updates; pull it after a push.

## Install in Claude Code

Per machine, unlike Cowork.

```bash
claude plugin marketplace add https://github.com/alex-radengineer/alex-skills.git
```

```bash
claude plugin install engineering-skills@alex-skills
```

Use the full `.git` URL. The `owner/repo` shorthand clones over SSH and dies on any machine
without keys loaded in `ssh-agent`. Choose **User scope** when prompted, otherwise the plugin
is tied to a single project.

`engineering-skills@alex-skills` is `plugin-name@marketplace-name`; the marketplace name comes
from `.claude-plugin/marketplace.json`, not from the GitHub repo name.

Pull later changes with `/plugin marketplace update`.

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
